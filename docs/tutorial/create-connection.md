# Create Connection

To create a connection to the ML Aide webserver with Python
clients you have to use `mlaide.MLAideClient`. An object
of this class is the main entry point for all kinds of operations.

```python
from mlaide import MLAideClient, ConnectionOptions
```
--8<-- "snippets/tutorial/connection.py.md"

Replace `api_key` with your personal API key that you created using the ML Aide Web UI.

The next step is to load and prepare the dataset.
