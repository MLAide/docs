# Data Preparation

In this chapter, we will load and prepare the 
[USA Housing dataset](https://www.kaggle.com/vedavyasv/usa-housing). All steps that we execute
will be stored in ML Aide.

## Import required Dataset

First download the [dataset](https://raw.githubusercontent.com/MLAide/docs/master/docs/tutorial/housing.csv)
and save it in a subdirectory called `data`.
```
curl https://raw.githubusercontent.com/MLAide/docs/master/docs/tutorial/housing.csv --output ./data/housing.csv
```

## Create Experiment
Before we read or process anything we should start tracking all relevant information in ML Aide. In ML Aide a [run](../essentials/runs.md)
is the key concept to track parameters, metrics, artifacts and models. All runs belong to one or more [experiments](../essentials/experiments.md).

Experiments can be created from the [Experiments View](http://localhost:8880/projects/usa-housing/experiments).
Click on `Add Experiment` and enter `Linear Regression` as the experiment name. Leave the tags empty and remain the status unchanged. Confirm the dialog by clicking `Create`. Now you can see the experiment in the UI.

## Create Run
Next, we switch back to our Python code and create a run for the data preparation.

```python
run_data_preparation = mlaide_client.start_new_run(experiment_key='linear-regression', run_name='data preparation')
```

Now we can read and process this file. Also, we are able to register the dataset as an [artifact](../essentials/artifacts.md) in ML Aide.
This gives us the ability to reproduce the following steps - even if the dataset is lost, deleted, or modified.
The artifact can be used in other runs as an input. This helps to track down the lineage of a machine learning model to its
root. In the end, don't forget to mark the run as completed.

```python
housing_data = pd.read_csv('data/housing.csv')

# add dataset as artifact
artifact = run_data_preparation.create_artifact(name="USA housing dataset", artifact_type="dataset", metadata={})
run_data_preparation.add_artifact_file(artifact, 'data/housing.csv')
run_data_preparation.set_completed_status()
```

Check the [Web UI](http://localhost:8880/projects/usa-housing/runs) to see the created run and the artifact.

## Summary
In this chapter we 

- created our first run in ML Aide
- attached the dataset as an artifact to the run

The next step is to create a model based on this dataset.
