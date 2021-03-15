# Create Connection to App

In the first step, we have to create a new python file in our working directory. For this, create the file `app.py`.

## Import required Libraries

Then, we need to import all libraries - including ML Aide.

```python
from mlaide import client
from mlaide.model import ArtifactRef
import pandas as pd
from sklearn import metrics
from sklearn.model_selection import cross_val_score, train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
```

## Setup Server URL and API Keys

Now we are ready to create a connection using the API key.

```python
options = client.MvcOptions(
    mvc_server_url='http://localhost:8881/api/v1', # the ML Aide demo server runs on port 8881 per default
    api_key='<your api key>'
)
mlaide_client = client.MvcClient(project_key='usa-housing', options=options)
```

## Summary

In this chapter we have

- imported all required libraries
- setup the connection to our web application

The next step is to load and prepare the dataset.