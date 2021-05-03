# Model Evaluation

## Compare Runs
A key feature of ML Aide is to compare several runs with their parameters and metrics.
Therefore open the [web UI](http://localhost:8880/projects/usa-housing/runs) and
select all runs that should be compared. In this case, we want to compare 
`linear regression` and `lasso model`. Select the two checkboxes and click on
the `Compare` button at the top of the table.

You will see all parameters and metrics of the two runs. All values that
are not equal will be highlighted.

## Visualize Lineage
Sometimes you want to know how a model was built or which runs (steps) were executed
in a particular experiment. For this, you can use the lineage visualization of experiments.

Go to the [experiment view](http://localhost:8880/projects/usa-housing-2/experiments) and select
an experiment. You will see all runs (blue color) and all input/output artifacts (red color).

The table below shows you all runs and artifacts. From the runs table, you can jump the run details
or to the run comparison.

## Model Staging
In this very basic example we can see that both models are quite similar. We can choose any of these
models and tag it as 'production ready'. This helps to keep track of models that are used in production,
are still under devlopment (or QA) or are already deprecated.

ML Aide provides the following stages for models:

- None
- Staging
- Production
- Deprecated
- Abandoned

## Summary
In this chapter we 

- compared the two model training runs
- visualized the model lineage
- staged the models

ML Aide provides us with tools to keep track of all machine learning experiments, the models, and their lineage.

In the next chapter, we will learn how we can load models from ML Aide to predict values.