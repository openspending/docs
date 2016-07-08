# Load data into OpenSpending

It is possible to load Fiscal Data Packages into OpenSpending via a web app (the Packager) and via a CLI.

## Using the Packager

- [Code repo](https://github.com/openspending/os-packager)
- [Packager URL](http://next.openspending.org/packager)

The Packager provides a simple user interface to load data into OpenSpending. The app is a wizard that guides the user through the uploading of a data source, the modeling of a Fiscal Data Package, the provision of metadata, and publication to the OpenSpending Datastore.

## Using the CLI

- [Code repo](https://github.com/openspending/os-cli)
- [CLI docs](http://docs.openspending.org/en/latest/developers/cli/)

The CLI provides a simple command line interface to interact with an OpenSpending instance. Using the CLI, you can authenticate with an OpenSpending instance and then push data directly to the datastore.

## Walkthroughs

### Load data via the Packager

{
pre. start with two data sources of fiscal data, one that meets the minimum quality requirements, one that does not.
1. Using the bad file, add it in step 1 of the packager, and show the errors found by goodtables
2. Using the good file, add it in step 1 of the packager (after you have cleared the previous step), and see how it is all valid.
3. Proceed to step2, go through the modeling, adding at least one measure and 3 dimensions.
4. Add meta data
5. Check the last step, to see it is all cool.
6. Two options: download; or; publish
7. Got back publish results with link to Viewer.
}

### Load data via the CLI

{
pre. start with two data sources, one good one bad, both already have an FDP.
1. check, validate, etc etc.
2. authenticate with the service.
3. Push files up.
4. Ping for API load status
}
