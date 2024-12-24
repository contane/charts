# Helm chart for Foreman

Foreman is a Kubernetes application for managing Renovate jobs, developed by [Contane](https://contane.net).

Foreman is intended to be deployed together with self-hosted [Mend Renovate](https://www.mend.io/renovate/), either in
the same or a secondary Kubernetes cluster.
It provides a user interface for monitoring the Renovate CronJob including interactive progress and logs as well as the
ability to trigger custom jobs, speeding up the dependency upgrade cycle in the case of many repositories.

## Quick Reference

- Repository and documentation: https://github.com/contane/foreman
- Helm chart on GitHub: https://github.com/contane/charts/tree/main/charts/foreman
- Helm chart on Artifact Hub: https://artifacthub.io/packages/helm/contane-github/foreman
- Container image on Docker Hub: https://hub.docker.com/r/contane/foreman

Installation (see below for values.yaml parameters):

```sh
helm install -f my-values.yaml my-foreman \
    oci://ghcr.io/contane/charts/foreman
```

## Parameters

### Global configuration options

| Name                       | Description                                        | Value |
| -------------------------- | -------------------------------------------------- | ----- |
| `global.nameOverride`      | String to partially override foreman standard name | `""`  |
| `global.commonLabels`      | Labels to add to all deployed objects              | `{}`  |
| `global.commonAnnotations` | Annotations to add to all deployed objects         | `{}`  |

### Image configuration

| Name                | Description                              | Value             |
| ------------------- | ---------------------------------------- | ----------------- |
| `image.repository`  | Docker image repository                  | `contane/foreman` |
| `image.tag`         | Docker image tag                         | `0.4.3`           |
| `image.pullPolicy`  | Docker image pull policy                 | `IfNotPresent`    |
| `image.pullSecrets` | Docker registry secret names as an array | `[]`              |

### Common configuration options

| Name                 | Description                  | Value |
| -------------------- | ---------------------------- | ----- |
| `replicaCount`       | Number of replicas to deploy | `2`   |
| `serviceAccountName` | Service Account Name         | `""`  |

### Resource requests and limits

| Name                        | Description                                             | Value   |
| --------------------------- | ------------------------------------------------------- | ------- |
| `resources.limits.memory`   | The maximum amount of memory that the container can use | `512Mi` |
| `resources.limits.cpu`      | The maximum amount of CPU that the container can use    | `250m`  |
| `resources.requests.memory` | The requested memory for the container                  | `256Mi` |
| `resources.requests.cpu`    | The requested CPU for the container                     | `100m`  |

### Ingress configuration

| Name                     | Description                          | Value                 |
| ------------------------ | ------------------------------------ | --------------------- |
| `ingress.className`      | Ingress class name                   | `nginx`               |
| `ingress.host`           | IP or hostname to access the service | `foreman.dev.local`   |
| `ingress.path`           | Path within the url structure        | `/`                   |
| `ingress.annotations`    | Ingress annotations                  | `{}`                  |
| `ingress.tls.secretName` | TLS secret name                      | `foreman-ingress-tls` |

### Application runtime configuration

| Name                            | Description                                                                | Value   |
| ------------------------------- | -------------------------------------------------------------------------- | ------- |
| `config.existingSecret`         | Name of an existing secret containing the configuration                    | `""`    |
| `config.existingConfigMap`      | Name of an existing configmap containing the configuration                 | `""`    |
| `config.cronJob.namespace`      | Namespace where the CronJob is deployed                                    | `""`    |
| `config.cronJob.name`           | Name of the CronJob                                                        | `""`    |
| `config.cookies.key`            | Key which is used to encrypt the session cookie                            | `""`    |
| `config.cookies.maxAge`         | Max age of the session cookie, e.g. "24h" or "7 days"                      | `""`    |
| `config.auth.local.enabled`     | Enable local authentication                                                | `false` |
| `config.auth.local.username`    | Username of the local admin user                                           | `""`    |
| `config.auth.local.password`    | Password of the local admin user                                           | `""`    |
| `config.auth.oidc.enabled`      | Enable OIDC authentication                                                 | `false` |
| `config.auth.oidc.issuer`       | Issuer of the OIDC provider                                                | `""`    |
| `config.auth.oidc.clientId`     | Client ID of the OIDC provider                                             | `""`    |
| `config.auth.oidc.clientSecret` | Client Secret of the OIDC provider                                         | `""`    |
| `config.auth.oidc.publicUrl`    | Public URL of the foreman instance                                         | `""`    |
| `config.gitlab.host`            | Optional: URL of the GitLab instance (if GitLab features should be active) | `""`    |
