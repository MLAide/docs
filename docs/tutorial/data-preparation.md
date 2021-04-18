# Data Preparation

In this chapter we will load and prepare the 
[USA Housing dataset](https://www.kaggle.com/vedavyasv/usa-housing). All steps that we execute
should be stored in ML Aide.

First download the [dataset](https://raw.githubusercontent.com/MLAide/docs/master/docs/tutorial/housing.csv)
and save it in a sub directory called `data`.
```
curl https://raw.githubusercontent.com/MLAide/docs/master/docs/tutorial/housing.csv --output ./data/housing.csv
```

Before we read or process anything we should start tracking all relevant information in ML Aide. In ML Aide a run
is the key concept to track parameters, metrics, artifacts and models. All runs belong to one or more experiments.

```python
run_data_preparation = mlaide_client.start_new_run(experiment_key='linear-regression', run_name='data preparation')
```

Now we can read and process the dataset. Also we are able to register the dataset as an artifact in ML Aide.
This brings the advantage that we are able to reproduce the following steps - even if the dataset is lost, deleted or modified.
The artifact can be used in other runs as an input. This helps to track down the lineage of a machine learning model to its
source. At the end don't forget to mark the run as completed.

```python
housing_data = pd.read_csv('data/housing.csv')

# add dataset as artifact
artifact = run_data_preparation.create_artifact(name="USA housing dataset", artifact_type="dataset", metadata={})
run_data_preparation.add_artifact_file(artifact, 'data/housing.csv')
run_data_preparation.set_completed_status()
```

Check the [Web UI](http://localhost:8880/projects/usa-housing/runs) to see the created run and the artifact.

In this chapter we created our first run in ML Aide. We attached the dataset as an artifact to the run. The
next step is to create a model based on this dataset.
