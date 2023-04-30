Store the shown yaml as `iam.yaml` in your working directory. Replace `<your-domain>` with your actual domain.

```yaml
# enable Keycloak deployment
keycloak:
  enabled: true
  postgresql:
    fullnameOverride: my-release-keycloak-postgresql

oidc:
  audience: "https://api.mlaide.<your-domain>"
  issuer: "https://login.mlaide.<your-domain>/auth/realms/mlaide-demo"
  scope: "openid profile email offline_access"
  ui:
    clientId: "mlaide-k8s-demo"
  webserver:
    jwkSetUri: "https://login.mlaide.<your-domain>/auth/realms/mlaide-demo/protocol/openid-connect/certs"
    userInfoEndpoint: "https://login.mlaide.<your-domain>/auth/realms/mlaide-demo/protocol/openid-connect/userinfo"
    nicknamePropertyName: "preferred_username"
```