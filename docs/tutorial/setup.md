# Setup
Before we start the actual work, we need to set up our project.

## Run ML Aide
For this tutorial, ML Aide server and web-UI are required. The [quickstart](../start/quickstart.md) helps to get ML Aide running.

## Create a workspace directory
In this tutorial, we will use `~/mlaide-tutorial/` as our working directory.

## Prepare environment
For this tutorial, we recommend a Python environment manager like [virtualenv](https://virtualenv.pypa.io/en/latest/) 
in combination with [pyenv](https://github.com/pyenv/pyenv). Of course, you don't have to use virtualenv or you can use
any other environment manager. But in all cases, you should install the dependencies from step 6.

1. Open a terminal and navigate to the project directory
```
cd ~/mlaide-tutorial
```

2. Install Python 3.9 (if not already present) via pyenv
```
pyenv install
```

3. Install virtualenv (if not already present)
```
pip install virtualenv
```

4. Create virtual environment
```
virtualenv .venv
```

5. Activate virtual environment
```
source .venv/bin/activate
```

6. Install all dependencies
```
pip install scikit-learn pandas numpy mlaide
```

## Create ML Aide project
- Open the [ML Aide web UI on localhost:8880](http://localhost:8880)
- Login as adam (username = `adam`; password = `adam1`)
- Click on `Add Project` to create a new project - enter `USA Housing` as project name

## Summary
In this chapter we have

- set up our working environment
- created our tutorial project

Next, we will load and prepare the dataset. Here, we will use the snippet.

Now you should have everything up and running to start coding.