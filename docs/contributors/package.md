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

**Activity** - use this when you have a data column on the contract/program/project being funded. "Code" is a unique identifier for the activity and will be used for querying. "Label" means "display name". 

**Date** - please select "fiscal-year" or "generic" (select "generic" when it is a date of a purchase/sale, mostly in case of contracts/invoices). The format should be modifiable according to the provided data (year, month, date), with “%Y”, “%m”, and “%d”.

**Administrative-classification** - the entity responsible for managing the public funds, such as the Ministry of Health, Education, Social Protection (or at a lower level, schools and hospitals). Examples: 
* *National Social Insurance Company*
* *Agency for Payments and Intervention in Agriculture*
* *State Tax Inspectorate*
* *Social support and care actions and facilities*

**Functional-classification** - expenditure according to the purposes and objectives for which they are intended. Examples:
* *Secondary education*
* *Roads service*
* *Healthcare*
* *State debt servicing*
* *Social benefits and pensions* 

**Economic-classification** - it identifies the type of budget and expenditure incurred, for example, salaries, goods and services, transfers and interest payments, or capital spending. Examples:

* *Remuneration of work*
* *Power (electricity)*
* *Manual, teaching materials*
* *Payment of interest*
* *Payment for goods and services*

**Generic** - if data it is not following a standard/classification, please select this.

**Description** - use this DataType to map longer descriptions (we will implement this for info boxes when hovering over the visualization).

**Administrator** - authority that spends the money. The administrator could be final level in the classification, but not necessarily.

**Procurer** - the government entity acting as procurer for the transaction, if different from the institution controlling the project.

**Supplier** - the recipient of the expenditure.

**Recipient** - the recipient (if any) targeted by the revenue item.

**Direction** - use this when you have a data column specifying revenues vs expenses.

**Phase** - use this to specify the budget phase of a specific amount. (ex. planned/approved/executed/adjusted). Let us know if another phase would apply better for your case. 

**Geo-source** - use "code" for id of location, "codeList" for the geo codelist from which the geocode is drawn, and "title" for the name or title of the geographical region targeted by the budget item.

**Budget-line-id** - this is simply the unique identifier for this budget line.

**Invoice-id** - the invoice number given by the vendor or supplier.

**Value** - mandatory to map a value. Use "Factor" if your data says 1.3mln instead of 1,300,000 (in this case factor will be "1,000,000”)
*Example*:
1.3bn will have a factor of 1bn (indicate 1,000,000,000 for a factor).
