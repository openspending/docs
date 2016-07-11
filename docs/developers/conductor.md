# OpenSpending Conductor

OS Conductor is a set of integration web services of OpenSpending Next, responsible for identity, notification, and access control.

Conductor is provided as a [Flask Blueprints](http://flask.pocoo.org/docs/0.10/blueprints/) for inclusion in a Flask codebase, and also includes a minimal Flask app for standalone use.

## Installation

Clone, and pip install -r requirements.txt

## Usage

### Environment variables

Conductor needs some environment variables populated in order to function:

- `OS_ACCESS_KEY_ID`
- `OS_SECRET_ACCESS_KEY`
- `OS_STORAGE_BUCKET_NAME`

## API

Conductor current ships with the following blueprints, and their API endpoints.

### Get authorized upload URL(s)
`/datastore/authorize`

**Method:** `POST`

**Query Parameters:**

 - `jwt` - permission token (received from `/user/authorize`)

**Headers:**

 - `Auth-Token` - permission token (can be used instead of the `jwt` query parameter)

**Body:**

JSON content with the following structure:
```json
{
    "metadata": {
        "owner": "<user-id-of-uploader>",
        "name": "<data-set-unique-id>"
    },
    "filedata": {
        "<relative-path-to-file-in-package>": {
            "length": 1234, #length in bytes of data
            "md5": "<md5-hash-of-the-data>",
            "type": "<content-type-of-the-data>",
            "name": "<file-name>"
        }
    }
}
```

`owner` must match the `userid` that is in the uthentication token.

### Load a datastore package into the OpenSpending DB
`/package/upload`

**Method:** `POST`

**Query Parameters:**

 - `jwt` - permission token (received from `/user/authorize`)
 - `datapackage` - URL of the Fiscal DataPackage to load

### Check on the status of uploading a package to the OpenSpending DB
`/package/status`

**Method:** `GET`

**Query Parameters:**

 - `datapackage` - URL of the Fiscal DataPackage being loaded

**Returns:**

```json
{
    "status": "<status-code>",
    "progress": 123,
    "error": "<error-message-if-applicable>"
}
```

 - `status-code`: one of the following:
    - `queued`: Waiting in queue for an available processor
    - `initializing`: Getting ready to load the package
    - `loading-datapackage`: Reading the Fiscal Data Package
    - `validating-datapackage`: Validating Data Package correctness
    - `loading-resource`: Loading Resource data
    - `deleting-table`: Clearing previous rows for this dataset from the database
    - `creating-table`: Preparing space for rows in the database
    - `loading-data-ready`: Starting to load rows to database
    - `loading-data`: Loading data into the database
    - `creating-babbage-model`: Converting the Data Package into an API model
    - `saving-metadata`: Saving package metadata
    - `done`: Done
    - `fail`: Failed
 - `progress`: # of records loaded so far

Wil return an `HTTP 404` if the package is not being loaded right now.

### Toggle or set a package's privacy setting
`/package/publish`

**Method:** `POST`

**Query Parameters:**

 - `jwt` - permission token (received from `/user/authorize`)
 - `id` - Unique identifier of the datapackage to modify
 - `publish` - Publishing status, either:
    - `true`: force publish,
    - `false`: force private,
    - `toggle`: toggle the state

**Returns:**

```json
{
    "success": true,
    "published": true # or false
}
```

### Search for specific packages
`/search/package`

**Method:** `GET`

**Query Parameters:**

 - `jwt` - authentication token (received from `/user/check`)
 - `q` - match-all query string
 - `package.title` - filter by package title
 - `package.author` - filter by package author
 - `package.description` - filter by package description
 - `package.regionCode` - filter by package region code
 - `package.countryCode` - filter by package region code
 - `package.packageCode` - filter by package region code
 - `size` - number of results to return

All values for all parameters (except `jwt`) should be passed as JSON values.

**Returns:**

All packages that match the filter.

If authentication-token was provided, then private packages from the authenticated user will also be included.
Otherwise, only public packages will be returned.

```json
[
    {
        "id": "<package-unique-id>",
        "model": { ... }, # Babbage model
        "package": { .... }, # Original FDP
        "origin_url": "<url-to-the-datapackage.json>"
    }
]
```

### Check an authentication token's validity
`/user/check`

**Method:** `GET`

**Query Parameters:**

 - `jwt` - authentication token
 - `next` - URL to redirect to when finished authentication

**Returns:**

If authenticated:

```json
{
    "authenticated": true,
    "profile": {
        "id": "<user-id>",
        "name": "<user-name>",
        "email": "<user-email>",
        "avatar_url": "<url-for-user's-profile-photo>",
        "idhash": "<unique-id-of-the-user>",
        "username": "<user-selected-id>"
    }
}
```

If not:

```json
{
    "authenticated": false,
    "providers": {
        "google": {
            "url": "<url-for-logging-in-with-the-Google-provider>"
        }
    }
}
```

When authentication flow is finished, the caller will be redirected to the `next` URL with an extra query parameter
`jwt` which will contain the authentication token. The caller should save this token for further interactions.

### Get permission for a certain user to perform a specific action
`/user/authorize`

**Method:** `GET`

**Query Parameters:**

 - `jwt` - permission token (received from `/user/authorize`)
 - `service` - Service to get permissions for (e.g. `os.datastore`)

**Returns:**

```json
{
    "userid": "<unique-id-of-the-user>",
    "permissions": {
        "permission-x": true,
        "permission-y": false
    },
    "service": "<service-for-which-this-is-relevant>"
}
```

### Change fields in a user's profile
`/user/update`

**Method:** `POST`

**Query Parameters:**

 - `jwt` - authentication token (received from `/user/check`)
 - `username` - If provided, will set the username for the profile (action only allowed once)

**Returns:**

```json
{
    "success": true,
    "error": "<error-message-if-applicable>"
}
```

### Receive authorization public key
`/user/public-key`

**Method:** `GET`

**Returns:**

The conductor's public key in PEM format.

Can be used by services to validate that the permission token is authentic.

### Read authentication JS library
`/user/lib`

**Method:** `GET`

**Returns:**

Authentication Javascript library with Angular 1.x binding.


## Contributing code

Found a bug? Got neat way to refactor an existing code path? Bursting with ideas to make OpenSpending more awesome?

We *can't wait* to see your contributions. Here are a few things that will help:

- All open issues for the Packager [can be found here](http://github.com/openspending/openspending/issues), labeled "Packager". If you are working on an existing issue, please let us know by commenting on an issue. Likewise, if you are working on something new, open an issue to let us know.
- We follow a set of [coding standards](https://github.com/okfn/coding-standards), and we have simple examples of those coding standards implemented for [Python](https://github.com/okfn/oki-py) and [Javascript](https://github.com/okfn/oki-js). Please do read before starting.

If anything is unclear, or you just want to talk with other people working on OpenSpending, then catch us on [Gitter.im](http://gitter.im/openspending/chat).
