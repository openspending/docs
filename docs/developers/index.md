# Table of Contents

This section of the OpenSpending documentation is for developers. Here you can learn about the design of the platform, and how to get OpenSpending running locally or on your own servers, and the process for contributing enhancements and bug fixes to the code.

- [Getting started](#getting-started)
- [Platform](platform/)
- [Datastore](datastore/)
- [API](api/)
- [Conductor](conductor/)
- [Packager](packager/)
- [Viewer](viewer/)
- [Explorer](explorer/)
- [Views](views/)
- [Auth Client](auth-client/)
- [CLI](cli/)
- [Where Does My Money Go?](wdmmg/)
- [Monitoring](#monitoring)
- [Status and Incident Notifications](#status-and-incident-notifications)
- [Theming Guide](theming-guide/)

# Getting started

Let's get started then! If you want to get the whole OpenSpending platform running locally, or deployed to your own servers, then go straight to the [platform](platform/) section of the documentation. For details on distinct components, go to the appropriate section from the list below.

### Platform

OpenSpending as a complete platform is run as a set of Docker containers via Docker Compose. Configurations are available to get running quickly on a local machine, or a remote server for production use.

- [Platform docs](platform/)

### Datastore

The OpenSpending Datastore is a flat file datastore with source data stored in [Fiscal Data Packages](http://fiscal.dataprotocols.org/spec/).

- [Datastore docs](datastore/)

### API

The OpenSpending API offers a rich suite of methods to query the database.

- [API docs](api/)
- [API code](https://github.com/openspending/os-api)

### Conductor

A set of integration web services for OpenSpending, responsible for identity, notification, and access control.

- [Conductor docs](conductor/)
- [Conductor code](https://github.com/openspending/os-conductor)

### Packager

The OpenSpending Packager is a Javascript application to validate source data, model it into a Fiscal Data Package, and publish data to the OpenSpending Datastore.

- [Packager docs](packager/)
- [Packager code](https://github.com/openspending/os-packager)

### Viewer

The OpenSpending Viewer is a Javascript application that provides views over data uploaded to OpenSpending.

- [Viewer docs](viewer/)
- [Viewer code](https://github.com/openspending/os-viewer)

### Explorer

The OpenSpending Explorer is a Javascript application that provides an interface to explore the packages available in the OpenSpending database.

- [Explorer docs](explorer/)
- [Explorer code](https://github.com/openspending/os-explorer)

### Views

The OpenSpending Views library is a set of JavaScript components for the visualisation of fiscal data.

- [Views documentation](views/)
- [Views code](https://github.com/openspending/babbage.ui/tree/feature/modern)

### Auth Client

The OpenSpending Auth Client is a Javascript library for working with the OpenSpending Auth APIs.

- [Auth Client docs](auth-client/)
- [Auth Client code](https://github.com/openspending/os-auth-client)

### CLI

The OpenSpending CLI is a Python lib and command line interface to interact with an OpenSpending instance.

- [CLI docs](cli/)
- [CLI code](https://github.com/openspending/os-cli)

### Where Does My Money Go?

Where Does My Money Go? is a simple visualisation of government budget and spend data, using the bubble tree and map components.

- [Where Does My Money Go? docs](wdmmg/)
- [Where Does My Money Go? code](https://github.com/openspending/wheredoesmymoneygo.org)

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

Application availability status for the OpenSpending website and the OpenSpending API is automatically monitored and available from the OpenSpending status dashboard: https://status.openspending.org/.

Users can subscribe to receive notifications about the availability status of OpenSpending, and other ad-hoc incident reports such as scheduled maintenance, from the status dashboard. Click the 'Subscribe' button at the bottom of the page to receive email notifications, or subscribe to the RSS/Atom feeds.
