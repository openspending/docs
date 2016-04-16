# OpenSpending Views

The OpenSpending Views library is a set of JavaScript components for the visualisation of fiscal data. As all views on data are currently powered by the Analytical API of OpenSpending (Babbage), the views are implemented completely as [Babbage.UI](https://github.com/openspending/babbage.ui).

## Features

- Javascript client for Babbage APIs
- A suite of view components for a range of common data visualisations
- Bindings for Angular 1.x
- Modular design to enable alternative bindings (React, Ember, Vanilla JS)

## Requirements

You need to have a recent version of Node.js (v5 and above) to work with the Views. The Views are largely designed for use in other applications. The [OpenSpending Viewer](./viewer/) is an example of such an application.

## Installation

The Views are install as part of the OpenSpending Platform inside the [Viewer](./viewer/). If you want to work with the views directly, clone the repo and run WebPack.

## Components

The library currently ships with the following components.

- API: A client for a Babbage API server
- Drilldown: Treemap, Pie Chart, Bubble Tree, GoewView
- Sortable-Series: Bar Chart, Table
- Time-Series: Line/Area Chart
- 2D-Table: Pivot Table

We would be *delighted* to accept Pull Requests that add new views, or add new bindings for other Javascript frameworks.

### Contributing code

Found a bug? Got neat way to refactor an existing code path? Bursting with ideas to make OpenSpending more awesome?

We *can't wait* to see your contributions. Here are a few things that will help:

- All open issues for the Viewer [can be found here](http://github.com/openspending/openspending/issues), labeled "Viewer". If you are working on an existing issue, please let us know by commenting on an issue. Likewise, if you are working on something new, open an issue to let us know.
- We follow a set of [coding standards](https://github.com/okfn/coding-standards), and we have simple examples of those coding standards implemented for [Python](https://github.com/okfn/oki-py) and [Javascript](https://github.com/okfn/oki-js). Please do read before starting.

If anything is unclear, or you just want to talk with other people working on OpenSpending, then catch us on [Gitter.im](http://gitter.im/openspending/chat).
