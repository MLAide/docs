Store the shown yaml as `s3.yaml` in your working directory and adopt it to your needs.

```yaml
webserver:
  s3:
    host: "my-release-minio"
    port: "9000"
    accessKey: "my-s3-user"
    secretKey: "my-s3-password"

# enable MinIO deployment
minio:
  enabled: true
  auth:
    rootUser: my-s3-user
    rootPassword: my-s3-password
```