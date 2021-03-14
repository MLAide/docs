# Runs
## Overview
--8<-- "snippets/essentials/snippet-runs.md"

## Features

### Show Runs

???+ note "Instructions"
    === "GUI"
        1. Select the relevant project by clicking it in the home view or via the _Projects_ dropdown in the main navigation
        2. Click the _Runs_ button in the side navigation

### Create Run

???+ note "Instructions"
    === "Code"
        ```python
        run = mlaide_client.start_new_run(experiment_key='linear-regression',
                                          run_name='linear regression')
        ```

### Toggle Paramenters

???+ note "Instructions"
    === "GUI"
        1. Select the relevant project by clicking it in the home view or via the _Projects_ dropdown in the main navigation
        2. Click the _Runs_ button in the side navigation
        3. Click _:material-eye: Show Parameters_ button at the top of the runs table to show parameters for runs
        3. Click _:material-eye-off: Hide Parameters_ button at the top of the runs table to hide parameters for runs

### Compare Runs

???+ note "Instructions"
    === "GUI"
        1. Select the relevant project by clicking it in the home view or via the _Projects_ dropdown in the main navigation
        2. Click the _Runs_ button in the side navigation
        3. Select the relevant runs by clicking the checkbox
        4. Click the _:material-compare: Compare_ button at the top of the runs table

### Export Runs

???+ note "Instructions"
    === "GUI"
        1. Select the relevant project by clicking it in the home view or via the _Projects_ dropdown in the main navigation
        2. Click the _Runs_ button in the side navigation
        3. Select the relevant runs by clicking the checkbox
        4. Click the _:material-cloud-download: Export_ button at the top of the runs table
