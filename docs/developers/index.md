# Table of Contents

This section of the OpenSpending documentation is for developers. Here you can learn about the design of the platform, and how to get OpenSpending running locally or on your own servers, and the process for contributing enhancements and bug fixes to the code.

* [Getting started](#getting-started)
* [Compose](compose/)
* [API](api/)
* [Packager](packager/)
* [Viewer](viewer/)
* [Views](views/)

# Getting started

Let's get started then!

## Run OpenSpending locally

Running OpenSpending on your local development machine is a simple process.

## Deploy OpenSpending elsewhere

You can easily deploy your own instance of OpenSpending.

## Hack on OpenSpending

By now, it should be clear that OpenSpending is not a single monolithic application. Rather, it is a set of modular components that work together to provide the features you know and love. Each component can be installed and used in a standalone fashion, and doing so is the easiest way to fix bugs, enhance functionality, and add features to OpenSpending.

Let's have a look at the components.

### API

The OpenSpending API offers a rich suite of methods to query the database.

* [API documentation](api/)
* [API code](https://github.com/openspending/os-api)

### Datastore

The OpenSpending Datastore is a flat file datastore with source data stored in [Fiscal Data Packages](http://fiscal.dataprotocols.org/spec/).

* [Datastore documentation](datastore/)

### Packager

The OpenSpending Packager is a Javascript application to validate source data, model it into a Fiscal Data Package, and publish data to the OpenSpending Datastore.

* [Packager documentation](packager/)
* [Packager code](https://github.com/openspending/os-packager)

### Viewer

The OpenSpending Viewer is a Javascript application that provides views over data uploaded to OpenSpending.

* [Viewer documentation](viewer/)
* [Viewer code](https://github.com/openspending/os-viewer)

### Views

The OpenSpending Views library is a set of JavaScript components for the visualisation of fiscal data.

* [Views documentation](views/)
* [Views code](https://github.com/openspending/babbage.ui)

### Registry

The OpenSpending Registry is an app to explore and discover data available via the OpenSpending API.

* [Registry documentation](registry/)
* [Registry code](https://github.com/openspending/os-registry)
