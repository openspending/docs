# OpenSpending Viewer

The OpenSpending Viewer is a Javascript app that provides views over data uploaded to OpenSpending.

The Viewer is the primary way that end users interact with the data of a single data package, and it also provides an example of how to incorporate [OS Views](./views/) into a frontend app.

## Features

- Preview of the resources in a data package.
- Read meta data for a data package.
- Use simplified query interface and a selection of views to visualise the data.
- Perform other core actions for single data packages, such as downloading the raw data sources.

## Requirements

You need to have a recent version of Node.js (v5 and above) to run the Viewer.

If you are not too familiar with Node, do not worry about that. The Viewer is almost completely a frontend Javascript app, with Node.js providing a simple shell and some conveniences for routing and setting environment variables.

The UI is written with [Angular 1](https://angularjs.org), with most of the views being written with [D3](https://d3js.org).

For details on the actual views, see the [OS Views](./views/) documentation.

## Installation

The Viewer can be installed as a component of the Platform, or as a stand alone component.

**Which installation method should you choose?**

- If your goal is to get a full instance of OpenSpending running, then go ahead with the platform installation.
- If you just want to hack on the Viewer (Suggest new features! Fix bugs!), or even run your own Viewer against a remote OpenSpending platform, then follow the standalone install.

If the options are confusing, then go ahead with the standalone install. By default, it runs against the Open Knowledge International instance of OpenSpending, so you'll immediately have lots of data to interact with.

### Platform install

Follow the instructions for installing a development environment for the [OpenSpending platform here](./platform/).

### Standalone install

Follow these steps to get the Viewer running:

```
# get the code
git clone https://github.com/openspending/os-viewer.git

# install dependencies
npm install

# build the frontend assets
npm run build

# run the tests
npm test

# run the server
npm start

# load the app in your default browser
open http://127.0.0.1:5000
```

Based on the default configuration of the Viewer, you can now work with the entire OpenSpending database hosted by Open Knowledge International from your local machine. If you want to point to a different OpenSpending instance, configure your environment variables accordingly based on the details below.

### Customisation

#### Environment variables

OpenSpending Viewer is configured using environment variables. The following variables are available:

- TBD

### Contributing code

Found a bug? Got neat way to refactor an existing code path? Bursting with ideas to make the Viewer more awesome?

We *can't wait* to see your contributions. Here are a few things that will help:

- All open issues for the Viewer [can be found here](http://github.com/openspending/openspending/issues), labeled "Viewer". If you are working on an existing issue, please let us know by commenting on an issue. Likewise, if you are working on something new, open an issue to let us know.
- We follow a set of [coding standards](https://github.com/okfn/coding-standards), and we have simple examples of those coding standards implemented for [Python](https://github.com/okfn/oki-py) and [Javascript](https://github.com/okfn/oki-js). Please do read before starting.

If anything is unclear, or you just want to talk with other people working on OpenSpending, then catch us on [Gitter.im](http://gitter.im/openspending/chat).
