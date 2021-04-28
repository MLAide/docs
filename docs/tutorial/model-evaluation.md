# Model Evaluation

## Compare runs
A key feature of ML Aide is to compare several runs with their parameters and metrics.
Therefore open the [Web UI](http://localhost:8880/projects/usa-housing/runs) and
select all runs that should be compared. In this case, we want to compare 
`linear regression` and `lasso model`. Select the two checkboxes and click on
the `Compare` button at the top of the table.

You will see all parameters and metrics of the two runs. All values that
are not equal will be highlighted.

## Visualize Lineage
Sometimes you want to know how a model was build or which runs (steps) were executed
in a particular experiment. For this, you can use the lineage visualization of experiments.

Go to the [Experiment View](http://localhost:8880/projects/usa-housing-2/experiments) and select
an experiment. You will see all runs (blue color) and all input/output artifacts (red color).

The table below shows you all runs and artifacts. From the runs table, you can jump the run details
or to the run comparison.