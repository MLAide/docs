```python
from mlaide import MLAideClient, ConnectionOptions, ArtifactRef
import pandas as pd
import numpy as np
from sklearn.model_selection import cross_val_score, train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression, Lasso
from sklearn import metrics

# create connection
options = ConnectionOptions(
    server_url='http://localhost:8881/api/v1', # the ML Aide demo server runs on port 8881 per default
    api_key='<your api key>'
)
mlaide_client = MLAideClient(project_key='usa-housing', options=options)

# get housing dataset
dataset_bytes = mlaide_client.get_artifact('USA housing dataset', version=None).load('data/housing.csv')
housing_data = pd.read_csv(dataset_bytes)

artifact_ref = ArtifactRef(name="USA housing dataset", version=1)
run_pipeline_setup = mlaide_client.start_new_run(experiment_key='linear-regression', 
                                                 run_name='pipeline setup', 
                                                 used_artifacts=[artifact_ref])

# train test split
X = housing_data[['Avg. Area Income', 'Avg. Area House Age', 'Avg. Area Number of Rooms',
               'Avg. Area Number of Bedrooms', 'Area Population']]
y = housing_data['Price']

test_size=0.3
random_state=42

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=test_size, random_state=random_state)

run_pipeline_setup.log_parameter('test_size', test_size)
run_pipeline_setup.log_parameter('random_state', random_state)

pipeline = Pipeline([
    ('std_scalar', StandardScaler())
])

X_train = pipeline.fit_transform(X_train)
X_test = pipeline.transform(X_test)

run_pipeline_setup.log_model(pipeline, model_name="pipeline")

run_pipeline_setup.set_completed_status()

# linear regression
dataset_artifact_ref = ArtifactRef(name="USA housing dataset", version=1)
pipeline_artifact_ref = ArtifactRef(name="pipeline", version=1)
run_linear_regression = mlaide_client.start_new_run(experiment_key='linear-regression',
                                                    run_name='linear regression',
                                                    used_artifacts=[dataset_artifact_ref, pipeline_artifact_ref])

lin_reg = LinearRegression(normalize=True)
lin_reg.fit(X_train,y_train)

run_linear_regression.log_model(lin_reg, 'linear regression')

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

# lasso regression
dataset_artifact_ref = ArtifactRef(name="USA housing dataset", version=1)
pipeline_artifact_ref = ArtifactRef(name="pipeline", version=1)
run_lasso = mlaide_client.start_new_run(experiment_key='lasso-regression',
                                        run_name='lasso regression',
                                        used_artifacts=[dataset_artifact_ref, pipeline_artifact_ref])

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