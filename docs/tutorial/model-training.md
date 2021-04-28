# Model Training

In the last chapter we loaded the USA Housing dataset. Now we will train two different
models on this dataset. All details of the training will be tracked in ML Aide.

Our code will be written in a new file named `training.py`. In the beginning
we will create a connection to the ML Aide webserver.
```python
from mlaide import MLAideClient, ConnectionOptions, ArtifactRef
import pandas as pd
import numpy as np
from sklearn.model_selection import cross_val_score, train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression, Lasso
from sklearn import metrics
```
--8<-- "snippets/tutorial/connection.py.md"

## Train Test Split
As you can see we are implementing these steps in a different file as the data preprocessing.
Therefore we somehow need to get our input data. We could read the CSV again. Or we could
retrieve the CSV file from ML Aide. In this case we will read the content of the file from 
ML Aide. In the previous step we saved the file as an artifact with the name `USA housing dataset`.
Ommiting the version means that we want to retrieve the latest version of the artifact.
```python
dataset_bytes = mlaide_client.get_artifact('USA housing dataset', version=None).load('data/housing.csv')
housing_data = pd.read_csv(dataset_bytes)
```

Usually a split will be done randomly. ML Aide helps you to keep things reproducible.

We start a new run to track the split. Also, we set the dataset as an input artifact.

```python
artifact_ref = ArtifactRef(name="USA housing dataset", version=1)
run_pipeline_setup = mlaide_client.start_new_run(experiment_key='linear-regression', 
                                                 run_name='pipeline setup', 
                                                 used_artifacts=[artifact_ref])
```

Now we split our dataset and link all information related to the split to our run.
In this case we want to track all arguments (`test_size` and `random_state`) of the 
`train_test_split()` function.

```python
X = housing_data[['Avg. Area Income', 'Avg. Area House Age', 'Avg. Area Number of Rooms',
               'Avg. Area Number of Bedrooms', 'Area Population']]
y = housing_data['Price']

test_size=0.3
random_state=42

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=test_size, random_state=random_state)

run_pipeline_setup.log_parameter('test_size', test_size)
run_pipeline_setup.log_parameter('random_state', random_state)
```

If you have a close look at the data, you can see that all X values must be scaled, before we can use them.
We use the `StandardScaler` of sklearn. The scaler that will be fitted here, must also be used later for 
predicting new values. ML Aide makes this easy by just storing the scaler (or the whole pipeline) in
ML Aide as an artifact. The artifact can be loaded later in a separate process for predicting.

```python
pipeline = Pipeline([
    ('std_scalar', StandardScaler())
])

X_train = pipeline.fit_transform(X_train)
X_test = pipeline.transform(X_test)

run_pipeline_setup.log_model(pipeline, model_name="pipeline")

run_pipeline_setup.set_completed_status()
```

## Linear Regression
After the train-test-split, we can fit a linear regression model. We start a new run and 
link dataset and the pipeline as input artifacts.

```python
dataset_artifact_ref = ArtifactRef(name="USA housing dataset", version=1)
pipeline_artifact_ref = ArtifactRef(name="pipeline", version=1)
run_linear_regression = mlaide_client.start_new_run(experiment_key='linear-regression',
                                                    run_name='linear regression',
                                                    used_artifacts=[dataset_artifact_ref, pipeline_artifact_ref])
```

Now just fit your model as usual. After that, you can log the model with `log_model()` in ML Aide.

```python
lin_reg = LinearRegression(normalize=True)
lin_reg.fit(X_train,y_train)

run_linear_regression.log_model(lin_reg, 'linear regression')
```

Finally, we calculate some model metrics. The metrics will also be tracked in ML Aide.

```python
test_pred = lin_reg.predict(X_test)
train_pred = lin_reg.predict(X_train)

mae = metrics.mean_absolute_error(y_test, test_pred)
mse = metrics.mean_squared_error(y_test, test_pred)
rmse = np.sqrt(metrics.mean_squared_error(y_test, test_pred))
r2 = metrics.r2_score(y_test, test_pred)
cross_validation = cross_val_score(LinearRegression(), X, y, cv=10).mean()

run_linear_regression.log_metric('mae', mae)
run_linear_regression.log_metric('mse', mse)
run_linear_regression.log_metric('rmse', rmse)
run_linear_regression.log_metric('r2', r2)
run_linear_regression.log_metric('cross validation', cross_validation)

run_linear_regression.set_completed_status()
```

## Lasso Regression

Until now, we created three runs (`data preparation`, `pipeline setup`, and `linear regression`). All of t
hese runs belong to the experiment `linear-regression`.

Now we train another model type - a lasso regression model. But we want to reuse the results of the data 
preparation and the pipeline setup. With ML Aide this can be achieved simply by using a new `experiment_key` 
and provide the artifacts of the previous runs via `used_artifacts`.

```python
dataset_artifact_ref = ArtifactRef(name="USA housing dataset", version=1)
pipeline_artifact_ref = ArtifactRef(name="pipeline", version=1)
run_lasso = mlaide_client.start_new_run(experiment_key='lasso-regression',
                                        run_name='lasso regression',
                                        used_artifacts=[dataset_artifact_ref, pipeline_artifact_ref])
```

We fit our model as usual.

```python
alpha = 0.1
precompute = True
positive = True
selection = 'random'
random_state = 42

run_lasso.log_parameter('alpha', alpha)
run_lasso.log_parameter('precompute', precompute)
run_lasso.log_parameter('positive', positive)
run_lasso.log_parameter('selection', selection)
run_lasso.log_parameter('random state', random_state)
    
model = Lasso(alpha=alpha, 
              precompute=precompute, 
              positive=positive, 
              selection=selection,
              random_state=random_state)
model.fit(X_train, y_train)

run_lasso.log_model(model, 'lasso')
```

And now we calculate some metrics for this model, too.

```python
test_pred = model.predict(X_test)
train_pred = model.predict(X_train)

mae = metrics.mean_absolute_error(y_test, test_pred)
mse = metrics.mean_squared_error(y_test, test_pred)
rmse = np.sqrt(metrics.mean_squared_error(y_test, test_pred))
r2 = metrics.r2_score(y_test, test_pred)
cross_validation = cross_val_score(Lasso(), X, y, cv=10).mean()

run_lasso.log_metric('mae', mae)
run_lasso.log_metric('mse', mse)
run_lasso.log_metric('rmse', rmse)
run_lasso.log_metric('r2', r2)
run_lasso.log_metric('cross validation', cross_validation)

run_lasso.set_completed_status()
```

Start your python script using your shell with `python training.py`. After the script completed check the 
[Web UI](http://localhost:8880/projects/usa-housing) to see the created runs and the artifact.

## Summary

In this chapter we

- created a sklearn pipeline with a standard scaler
- trained a linear regression model
- trained a lasso regression model

All these steps were tracked in ML Aide as separate runs. The runs included all parameters and 
metrics that we need for reproducibility and further investigation. The pipeline and the models 
are stored as artifacts in ML Aide.

Your code should look like the following snippet shows.
??? note "Code"
    === "training.py"
        --8<-- "snippets/tutorial/training.py.md"
    === "data_preparation.py"
        --8<-- "snippets/tutorial/data_preparation.py.md"
    === "data/housing.csv"
        --8<-- "snippets/tutorial/data_housing.csv.md"

In the next chapter, we will learn how to evaluate models with ML Aide.
