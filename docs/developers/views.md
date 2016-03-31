# OpenSpending Views

The OpenSpending Views library is a set of JavaScript components for the visualisation of fiscal data.



Application State
We have a few different types of charts in OS viewer. Some are based on similar concepts and interaction, and some are different.
The viewer will keep a separate state for each of these chart classes. Selecting a specific chart will load the state for that chart class - so 
when switching from one chart type to another in the same class, the data selection will remain the same.
when selecting a chart from another class, we’ll load the state for that class.
when returning to a chart from a previously visited class, we will return to the last state for that specific class

On init, the ‘Table’ chart is selected with no grouping.
Chart Types
The current classes are:
Drilldown: Treemap, Pie-Chart, Bubble-Tree
Sortable-Series: Bar Chart, Table
Time-Series: Line/Area Chart
2D-Table: Pivot-Table
Drilldown
A drilldown chart is one that basically allows to traverse along a hierarchy. 

UI Appearance and Behaviour 
Under ‘Measures’ a list of all measures is shown, from which the user chooses one measure to use.
If there’s only one measure, this section should not appear and the only measure is auto-selected
Under ‘Hierarchies’ a list of all hierarchies is shown, from which the user chooses one hierarchy to follow.
Under ‘Filters’ a list of all dimensions. When clicking on a dimension, it expands while disclosing all possible values for that dimension.
Filters should be grouped by containing hierarchy
The selected value is always the key attribute.
If the dimension has a label attribute, then show the label for each value instead.
Clicking on a specific value creates a ‘cut’ parameter in the API call
You can only select one value for each dimension.
Once a hierarchy is selected, its dimensions are removed from the list of filters.
Sorting controls are not enabled.

API Handling
At first there are no internal filters and and ‘drilldown’ API parameter is set to the highest dimension in the selected hierarchy.
Clicking on the chart performs a ‘drilldown’ action:
Add a cut for the active dimension in the hierarchy 
change the active dimension to the next dimension in the selected hierarchy.
Backing up from the drilldown means:
Removing the last cut added
change the active dimension to the previous dimension in the selected hierarchy.
User provided filters and the ‘drilldown cuts’ are combined together in the ‘cut’ API parameter.
Data should always be sorted by the measure value, descending.
Sortable-Series
UI Appearance and Behaviour 
Under ‘Measures’ a list of all measures is shown, from which the user chooses one measure to use.
If there’s only one measure, this section should not appear and the only measure is auto-selected
Under ‘X-axis’ a list of all dimensions is shown, grouped by hierarchy
Only one dimension can be selected for the x-axis
The first dimension (top of the list in the UI) should be selected initially
Under ‘Series’ a list of all dimensions is shown, grouped by hierarchy
Only one series can be selected - but it’s also possible not to have a series selected at all
Selecting a series makes the graph to appear as a multi-series graph. In this case a legend of sorts should be shown in the chart.
Under ‘Filters’ a list of all dimensions is shown. Same as in ‘Drilldown’
Data can be ordered according the measure or by the x-axis dimension, ascending or descending
Initially the ordering should be measure, descending
Clicking an active sort control toggles the direction (asc/desc)
Clicking an inactive sort control makes it active and disables all other sort controls.


API Handling
‘drilldown’ API parameter is derived from the x-axis selection and also the series selection in case it is made.
The ‘cut’ API parameter is derived from the filter selection in a straightforward manner.
The ordering of the data is derived from the sort controls state
Time-Series
UI Appearance and Behaviour 
This class is only enabled if there’s a ‘time’ typed dimension
Under ‘Measures’ a list of all measures is shown, from which the user chooses one measure to use.
If there’s only one measure, this section should not appear and the only measure is auto-selected
Under ‘Series’ a list of all dimensions is shown, grouped by hierarchy
vOnly one series can be selected - but it’s also possible not to have a series selected at all
Selecting a series makes the graph to appear as a multi-series graph. In this case a legend of sorts should be shown in the chart.
Under ‘Filters’ a list of all dimensions is shown. Same as in ‘Drilldown’
Sorting controls are not enabled.

API Handling
‘drilldown’ API parameter should always contain the time dimension.
In case a series dimension was selected, it should be appended to the ‘drilldown’ API parameter
The ‘cut’ API parameter is derived from the filter selection in a straightforward manner.
Data is always sorted by the time dimension.
2D-Table
UI Appearance and Behaviour 
API Handling

### Contributing code

Found a bug? Got neat way to refactor an existing code path? Bursting with ideas to make OpenSpending more awesome?

We *can't wait* to see your contributions. Here are a few things that will help:

- All open issues for the Viewer [can be found here](http://github.com/openspending/openspending/issues), labeled "Viewer". If you are working on an existing issue, please let us know by commenting on an issue. Likewise, if you are working on something new, open an issue to let us know.
- We follow a set of [coding standards](https://github.com/okfn/coding-standards), and we have simple examples of those coding standards implemented for [Python](https://github.com/okfn/oki-py) and [Javascript](https://github.com/okfn/oki-js). Please do read before starting.

If anything is unclear, or you just want to talk with other people working on OpenSpending, then catch us on [Gitter.im](http://gitter.im/openspending/chat).



