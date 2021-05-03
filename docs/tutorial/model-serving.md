# Model Serving

In the previous chapters we trained two models based on the 
[USA Housing dataset](https://www.kaggle.com/vedavyasv/usa-housing).

Now we will reload the linear regression model to do some predictions.

## Create connection to ML Aide webserver
Our code will be written in a new file named `serving.py`. In the beginning,
we will create a connection to the ML Aide webserver.
```python
from mlaide import MLAideClient, ConnectionOptions
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LinearRegression
import numpy as np
```
--8<-- "snippets/tutorial/connection.py.md"

## Load Model and Pipeline
To do some predictions we want to use the linear regression model. But before we predict
values with the model, we have to use the sklearn pipeline to transform our input vectors.
The pipeline was also stored in ML Aide. Thus, we can load both from ML Aide.

```python
# read the model
lin_reg: LinearRegression = mlaide_client.load_model('linear regression')

# read the pipeline containing the standard scaler
pipeline: Pipeline = mlaide_client.load_model('pipeline')
```

## Predict Values
Now we are ready to use our model. In this case, we will hardcode a house area for our prediction.
In real-world scenarios, we would get the input from HTTP requests or something similar.

```python
# create some data for prediction
data = np.array([[80000, 6.32, 7.4, 4.24, 25000]])
# The values are
# - Avg. Area Income
# - Avg. Area House Age
# - Avg. Area Number of Rooms
# - Avg. Area Number of Bedrooms
# - Area Population


# predict the house price
data = pipeline.transform(data)
pred = lin_reg.predict(data)
print(pred) # output is: [1415072.9471789]
```

## Summary

In this chapter we

- loaded the linear regression model
- loaded the sklearn pipeline
- predicted a value using the model

Your code should look like the following snippet shows.
??? note "Code"
    === "serving.py"
        --8<-- "snippets/tutorial/serving.py.md"
    === "training.py"
        --8<-- "snippets/tutorial/training.py.md"
    === "data_preparation.py"
        --8<-- "snippets/tutorial/data_preparation.py.md"
    === "data/housing.csv"
        --8<-- "snippets/tutorial/data_housing.csv.md"
