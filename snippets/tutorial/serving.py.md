```python
from mlaide import MLAideClient, ConnectionOptions
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LinearRegression
import numpy as np

options = ConnectionOptions(
    server_url='http://localhost:8881/api/v1', # the ML Aide demo server runs on port 8881 per default
    api_key='<your api key>'
)
mlaide_client = MLAideClient(project_key='usa-housing', options=options)

# read the model
lin_reg: LinearRegression = mlaide_client.load_model('linear regression')

# read the pipeline containing the standard scaler
pipeline: Pipeline = mlaide_client.load_model('pipeline')

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
print(pred)
```