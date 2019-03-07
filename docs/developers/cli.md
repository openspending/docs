# OpenSpending CLI

A minimal, command line interface to load data into an Open Spending flat file datastore.

## Installation

Ensure you have `Python 2.7, 3.3 or 3.4` installed system-wide or using virtualenv.

Get the code:

```
git clone https://github.com/openspending/os-cli.git
```

To get started install cli:

```
$ python setup.py install
```

You now have `openspending` and `os` (an alias) on your path.

See the help:

```
$ openspending --help
```

## Configuration

The `openspending` CLI uses an `.openspendingrc` file to manage various settings related to you, the user. Default configuration is stored inside the package. User configuration will be merged with default configuration with high priority for user configuration.

When using the CLI, it will look for an `.openspendingrc` file in one of two places, in order:

* The current working directory
* The executing user's $HOME

An example of the basic config file stored in `.openspendingrc`:

```
{
  "api_key": ""
}
```

The CLI has a helper command for working with config files: `openspending config`:

* `openspending config locate`: return the filepath of the currently active config, or `null`.
* `openspending config ensure`: return the filepath of the currently active config, creating a skeleton config first in $HOME if no config is found.
* `openspending config read`: return the currently active config as JSON.
* `openspending config write '<json>'`: write additional data to config file or create a new config file and return the currently active config as JSON.

So, to configure correctly, do the following:

* Create an `.openspendingrc` file as per the above description, or, run `openspending config ensure` to add a skeleton file in your $HOME directory

## Working with data

You'll need some spend data in CSV format. The `examples` directory contains some data to test with.

### Upload

Once you have fully configured your setup, we can get to work.

Here I'll describe the linear sequence for using the CLI, where you can start from having a CSV of spend data, and proceeed through modeling and upload of that data as part of an Open Spending Data Package.

Of course, you can start at any step in the sequence if you know that your data conforms with the previous steps.

#### Step 1. Ensure resources are well formed

Use the Good Tables CLI to ensure there are no obvious structural errors in your resource.

```
$ goodtables structure examples/data_invalid.csv

OOPS.THE DATA IS INVALID :(

META.
Name: structure

###

RESULTS.
+-------------+-----------------------------------------------------------------------+---------------+---------------+
|   row_index | result_message                                                        | result_id     | result_name   |
+=============+=======================================================================+===============+===============+
|           2 | Row 2 is empty.                                                       | structure_005 | Empty Row     |
+-------------+-----------------------------------------------------------------------+---------------+---------------+
|           3 | Row 3 is defective: the dimensions are incorrect compared to headers. | structure_003 | Defective Row |
+-------------+-----------------------------------------------------------------------+---------------+---------------+
```

If you do have errors, you'll get a report similar to that above.

Use that information to fix the errors until you get something like:

```
$ goodtables structure examples/data_valid.csv

WELL DONE! THE DATA IS VALID :)

```

See the [Good Tables documentation](http://goodtables.readthedocs.org/) for more.

#### Step 2. Model the data

Use the `jsontableschema` CLI to infer a model from the data.

Modeling the data means:

* Creating an [Open Spending Data Package](#open-spending-data-package) to "house" the data
* Inferring a schema for the data resources therein (Data Packages use [JSON Table Schema](http://dataprotocols.org/json-table-schema/)).

```
$ jsontableschema infer examples/data_valid.csv
```

**Note:** If your data features both `id` and `amount` fields, then you are not required to provide a mapping via the command line.

See the [jsontableschema documentation](https://github.com/frictionlessdata/jsontableschema-py) for more.

#### Step 3. Validate the model

Use the `validate model` subcommand to ensure that the Data Package descriptor is valid.

Now we actually have a data package and an initial schema for our data, let's check that our data package descriptor is a valid Fiscal Data Package (which it obviously will be if it was created at step 2 ... but let's do it anyway).

```
$ openspending validate model examples/dp-valid
```

To see how it looks for invalid model:

```
$ openspending validate model examples/dp-invalid
```

See the [validate docstring](https://github.com/openspending/oscli-poc/blob/master/oscli/cli.py) for more documentation.

#### Step 4. Check the Data Schema

Use the `validate data` subcommand to ensure that the data conforms to the schema.

```
$ openspending validate data examples/dp-valid
```

To see how it looks for invalid data:

```
$ openspending validate data examples/dp-invalid
```

See the [validate docstring](https://github.com/openspending/oscli-poc/blob/master/oscli/cli.py) for more documentation.

#### Step 5. Upload to the Open Spending datastore

Use the `upload` subcommand to upload a data package to Open Spending.

To make it done there has to be an `api_key` setting in your .openspendingrc.

```
$ openspending upload examples/dp-valid
```

See the [upload docstring](https://github.com/openspending/oscli-poc/blob/master/oscli/cli.py) for more documentation.

### Contributing code

Found a bug? Got neat way to refactor an existing code path? Bursting with ideas to make OpenSpending more awesome?

We *can't wait* to see your contributions. Here are a few things that will help:

- All open issues for the Packager [can be found here](https://github.com/openspending/openspending/issues), labeled "Packager". If you are working on an existing issue, please let us know by commenting on an issue. Likewise, if you are working on something new, open an issue to let us know.
- We follow a set of [coding standards](https://github.com/okfn/coding-standards), and we have simple examples of those coding standards implemented for [Python](https://github.com/okfn/oki-py) and [Javascript](https://github.com/okfn/oki-js). Please do read before starting.

If anything is unclear, or you just want to talk with other people working on OpenSpending, then catch us on [Gitter.im](http://gitter.im/openspending/chat).
