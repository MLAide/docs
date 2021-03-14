# Introduction

In this tutorial we will use the [USA Housing dataset](https://www.kaggle.com/vedavyasv/usa-housing) 
to predict prices of houses in Boston. To keep things simple for this tutorial we won't use 
Jupyter Notebooks. Instead we write just simple Python code.

We will use the dataset to train some machine learning models. All processed data and all experiments
should be tracked in ML Aide. We also want to store the trained models in ML Aide for later usage.

To get started we need some initial work to be done

## Run ML Aide
For this tutorial ML Aide server und web UI is needed. The [quickstart](../start/quickstart.md) helps to get ML Aide running.

## Create a workspace directory
In this tutorial we will use `~/mlaide-tutorial/` as our working directory.

## Install dependencies via pip
Open a terminal the working directory and install all dependecies.
```
cd ~/mlaide-tutorial
pip install scikit-learn pandas mlaide
```

## Create ML Aide project
- Open the [ML Aide Web UI on localhost:8880](http://localhost:8880)
- Login as adam (username = `adam`; password = `adam1`)
- Click on `Add Project` to create a new project - enter `USA Housing` as project name

## Create an API key
Later we want to send all parameters, metrics and models of our experiments to ML Aide. 
Therefore we need to set a API key in our python client. Otherwise we won't be able
to authenticate against the ML Aide server.

- In the upper right click on `adam` > `Settings`
- Go to `API Keys` in the left navigation
- Click on `Add API Key`
- Enter any description and click on `Create`
- Copy the show API key and store it somewhere safe. The API key won't be shown again. If you loose your API key you have to create a new one.

Now you should have everything up and running to start coding.