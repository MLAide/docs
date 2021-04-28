```python
options = ConnectionOptions(
    server_url='http://localhost:8881/api/v1', # the ML Aide demo server runs on port 8881 per default
    api_key='<your api key>'
)
mlaide_client = MLAideClient(project_key='usa-housing', options=options)
```