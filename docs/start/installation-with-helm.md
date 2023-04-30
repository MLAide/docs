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

1. Expose ML Aide using Ingress (DNS and TLS configuration)
2. Connection to S3 compatible storage
3. Connection to MongoDB
4. Connection to IAM using OpenID Connect (OIDC)

### 1. Expose ML Aide using Ingress

=== "NGINX Ingress"
    TODO
=== "Google Cloud Ingress for HTTPS Load Balancing"
    --8<-- "snippets/start/helm-ingress-gke.md"

### 2. Connection to S3 compatible storage
ML Aide uses the S3 (simple storage service) API to store artifacts. You can use AWS S3 or any
other S3 compatible service. The ML Aide helm charts can be installed using MinIO directly running
on Kubernetes.

=== "MinIO shipped with Helm Chart"
    --8<-- "snippets/start/helm-s3-included.md"
=== "AWS S3"
    TODO

### 3. Connection to MongoDB
ML Aide uses the MongoDB to store projects, run, metrics, and other metadata. You can use any MongoDB instance or alternatively use MongoDB shipped as part of the helm chart.

=== "MongoDB shipped with Helm Chart"
    --8<-- "snippets/start/helm-mongodb-included.md"
=== "MongoDB"
    TODO

### 4. Connection to IAM
=== "Keycloak shipped with Helm Chart"
    --8<-- "snippets/start/helm-iam-included.md"
=== "OpenID Connect provider"
    TODO

## Installing the Chart

Install the ML Aide helm chart with a release name `my-release`:

```bash
helm install my-release mlaide/mlaide -f ingress.yaml -f s3.yaml -f mongodb.yaml -f iam.yaml
```

## Try it out
Open the configured URL (`https://mlaide.<your-domain>`) for MLAide in your browser.

If you have installed MLAide using the built-in Keycloak, you can log in using the
pre-configured users:

* User: `adam@example.com`<br/>
  Password: `adam1`
* User: `bob@example.com`<br/>
  Password: `bob1`

If you have used another OpenID connect provider, use any registered user within
the particular provider.

## Upgrading the Chart

If you have a running installation of MLAide using Helm, you can update configured
paremeters using the follong command::

```
helm upgrade my-release mlaide/mlaide
```

## Uninstalling the Chart

To uninstall the release `my-release` use the following command:

```
helm uninstall my-release
```

## Configuration
--8<-- "snippets/start/helm-configuration.md"