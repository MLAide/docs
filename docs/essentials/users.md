# Users
## Overview
--8<-- "snippets/essentials/snippet-users.md"

## Features

### Show User Settings

???+ note "Instructions"
    === "GUI"
       1. Click the _User name_ button in the upper right corner to open the user drop down menu
       2. Click the _Settings_ button

### Update User Profile

???+ note "Instructions"
    === "GUI"
        1. Click the _User name_ button in the upper right corner to open the user drop down menu
        2. Click the _Settings_ button
        3. Click the _Profile_ button in the side navigation
        4. Change
            - _First name - optional_
            - _Last name - optional_
            - _Nickname_
        5. Confirm by clicking the _Save_ button

### Add API Key

???+ note "Instructions"
    === "GUI"
        1. Click the _User name_ button in the upper right corner to open the user drop down menu
        2. Click the _Settings_ button
        3. Click the _API Keys_ button in the side navigation
        4. Click the _Add API Key_ button
        5. Provide
            - _Description - optional_
            - _Expires at - optional_
        6. Confirm by clicking the _Create_ button

### Use API Key

???+ note "Instructions"
    === "Code"
        ```python
        options = client.MvcOptions(
            mvc_server_url='http://localhost:8881/api/v1',
            api_key='<api-key>'
        )
        mlaide_client = client.MvcClient(project_key='usa-housing', options=options)
        ```

### Delete API Key

???+ note "Instructions"
    === "GUI"
        1. Click the _User name_ button in the upper right corner to open the user drop down menu
        2. Click the _Settings_ button
        3. Click the _API Keys_ button in the side navigation
        4. Click the _Delete API Key_ button (:material-delete:) for the relevant API key