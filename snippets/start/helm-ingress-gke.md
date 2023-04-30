To use a [Google Kubernetes Engine (GKE) Ingress](https://cloud.google.com/kubernetes-engine/docs/concepts/ingress)
use the following configuration.

1. Reserve static IP addresses on Google Cloud
2. Configure DNS entries
3. Configure Ingress for webserver and UI
4. Optional: Configure Ingress for Keycloak

---

#### 1. Reserve static IP addresses on Google Cloud
Google Cloud Load Balancers are assigned to a public IP address. You need to 
[reserve the IP addresses](https://cloud.google.com/compute/docs/ip-addresses/reserve-static-external-ip-address) 
by running the following commands.

??? note "Reserve IP addresses"
    ```shell
    # IP for webserver
    gcloud compute addresses create mlaide-webserver \
      --global \
      --ip-version IPV4
    ```

    ```shell
    # IP for UI
    gcloud compute addresses create mlaide-ui \
      --global \
      --ip-version IPV4
    ```

    ```shell
    # Optional: IP for Keycloak
    gcloud compute addresses create mlaide-keycloak \
      --global \
      --ip-version IPV4
    ```

---
#### 2. Configure DNS entries
Use your DNS management tool to configure the A-records for the three domains pointing 
to the reserved IP addresses. You can get the reserved IPs by using the following 
command: `gcloud compute addresses list`

Assign the IPs to the following domains using your DNS configuration tool:

* `mlaide-webserver` &rarr; `api.mlaide.<your-domain>`
* `mlaide-ui` &rarr; `mlaide.<your-domain>`
* Optional: `mlaide-keycloak` &rarr; `login.mlaide.<your-domain>`

---
#### 3. Configure Ingress for webserver and UI
Store the shown yaml as `ingress.yaml` in your working directory. 
Replace `<your-domain>` with your actual domain configured in the step above.

??? note "Webserver and UI Ingress"
    ```yaml
    webserver:
      ingress:
        enabled: true
        domain: api.mlaide.<your-domain>
        annotations:
          networking.gke.io/managed-certificates: mlaide-webserver-cert
          kubernetes.io/ingress.global-static-ip-name: mlaide-webserver
          kubernetes.io/ingress.class: gce
          kubernetes.io/ingress.allow-http: "false"
        hosts:
        - host: api.mlaide.<your-domain>
          paths:
            - path: /*
              pathType: ImplementationSpecific

    ui:
      ingress:
        enabled: true
        domain: mlaide.<your-domain>
        annotations:
          networking.gke.io/managed-certificates: mlaide-ui-cert
          kubernetes.io/ingress.global-static-ip-name: mlaide-ui
          kubernetes.io/ingress.class: gce
          kubernetes.io/ingress.allow-http: "false"
        hosts:
        - host: mlaide.<your-domain>
          paths:
            - path: /*
              pathType: ImplementationSpecific

    googleCloudPlatform:
      enableManagedCertificate: true
    ```

---
#### 4. Optional: Configure Ingress for Keycloak
If you want to use the Keycloak instance shipped with the Helm Chart, you need to add the ingress configuration for Keycloak. Add this to your `ingress.yaml`.

??? note "Keycloak Ingress"
    ```yaml
    keycloak:
      ingress:
        enabled: true
        domain: "login.mlaide.<your-domain>"
        rules:
          - host: "login.mlaide.<your-domain>"
            paths:
              - path: /*
                pathType: ImplementationSpecific
        tls: []
        annotations:
          networking.gke.io/managed-certificates: mlaide-keycloak-cert
          kubernetes.io/ingress.global-static-ip-name: mlaide-keycloak
          kubernetes.io/ingress.class: gce
          kubernetes.io/ingress.allow-http: "false"
    ```