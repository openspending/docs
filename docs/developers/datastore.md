# OpenSpending Datastore

The OpenSpending Datastore is a flat file datastore with source data stored in [Fiscal Data Packages](http://fiscal.dataprotocols.org/spec/).

There is not a great deal to document. The following notes are important to know:

- The Datastore runs from S3, or, an object storage which supports the S3 API.
- The Datastore is the point of truth for data, holding the raw data sources, and the [Fiscal Data Package](http://fiscal.dataprotocols.org/spec/) that describes the sources.
- All data coming into OpenSpending first hits the Datastore. From the Datastore, various services read this data and create derived databases to represent the data in certain ways. For example, the data is read into an SQL backend to provide the analytics API, and a search backend for the search API.
