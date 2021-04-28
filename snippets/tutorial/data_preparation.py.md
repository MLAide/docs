```python
from mlaide import MLAideClient, ConnectionOptions
import pandas as pd

options = ConnectionOptions(
    server_url='http://localhost:8881/api/v1', # the ML Aide demo server runs on port 8881 per default
    api_key='<your api key>'
)
mlaide_client = MLAideClient(project_key='usa-housing', options=options)

run_data_preparation = mlaide_client.start_new_run(experiment_key='linear-regression', run_name='data preparation')

housing_data = pd.read_csv('data/housing.csv')

# add dataset as artifact
artifact = run_data_preparation.create_artifact(name="USA housing dataset", artifact_type="dataset", metadata={})
run_data_preparation.add_artifact_file(artifact, 'data/housing.csv')

run_data_preparation.set_completed_status()
```