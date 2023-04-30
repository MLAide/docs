Store the shown yaml as `mongodb.yaml` in your working directory and adopt it to your needs.

```yaml
webserver:
  mongodb:
    host: "my-mlaide-mongodb"
    port: "27017"
    username: "root"
    password: "mypassword"
    database: "mlaide"
    autoIndexCreation: true
    authenticationDatabase: admin

# enable MongoDB deployment
mongodb:
  enabled: true
  auth:
    databases:
    - mlaide
    rootPassword: mypassword
```