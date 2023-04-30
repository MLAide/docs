# mlaide

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.1.0](https://img.shields.io/badge/AppVersion-0.1.0-informational?style=flat-square)

A Helm chart to install ML Aide on Kubernetes

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | minio | 11.10.25 |
| https://charts.bitnami.com/bitnami | mongodb | 13.1.5 |
| https://codecentric.github.io/helm-charts | keycloak | 18.4.0 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| fullnameOverride | string | `""` | String to fully override mlaide.fullname template |
| imagePullSecrets | list | `[]` | The name of the secret containing docker registry credentials. Secret must exist in the same namespace as the helm release. |
| keycloak.enabled | bool | `false` | Specifies whether this Helm chart should install Keycloak. |
| minio.enabled | bool | `false` | Specifies whether this Helm chart should install MinIO (S3). |
| mongodb.enabled | bool | `false` | Specifies whether this Helm chart should install MongoDB. |
| nameOverride | string | `""` | String to partially override mlaide.fullname template (will maintain the release name) |
| oidc | object | see below | Configures OpenID Connect (OIDC) for MLAide. |
| oidc.audience | string | `nil` | The audience specified in the access token issued by the authorization server. |
| oidc.issuer | string | `nil` | The issuer URL of the authorization server. |
| oidc.scope | string | `nil` | The scopes to request during login. |
| oidc.ui.clientId | string | `nil` | The client ID of MLAide registered on the authorization server. |
| oidc.webserver.jwkSetUri | string | `nil` | The JWKS URI provided by the authorization server. |
| oidc.webserver.nicknamePropertyName | string | `nil` | The property name withing the user info JSON containing  the nickname/name of the user. |
| oidc.webserver.userInfoEndpoint | string | `nil` | The User Info Endpoint URI provided by the authorization server to retrieve user details. |
| ui.affinity | object | `{}` | Pod affinity. |
| ui.autoscaling.enabled | bool | `false` | Specifies whether autoscaling should be enabled. |
| ui.autoscaling.maxReplicas | int | `100` | The maximum number of Pods when autoscaling is enabled. |
| ui.autoscaling.minReplicas | int | `1` | The minimum number of Pods when autoscaling is enabled. |
| ui.autoscaling.targetCPUUtilizationPercentage | string | `nil` | The target CPU utilization for the horizontal pod autoscaler. |
| ui.autoscaling.targetMemoryUtilizationPercentage | string | `nil` | The target memory utilization for the horizontal pod autoscaler. |
| ui.image.pullPolicy | string | `"IfNotPresent"` | The pull policy for the MLAide UI image. |
| ui.image.repository | string | `"mlaide/web-ui"` |  |
| ui.image.tag | string | `"latest"` | The tag of the MLAide UI image. |
| ui.ingress.annotations | object | `{}` | Ingress annotations. |
| ui.ingress.className | string | `""` | The name of the Ingress Class associated with the ingress. |
| ui.ingress.enabled | bool | `false` | Specifies whether a ingress should be created. |
| ui.ingress.hosts[0].host | string | `nil` | Host for the ingress rule. |
| ui.ingress.hosts[0].paths[0].path | string | `"/"` | Path for the Ingress rule. |
| ui.ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` | Path Type for the Ingress rule. |
| ui.ingress.tls | list | `[]` | TLS configuration. |
| ui.nodeSelector | object | `{}` | Node labels for Pod assignment. |
| ui.podAnnotations | object | `{}` | Pod annotations for MLAide UI. |
| ui.podSecurityContext | object | `{}` | Pod security context configuration to be applied for MLAide UI. |
| ui.replicaCount | int | `1` | The number of replicas of the UI deployment. |
| ui.resources | object | `{}` | Pod resource requests and limits. |
| ui.securityContext | object | `{}` | Container security context configuration to be applied for MLAide UI. |
| ui.service.port | int | `80` | The port for the MLAide UI service. |
| ui.service.type | string | `"ClusterIP"` | The type of service to create for the MLAide UI. |
| ui.serviceAccount.annotations | object | `{}` | Annotations to add to the service account. |
| ui.serviceAccount.create | bool | `true` | Specifies whether a service account should be created. |
| ui.serviceAccount.name | string | `"ui"` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template. |
| ui.tolerations | list | `[]` | Node taints to tolerate. |
| webserver.affinity | object | `{}` | Pod affinity. |
| webserver.autoscaling.enabled | bool | `false` | Specifies whether autoscaling should be enabled. |
| webserver.autoscaling.maxReplicas | int | `100` | The maximum number of Pods when autoscaling is enabled. |
| webserver.autoscaling.minReplicas | int | `1` | The minimum number of Pods when autoscaling is enabled. |
| webserver.autoscaling.targetCPUUtilizationPercentage | string | `nil` | The target CPU utilization for the horizontal pod autoscaler. |
| webserver.autoscaling.targetMemoryUtilizationPercentage | string | `nil` | The target memory utilization for the horizontal pod autoscaler. |
| webserver.image.pullPolicy | string | `"IfNotPresent"` | The pull policy for the MLAide UI image. |
| webserver.image.repository | string | `"mlaide/webserver"` |  |
| webserver.image.tag | string | `"latest"` | The tag of the MLAide UI image. |
| webserver.ingress.annotations | object | `{}` | Ingress annotations. |
| webserver.ingress.className | string | `""` | The name of the Ingress Class associated with the ingress. |
| webserver.ingress.enabled | bool | `false` | Specifies whether a ingress should be created. |
| webserver.ingress.hosts[0].host | string | `nil` | Host for the ingress rule. |
| webserver.ingress.hosts[0].paths[0].path | string | `"/"` | Path for the Ingress rule. |
| webserver.ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` | Path Type for the Ingress rule. |
| webserver.ingress.tls | list | `[]` | TLS configuration. |
| webserver.loggingLevel | string | `"INFO"` | The logging level. Must be one of [TRACE, DEBUG, INFO, WARN, ERROR] |
| webserver.mongodb.database | string | `nil` | The MongoDB® database name. |
| webserver.mongodb.host | string | `nil` | The MongoDB® hostname. |
| webserver.mongodb.password | string | `nil` | The MongoDB® password. This will be stored as a kubernetes secret. |
| webserver.mongodb.port | string | `nil` | The MongoDB® port. |
| webserver.mongodb.username | string | `nil` | The MongoDB® username. This will be stored as a kubernetes secret. |
| webserver.nodeSelector | object | `{}` | Node labels for Pod assignment. |
| webserver.podAnnotations | object | `{}` | Pod annotations for MLAide UI. |
| webserver.podSecurityContext | object | `{}` | Pod security context configuration to be applied for MLAide UI. |
| webserver.replicaCount | int | `1` | The number of replicas of the UI deployment. |
| webserver.resources | object | `{}` | Pod resource requests and limits. |
| webserver.s3.accessKey | string | `nil` | The S3 access key. This will be stored as a kubernetes secret. |
| webserver.s3.host | string | `nil` | The S3 hostname. |
| webserver.s3.port | string | `nil` | The S3 port. |
| webserver.s3.secretKey | string | `nil` | The S3 secret key. This will be stored as a kubernetes secret. |
| webserver.securityContext | object | `{}` | Container security context configuration to be applied for MLAide UI. |
| webserver.service.port | int | `80` | The port for the MLAide UI service. |
| webserver.service.type | string | `"ClusterIP"` | The type of service to create for the MLAide UI. |
| webserver.serviceAccount.annotations | object | `{}` | Annotations to add to the service account. |
| webserver.serviceAccount.create | bool | `true` | Specifies whether a service account should be created. |
| webserver.serviceAccount.name | string | `"webserver"` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template. |
| webserver.tolerations | list | `[]` | Node taints to tolerate. |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.11.0](https://github.com/norwoodj/helm-docs/releases/v1.11.0)
