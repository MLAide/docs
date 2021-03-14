# Artifacts
## Overview
--8<-- "snippets/essentials/snippet-artifacts.md"

## Features

### Show Artifacts

???+ note "Instructions"
    === "GUI"
        1. Select the relevant project by clicking it in the home view or via the _Projects_ dropdown in the main navigation
        2. Click the _Artifacts_ button in the side navigation

### Create Artifact

???+ note "Instructions"
    === "Code"
        ```python
        artifact = run.create_artifact(name="my-dataset", artifact_type="dataset", metadata={})
        run.add_artifact_file(artifact, 'dataset.csv')
        ```