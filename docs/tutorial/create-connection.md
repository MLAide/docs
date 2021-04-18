# Create Connection

First we have to create a new python file in our working directory. Create
the file `app.py`.

First of all we need to import all libraries - including ML Aide.

```python
from mlaide import MLAideClient, ConnectionOptions, ArtifactRef
import pandas as pd
from sklearn import metrics
from sklearn.model_selection import cross_val_score, train_test_split
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
```

Now we are ready to create a connection using the API key.

```python
options = ConnectionOptions(
    mvc_server_url='http://localhost:8881/api/v1', # the ML Aide demo server runs on port 8881 per default
    api_key='<your api key>'
)
mlaide_client = MLAideClient(project_key='usa-housing', options=options)
```

The next step is to load and prepare the dataset.
