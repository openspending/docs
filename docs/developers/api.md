# OpenSpending API

The OpenSpending API is a Python app that provides a range of API endpoints to query an OpenSpending database.

The API is available for general use, and also powers all of the core components of OpenSpending, such as the [Viewer](./viewer/), the [Packager](./packager/), and the [Explorer](./explorer/).

## Features

- An analytical API powered by [Babbage](https://github.com/openspending/babbage)
- A search API to access package-level meta data
- A search API to access fiscal line-level data.
- A set of backwards-compatible OpenSpending V2 endpoints

## Requirements

You need to have Python 2.7.x or Python 3 to run the API. The API itself is a set of Flask blueprints. We recommend using Python 3.

## Installation

The API can be installed as a component of the Platform, or as a stand alone component.

**Which installation method should you choose?**

- If your goal is to get a full instance of OpenSpending running, then go ahead with the platform installation.
- If you just want to hack on the API (Suggest new features! Fix bugs!), or even run your own API against a remote OpenSpending platform, then follow the standalone install.

If the options are confusing, then go ahead with the platform installation. This will allow you to easily upload new data into the platform, modify the API code and see how that affects the visualisation engines.

### Platform install

Follow the instructions for installing a development environment for the [OpenSpending platform here](./platform/).

### Standalone install

Follow these steps to get the API running:

```
 $ git clone https://github.com/openspending/os-api.git
 $ cd os-api
 $ export OS_API_ENGINE=sqlite:///`pwd`/osapi.db
 $ celery -A babbage_fiscal.tasks worker &
 $ python dev_server.py
```

Based on the default configuration of the API, you can now work with your local OpenSpending database hosted on your local machine. If you want to point to a different OpenSpending instance, configure your environment variables accordingly based on the details below.

## Interface

### Call reference

- `/api/3/info/<dataset>/package`
  - Returns the Fiscal Data-Pacakge for this dataset
- `/api/3/cubes`:
  - Returns a list of the available datasets in the store
- `/api/3/cubes/<dataset>/model`:
  - Returns the `babbage` model for the dataset. This is the model which is used  when querying the data.
- `/api/3/cubes/<dataset>/facts`:
  - Returns individual entries from the dataset in non-aggregated form.
  - Parameters:
    - `cut` - filters on the data (`field_name:value`, `field_name:value|field_name:value` etc.)
    - `fields` - fields to return
    - `order` - data ordering (e.g. `field_name:desc`)
    - `pagesize` - number of entries in one batch of returned data
    - `page` - page selection
- `/api/3/cubes/<dataset>/members/<dimension>`
  - Returns the distinct set of values for a specific dimension.
  - Parameters: `cut`, `order`, `page` and `pagesize` as above
- `/api/3/cubes/<dataset>/aggregate`
  - Returns an aggregate of the data in the specified dataset.
  - Parameters:
    - `cut`, `order`, `page` and `pagesize` as above
    - `drilldown` - group by these dimensions (e.g. `field_name_1|field_name_2`)
    - `aggregates` - which measures to aggregate (and what function to perform (e.g. `amount.sum`, `count`)
- `/api/2/aggregate`
  - A backwards compatible version of the aggregate API.
  - Parameters:
    - `dataset` - dataset to query
    - `measure` - measure to aggregate
    - `cut` - filters on the data
    - `drilldown` - fields to group by the results
    - `page` and `page_size` - as above
    - `order` - same as `sort`, above

### Contributing code

Found a bug? Got neat way to refactor an existing code path? Bursting with ideas to make OpenSpending more awesome?

We *can't wait* to see your contributions. Here are a few things that will help:

- All open issues for the API [can be found here](http://github.com/openspending/openspending/issues), labeled "API". If you are working on an existing issue, please let us know by commenting on an issue. Likewise, if you are working on something new, open an issue to let us know.
- We follow a set of [coding standards](https://github.com/okfn/coding-standards), and we have simple examples of those coding standards implemented for [Python](https://github.com/okfn/oki-py) and [Javascript](https://github.com/okfn/oki-js). Please do read before starting.

If anything is unclear, or you just want to talk with other people working on OpenSpending, then catch us on [Gitter.im](http://gitter.im/openspending/chat).
