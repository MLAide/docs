# Data Preparation

In this chapter, we will load and prepare the 
[USA Housing dataset](https://www.kaggle.com/vedavyasv/usa-housing). All steps that we execute
will be stored in ML Aide.

## Download required Dataset

First, download the [dataset](https://raw.githubusercontent.com/MLAide/docs/master/docs/tutorial/housing.csv)
and save it in a subdirectory called `data`.
```
mkdir data
curl https://raw.githubusercontent.com/MLAide/docs/master/docs/tutorial/housing.csv --output ./data/housing.csv
```

## Create an API key
Later, we want to send all parameters, metrics, and models of our experiments to ML Aide.
Therefore, we need to set an API key in our python client. Otherwise, we won't be able
to authenticate against the ML Aide server.

- In the upper right click on `adam` > `Settings`
- Go to `API Keys` in the left navigation
- Click on `Add API Key`
- Enter any description and click on `Create`
- Copy the show API key and store it somewhere safe. The API key won't be shown again. If you lose your API key you have to create a new one.

## Create connection to ML Aide webserver
Our data preparation will be implemented in `data_preparation.py`. Therefore, create a new file with this name.
To create a connection to the ML Aide webserver with Python clients you have to use `mlaide.MLAideClient`. An object
of this class is the main entry point for all kinds of operations. Replace `api_key` with your personal API key that 
you created using the ML Aide web UI.

```python
from mlaide import MLAideClient, ConnectionOptions
import pandas as pd
```
--8<-- "snippets/tutorial/connection.py.md"

## Create Run
Before we read or process anything we should start tracking all relevant information in ML Aide. 
In ML Aide a [run](../essentials/runs.md) is the key concept to track parameters, metrics, artifacts 
and models. All runs belong to one or more [experiments](../essentials/experiments.md).

```python
run_data_preparation = mlaide_client.start_new_run(experiment_key='linear-regression', run_name='data preparation')
```

Now we can read and process this dataset. Also, we can register the dataset as an [artifact](../essentials/artifacts.md) 
in ML Aide. This gives us the ability to reproduce the following steps - even if the dataset is lost, deleted, or modified.
The artifact can be used in other runs as an input. This helps to track down the lineage of a machine learning model to its
root. In the end, don't forget to mark the run as completed.

```python
housing_data = pd.read_csv('data/housing.csv')

# add dataset as artifact
artifact = run_data_preparation.create_artifact(name="USA housing dataset", artifact_type="dataset", metadata={})
run_data_preparation.add_artifact_file(artifact, 'data/housing.csv')

run_data_preparation.set_completed_status()
```

Start your python script using your shell with `python data_preparation.py`. After the script completed check the 
[web UI](http://localhost:8880/projects/usa-housing/runs) to see the created run and the artifact.

## Summary
In this chapter we 

- created an API key for authorization 
- created our first run in ML Aide
- attached the dataset as an artifact to the run
- connected the python client to the ML Aide webserver

Your code should look like the following snippet shows.
??? note "Code"
    === "data_preparation.py"
        --8<-- "snippets/tutorial/data_preparation.py.md"
    === "data/housing.csv"
        --8<-- "snippets/tutorial/data_housing.csv.md"

The next step is to create a model based on this dataset.
