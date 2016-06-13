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

***Time***

**Date** - please select "Fiscal year" or "Other date" (select "Other date" when it is a date of a purchase/sale, mostly in case of contracts/invoices). You can specify the exact format in which the data is provided. e.g. “%m/%d/%Y” for US style dates.

***Classifications***

**Administrative classification** - the entity responsible for managing the public funds, such as the Ministry of Health, Education, Social Protection (or at a lower level, schools and hospitals).
*Examples:* 
* *National Social Insurance Company*
* *Agency for Payments and Intervention in Agriculture*
* *State Tax Inspectorate*
* *Social support and care actions and facilities*
* *Local City Council*

**Economic classification** - it identifies the type of budget and expenditure incurred, for example, salaries, goods and services, transfers and interest payments, or capital spending. Select between “Non-standard” and “GFSM” economic classification, depending on your data.
*Examples:*
* *Remuneration of work*
* *Power (electricity)*
* *Manual, teaching materials*
* *Payment of interest*
* *Payment for goods and services*

**Functional classification** - expenditure according to the purposes and objectives for which they are intended. Select between “Non-standard” and “COFOG” functional classification, depending on your data.
*Examples:*
* *Secondary education*
* *Roads service*
* *Healthcare*
* *State debt servicing*
* *Social benefits and pensions*

**Description** - use this DataType to map longer (1-2 sentence) descriptions (we will implement this for info boxes when hovering over the visualization).

**Activity**
**Activity** - use this when you have a data column on the contract/program/project being funded.

**Participating entities**

**Administrator** - authority that spends the money. The administrator could be last level in the hierarchy, but not necessarily.

**Procurer** - the government entity acting as procurer for the transaction, if different from the institution controlling the project.

**Recipient** - the recipient (if any) targeted by the revenue item.

**Supplier** - the recipient of the expenditure.

**Fiscal Attributes**
**Budgetary Transfers** - extra properties regarding whether the expenditure contains budgetary transfers.

**Budget Direction** - specifies whether the values in this line are expenditures or revenues.

**Expenditure Type** - extra attributes providing more properties regarding the expenditure.

**Financial Source** - the financial source for the budgetary funds.

**Budget Life-cycle Phase** - the phase identifier for the values in this line (e.g. approved, executed etc.)

**Geographic**
**Geographic information** - use "Code List" for the geo codelist from which the geocode is drawn, and "Display name" for the name or title of the geographical region targeted by the budget item.

**Identifiers**
**Budget line identifier** - this is simply the unique identifier for this budget line.

**Invoice identifier** - the invoice number given by the vendor or supplier.

**Amount**
**Amount (value)** - mandatory to map a value. Use "Factor" if your data says 1.3mln instead of 1,300,000 (in this case factor will be "1,000,000”)
*Example:*
1.3bn will have a factor of 1bn (indicate 1,000,000,000 for a factor).

**Other**
**Unknown Mapping** - Use when no other DataType applies to the column.
