# OpenSpending Conductor

OS Conductor is a set of integration web services of OpenSpending Next, responsible for identity, notification, and access control.

Conductor is provided as a [Flask Blueprints](http://flask.pocoo.org/docs/0.10/blueprints/) for inclusion in a Flask codebase, and also includes a minimal Flask app for standalone use.

## Installation

Clone, and pip install -r requirements.txt

## Usage

### Environment variables

Conductor needs some environment variables populated in order to function:

- `OPENSPENDING_ACCESS_KEY_ID`
- `OPENSPENDING_SECRET_ACCESS_KEY`
- `OPENSPENDING_STORAGE_BUCKET_NAME`

### API

Conductor current ships with the following blueprints, and their API endpoints.

#### Datastore

- `/datastore/authorize` - get authorized upload URL

#### Authorization

To be documented.

#### Authentication

To be documented.

#### API Load

- `/hooks/load/api`
  - `POST` to initiate loading of an FDP to the OS API
  - `GET` to get the status for loading of an FDP to the OS API
-  `/hooks/load/callback` - internal api for the OS API server to report on FDP loading status
