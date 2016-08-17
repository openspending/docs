# Prepare data for OpenSpending

OpenSpending loads and stores data in common tabular data formats such as CSV and Excel. While the system can work with a range of data structures in these files, due to the flexible modeling scheme of [Fiscal Data Package](http://fiscal.dataprotocols.org/spec/), a minimum set of quality requirements must be met.

## Minimum quality requirements

Essentially, the minimum quality requirements are as follows:

- The file must have headers on the first row.
- There must not be any blank rows.
- There must not be any mismatch between the length of a row, and the length of the headers.
- Each column must have a consistent "data type" (date columns should contain dates, amount columns should contain numbers).

## Ensuring quality

Files added to OpenSpending need to meet a certain quality level in the structure of the file, and the schema.

If you use the [OpenSpending Packager](https://github.com/openspending/os-packager) to upload files via a UI, or, the [OpenSpending CLI](https://github.com/openspending/os-cli) to upload files via the command line, the data sources will be checked using the [GoodTables data validator](https://github.com/frictionlessdata/goodtables).

Using these tools, you'll not only be told that the data sources are valid (or not), you'll also get hints on how to address issues in the case of invalid files.

If you have a custom data processing pipeline, or in general, would like to validate your files without using the Packager and CLI, that is entirely possible by using GoodTables directly in your own setup.

## Why is this important?

OpenSpending uses a flat file datastore to store the raw data provided by users, with additional information on how to understand that raw data via the Fiscal Data Package descriptor. From the datastore, other databases are derived, to provide the OpenSpending APIs and other related data services. The data quality checks ensure that the ecosystem that reads data out of the datastore can expect the data to be of a reliable quality.

## Walkthroughs

### Checking data quality with the Packager

1. Access OS Packager: http://next.openspending.org/packager/provide-data.
![Image 1](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/DQ%201..jpg)

2. Authenticate to OpenSpending by clicking “Login/Register” in the upper-right corner.
![Image 2](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/login..jpg)

3. Select a file/data source from your computer or insert a URL.
![Image 3](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/DQ%203..jpg)

4. If your data source passed the “validation step,” you will get a message saying “Resource is valid. Now you can continue.”
![Image 4](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/DQ%205..jpg)

5. If the data source contain errors, you will get the following message: “There are some errors. Click here to view details.”
![Image 5](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/DQ%202..jpg)

6. Click to see the “Data Validation Results.”
![Image 6](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/DQ%204..jpg)

7. Correct errors in your data source and try again.

### Checking data quality with the CLI

1. Download the goodtables library, which is a Python package, and can be used as a command line tool. It runs on Python 2 or 3:`pip install goodtables`

2. Ensure goodtables is installed correctly by typing `goodtables` in your shell. You should see something like the following:
![Image 6](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/Picture1.png)

3. We want to check the structure of our CSV file. This is done with the following command: `goodtables structure {PATH_TO_FILE}`. See two screenshots below, one with a check that returned structural errors, and one with a check that found the file valid.
![Image 7](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/Picture2.png)
![Image 8](https://raw.githubusercontent.com/VictoriaVlad/docs/master/images/Picture3.png)
