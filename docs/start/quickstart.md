# Quickstart

This quickstart shows how to get ML Aide running on your local environment. This quickstart
is only for demo purposes and should not be used for a production setup.

ML Aide is shipped with Docker. Therefore you need [Docker](https://docs.docker.com/get-docker/) 
installed. On Linux you also have to install [Docker Compose](https://docs.docker.com/compose/install/).

## Clone Repo
Clone the ML Aide git repository
```
git clone https://github.com/MLAide/MLAide.git
```
For this quickstart you don't have to compile or build anything. We just need the `docker-compose.yaml` from 
the `demo/` directory.

## Prepare
Add the following entry to your hosts file, to make sure keycloack can verify the user tokens.
The file is located at `/etc/hosts` (Unix) or `C:\Windows\System32\drivers\etc\hosts` (Windows).
```
127.0.0.1 keycloak.mlaide
```

On Unix systems you can use the following command to add the entry to your hosts file.
```
echo '127.0.0.1 keycloak.mlaide' | sudo tee -a /etc/hosts
```

## Start
After that start ML Aide from your `demo/` folder that is located in the cloned repository using:
```
cd demo
docker-compose up
```

## Verify
Now you should have several containers running:

- **MLAide web user interface**
- **MLAide webserver**
- **MongoDB** that is used by the webserver to store all structured metadata
- **min.io** that is used by the webserver to store all artifacts and models
- **keycloak** to provide an identity provider, authentication and authorization

## Use
You can access the [Web UI on localhost:8880](http://localhost:8880) with your browser. This demo
provides three pre-defined users:

- adam (password = adam1, email = adam@demo.mlaide.com)
- bob (password = bob1, email = bob@demo.mlaide.com)
- eve (password = eve1, email = eve@demo.mlaide.com)

## Using the Python client
To track your machine learning runs you can use the Python client. Start the [Tutorial](../tutorial/introduction.md) for your first steps.