# Prepare data for OpenSpending

OpenSpending loads and stores data in common tabular data formats such as CSV and Excel. While the system can work with a range of data structures in these files, due to the flexible modeling scheme of [Fiscal Data Package](http://fiscal.dataprotocols.org/spec/), a minimum set of quality requirements must be met.

## Minimum quality requirements

Essentially, the minimum quality requirements are as follows:

- The file must have headers on the first row.
- There must not be any blank rows.
- There must not be any mismatch between the length of a row, and the length of the headers.
- Each column must have a consistent "data type" (date columns should contain dates, amount columns should contain numbers without currency signs or names).

## Ensuring quality

Files added to OpenSpending need to meet a certain quality level in the structure of the file, and the schema.

If you use the [OpenSpending Packager](https://github.com/openspending/os-packager) to upload files via a UI, or, the [OpenSpending CLI](https://github.com/openspending/os-cli) to upload files via the command line, the data sources will be checked using the [GoodTables data validator](https://github.com/frictionlessdata/goodtables).

Using these tools, you'll not only be told that the data sources are valid (or not), you'll also get hints on how to address issues in the case of invalid files.

If you have a custom data processing pipeline, or in general, would like to validate your files without using the Packager and CLI, that is entirely possible by using GoodTables directly in your own setup.

## Why is this important?

OpenSpending uses a flat file datastore to store the raw data provided by users, with additional information on how to understand that raw data via the Fiscal Data Package descriptor. From the datastore, other databases are derived, to provide the OpenSpending APIs and other related data services. The data quality checks ensure that the ecosystem that reads data out of the datastore can expect the data to be of a reliable quality.

## Walkthroughs

### Checking data quality with the Packager

{
Use packager to add a data source, and show the UI for the GoodTables error report.
}

### Checking data quality with the CLI

{
Use CLI on a data source to get a goodtables result, showing data errors.
}
