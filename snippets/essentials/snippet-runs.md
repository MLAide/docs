Runs belong to exactly one project and to none, one or many experiments. However, it is good practice to assign a run to at least one experiment. They may have input from previous runs and may generate outputs &ndash; named artifacts &ndash; such as models. Runs also contain parameters and metrics that are key value pairs to make them comparable.

???+ example "Example"

    _Project: House Price Prediction_

    - _Experiment 1: Linear Regression_
        - _Run 1: Data Preparation_
        - _Run 2: Test Train Split_
        - _Run 3: Linear Regression Training_
    - _Experiment 2: Random Forest Regression_
        - _Run 1: Data Preparation_
        - _Run 2: Test Train Split_
        - _Run 4: Random Forest Regression Training_