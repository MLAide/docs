# Models
## Overview
--8<-- "snippets/essentials/snippet-models.md"

### Show Models

???+ note "Instructions"
    === "GUI"
        1. Select the relevant project by clicking it in the home view or via the _Projects_ dropdown in the main navigation
        2. Click the _Models_ button in the side navigation

### Create Model

???+ note "Instructions"
    === "Code"
        ```python
        lin_reg = LinearRegression()
        lin_reg.fit(X_train, y_train)

        run.log_model(lin_reg, model_name="linear regression model")
        ```

### Edit Model

???+ note "Instructions"
    === "GUI"
        1. Select the relevant project by clicking it in the home view or via the _Projects_ dropdown in the main navigation
        2. Click the _Models_ button in the side navigation
        3. Click the _Edit Model_ button (:material-pencil:) for the relevant model
        4. Change
            - _Model stage_
            - _Note - optional_ 
        5. Confirm by clicking the _Update_ button

### Show Stage Log

???+ note "Instructions"
    === "GUI"
        1. Select the relevant project by clicking it in the home view or via the _Projects_ dropdown in the main navigation
        2. Click the _Models_ button in the side navigation
        3. Click the _Stage log_ button (:material-history:) for the relevant model
        4. Close by clicking the _Close_ button