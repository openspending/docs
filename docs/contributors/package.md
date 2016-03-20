# Package data for OpenSpending

OpenSpending "understands" the contents of a source data file via another "descriptor" called a [Fiscal Data Package](http://fiscal.dataprotocols.org/spec/).

In fact, the OpenSpending Datastore does not strictly store any old data file, but rather, it stores Fiscal Data Packages, being a collection of data sources and a `datapackage.json` descriptor file.

## Creating a Fiscal Data Package

At this stage, there are two methods for creating Fiscal Data Packages:

- [OS Packager](https://github.com/openspending/os-packager)
- Manually (not recommended)

We are working on an interactive modeler on the command line, as part of [OS CLI](https://github.com/openspending/os-cli).

## Validating a Fiscal Data Package

Fiscal Data Packages can be validated using the following tools:

- [OS CLI](https://github.com/openspending/os-cli)
- [OS Packager](https://github.com/openspending/os-packager)
- [DataPackage Lib](https://github.com/frictionlessdata/datapackage-py)

## Walkthroughs

### Packaging data with the Packager

{
Load a good data source and go in detail on the modeling process of step2.
}
