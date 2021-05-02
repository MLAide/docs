# Setup
Before we start the actual work, we need to set up our project.

## Run ML Aide
For this tutorial, ML Aide server and web-UI are required. The [quickstart](../start/quickstart.md) helps to get ML Aide running.

## Create a workspace directory
In this tutorial, we will use `~/mlaide-tutorial/` as our working directory.

## Install dependencies via pip
Open a terminal in the working directory and install all dependencies.
```
cd ~/mlaide-tutorial
pip install scikit-learn pandas mlaide
```

## Create ML Aide project
- Open the [ML Aide web UI on localhost:8880](http://localhost:8880)
- Login as adam (username = `adam`; password = `adam1`)
- Click on `Add Project` to create a new project - enter `USA Housing` as project name

## Create an API key
Later, we want to send all parameters, metrics, and models of our experiments to ML Aide.
Therefore, we need to set an API key in our python client. Otherwise, we won't be able
to authenticate against the ML Aide server.

- In the upper right click on `adam` > `Settings`
- Go to `API Keys` in the left navigation
- Click on `Add API Key`
- Enter any description and click on `Create`
- Copy the show API key and store it somewhere safe. The API key won't be shown again. If you lose your API key you have to create a new one.


## Create Connection
To create a connection to the ML Aide webserver with Python
clients you have to use `mlaide.MLAideClient`. An object
of this class is the main entry point for all kinds of operations.

```python
from mlaide import MLAideClient, ConnectionOptions
```
--8<-- "snippets/tutorial/connection.py.md"

Replace `api_key` with your personal API key that you created using the ML Aide Web UI.

## Summary
In this chapter we have

- set up our working environment
- created our tutorial project
- created an API key for authorization 
- created a snippet to connect our python client to the ML Aide webserver.

Next, we will load and prepare the dataset. Here, we will use the snippet.

Now you should have everything up and running to start coding.