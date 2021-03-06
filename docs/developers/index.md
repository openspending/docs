# Table of Contents

This section of the OpenSpending documentation is for developers. Here you can learn about the design of the platform, and how to get OpenSpending running locally or on your own servers, and the process for contributing enhancements and bug fixes to the code.

- [Getting started](#getting-started)
- [Platform](#platform)
- [Datastore](datastore/)
- [API](#api)
- [Conductor](#conductor)
- [Packager](#packager)
- [Viewer](#viewer)
- [Views (babbage.ui)](#views)
- [Explorer](#explorer)
- [Auth Client](#auth-client)
- [Data Importers](#data-importers)
- [Monitoring](#monitoring)
- [Status and Incident Notifications](#status-and-incident-notifications)
- [Theming Guide](theming-guide/)
- [Contributing Code](#contributing-code)

# Getting started

Let's get started then! If you want to get the whole OpenSpending platform running locally, or deployed to your own servers, then go straight to the [platform](#platform) section of the documentation. For details on distinct components, go to the appropriate section from the list below.

### Platform

OpenSpending as a complete platform is a set of Docker containers, run via Docker Compose in development. Configurations are available to get running quickly on a local machine, and pre-built Docker images are available for deployment to a remote server for production use. Details to run the platform are available in the central github repository README: https://github.com/openspending/openspending

- [Platform docs and code](https://github.com/openspending/openspending)
- [Platform issues tracker](https://github.com/openspending/openspending/issues)
- [Docker hub organisation](https://hub.docker.com/r/openspending/)

### Datastore

The OpenSpending Datastore is a flat file datastore with source data stored in [Fiscal Data Packages](https://frictionlessdata.io/specs/fiscal-data-package/).

- [Datastore docs](datastore/)

### API

The OpenSpending API offers a rich suite of methods to query the database.

- [os-api docs and code](https://github.com/openspending/os-api)

### Conductor

A set of integration web services for OpenSpending, responsible for identity, notification, and access control.

- [os-conductor docs and code](https://github.com/openspending/os-conductor)

### Packager

The OpenSpending Packager is a Javascript application to validate source data, model it into a Fiscal Data Package, and publish data to the OpenSpending Datastore.

- [os-packager docs and code](https://github.com/openspending/os-packager)

### Viewer

The OpenSpending Viewer is a Javascript application that provides views over data uploaded to OpenSpending.

- [os-viewer docs and code](https://github.com/openspending/os-viewer)

### Views (babbage.ui)

The OpenSpending Views library is a set of JavaScript components for the visualisation of fiscal data.

- [babbage.ui docs and code](https://github.com/openspending/babbage.ui)

### Explorer

The OpenSpending Explorer is a Javascript application that provides an interface to search for and explore the packages available in the OpenSpending database.

- [os-explorer docs and code](https://github.com/openspending/os-explorer)

### Auth Client

The OpenSpending Auth Client is a Javascript library for working with the OpenSpending Auth APIs.

- [Auth Client docs and code](https://github.com/openspending/os-auth-client)

### Data Importers

The Data Importers application is an alternative way to upload data and create Fiscal Datapackages for Openspending. Instead of using the web Packager interface, data publishers can define data sources, field definitions, and additional processor steps, in a source specification file. This 'source-spec' file is used to generate a [Datapackage Pipeline](https://github.com/frictionlessdata/datapackage-pipelines), using the [datapackage-pipelines-fiscal](https://github.com/openspending/datapackage-pipelines-fiscal) plugin.

- [Data Importers docs and code](https://github.com/openspending/os-data-importers)
- [Source spec files used by OpenSpending.org](https://github.com/openspending/os-source-specs)

### Monitoring

Error monitoring with [Sentry](https://sentry.io/) is supported for several of the OpenSpending applications. To configure an application container for Sentry, add the appropriate DSN value as an environmental variable. Sentry DSN values can be found within the Sentry project settings > Client Keys (DSN).

#### Private DSN

Add the environmental variable `SENTRY_DSN` with the appropriate **private** Sentry DSN value for each of the following containers:

- os-api
- os-packager
- os-viewer

#### Public DSN

The following applications require the **public** Sentry DSN key, as it is used by client-side code. Add the environmental variable `SENTRY_PUBLIC_DSN` with the public Sentry DSN value for each of the following containers:

- os-admin
- os-explorer
- os-viewer (os-viewer uses both the private and public DSN keys)

### Status and Incident Notifications

Application availability status for the OpenSpending website and the OpenSpending API is automatically monitored and available from the OpenSpending status dashboard: [https://status.openspending.org/](https://status.openspending.org/).

Users can subscribe to receive notifications about the availability status of OpenSpending, and other ad-hoc incident reports such as scheduled maintenance, from the status dashboard. Click the 'Subscribe' button at the bottom of the page to receive email notifications, or subscribe to the RSS/Atom feeds.

### Contributing Code

Found a bug? Got neat way to refactor an existing code path? Bursting with ideas to make OpenSpending more awesome?

We *can't wait* to see your contributions. Here are a few things that will help:

- All open issues [can be found here](https://github.com/openspending/openspending/issues). If you are working on an existing issue, please let us know by commenting on an issue. Likewise, if you are working on something new, open an issue to let us know.
- We follow a set of [coding standards](https://github.com/okfn/coding-standards), and we have simple examples of those coding standards implemented for [Python](https://github.com/okfn/oki-py) and [Javascript](https://github.com/okfn/oki-js). Please do read before starting.

If anything is unclear, or you just want to talk with other people working on OpenSpending, then catch us on [Gitter.im](http://gitter.im/openspending/chat).
