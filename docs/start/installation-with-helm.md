# Installation with Helm

This document describes how to install the ML Aide in your Kubernetes cluster using Helm.
ML Aide requires an S3 compatible storage and MongoDB to store machine learning models
and metadata. Additionally, an identity and access management (IAM) system is required.
The helm chart can be configured to use external, existing installations of S3, MongoDB,
and IAM or to instantiate those as part of the Helm deployment.

## Prerequisites

- Kubernetes cluster 1.19+
- Helm 3.0+
- Any domain where you can configure A or AAAA records

## Adding the Helm Repository

```bash
helm repo add mlaide https://helm.mlaide.com
helm repo update
```

## Configure the Chart

ML Aide requires configuration of the following core functionalities:

- Expose ML Aide using Ingress (DNS and TLS configuration)
- Connection to S3 compatible storage
- Connection to MongoDB
- Connection to IAM using OpenID Connect (OIDC)

### Expose ML Aide using Ingress

=== "NGINX Ingress"
    TODO
=== "Google Cloud Ingress for HTTPS Load Balancing"
    --8<-- "snippets/start/helm-ingress-gke.md"

### Connection to S3 compatible storage
ML Aide uses the S3 (simple storage service) API to store artifacts. You can use AWS S3 or any
other S3 compatible service. The ML Aide helm charts can be installed using MinIO directly running
on Kubernetes.

=== "MinIO shipped with Helm Chart"
    --8<-- "snippets/start/helm-s3-included.md"
=== "AWS S3"
    TODO

### Connection to MongoDB
ML Aide uses the MongoDB to store projects, run, metrics, and other metadata. You can use any MongoDB instance or alternatively use MongoDB shipped as part of the helm chart.

=== "MongoDB shipped with Helm Chart"
    --8<-- "snippets/start/helm-mongodb-included.md"
=== "MongoDB"
    TODO

### Connection to IAM
=== "Keycloak shipped with Helm Chart"
    --8<-- "snippets/start/helm-iam-included.md"
=== "OpenID Connect provider"
    TODO

## Installing the Chart

Install the ML Aide helm chart with a release name `my-release`:

```bash
helm install --name my-release mlaide/mlaide
```

## Upgrading the Chart

To upgrade the release `my-release`:

```
helm upgrade my-release mlaide/mlaide
```

## Uninstalling the Chart

To uninstall the release `my-release`:

```
helm uninstall my-release
```

## Configuration
--8<-- "snippets/start/helm-configuration.md"