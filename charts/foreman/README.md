# foreman - A Renovate UI

A Kubernetes application for managing Renovate jobs, developed by [Contane](https://contane.net).

Foreman is intended to be deployed together with self-hosted [Mend Renovate](https://www.mend.io/renovate/), either in
the same or a secondary Kubernetes cluster.
It provides a user interface for monitoring the Renovate CronJob including interactive progress and logs as well as the
ability to trigger custom jobs, speeding up the dependency upgrade cycle in the case of many repositories.

Fore more information consult the [documentation](https://github.com/contane/foreman).

## TL;DR

```bash
helm install my-custom-release oci://ghcr.io/contane/charts/foreman
```

If you want to use foreman in production we recommend proper configuration.

## Parameters

### Global parameters

| Name                       | Description                                        | Value |
|----------------------------|----------------------------------------------------|-------|
| `global.nameOverride`      | String to partially override foreman standard name | `""`  |
| `global.commonLabels`      | Labels to add to all deployed objects              | `{}`  |
| `global.commonAnnotations` | Annotations to add to all deployed objects         | `{}`  |

### Image parameters

| Name                | Description                              | Value             |
|---------------------|------------------------------------------|-------------------|
| `image.repository`  | Docker image repository                  | `contane/foreman` |
| `image.tag`         | Docker image tag                         | `0.1.0`           |
| `image.pullPolicy`  | Docker image pull policy                 | `IfNotPresent`    |
| `image.pullSecrets` | Docker registry secret names as an array | `[]`              |

### Resource parameters

| Name                        | Description                       | Value   |
|-----------------------------|-----------------------------------|---------|
| `resources.limits.memory`   | Memory limits for the container   | `512Mi` |
| `resources.limits.cpu`      | CPU limits for the container      | `250m`  |
| `resources.requests.memory` | Memory requests for the container | `256Mi` |
| `resources.requests.cpu`    | CPU requests for the container    | `100m`  |

### Ingress parameters

| Name                     | Description                     | Value                 |
|--------------------------|---------------------------------|-----------------------|
| `ingress.className`      | Memory limits for the container | `nginx`               |
| `ingress.host`           | Memory limits for the container | `foreman.dev.local`   |
| `ingress.path`           | Memory limits for the container | `/`                   |
| `ingress.annotations`    | Memory limits for the container | `{}`                  |
| `ingress.tls.secretName` | Memory limits for the container | `foreman-ingress-tls` |

### Config parameters

| Name                            | Description                                                                | Value   |
|---------------------------------|----------------------------------------------------------------------------|---------|
| `config.existingSecret`         | Name of an existing secret containing the configuration                    | `""`    |
| `config.existingConfigMap`      | Name of an existing configmap containing the configuration                 | `""`    |
| `config.cronJob.namespace`      | Namespace where the CronJob is deployed                                    | `""`    |
| `config.cronJob.name`           | Name of the CronJob                                                        | `""`    |
| `config.cookies.key`            | Key which is used to encrypt the session cookie                            | `""`    |
| `config.cookies.naxAge`         | Max age of the session cookie, e.g. "24h" or "7 days"                      | `""`    |
| `config.auth.local.enabled`     | Enable local authentication                                                | `false` |
| `config.auth.local.username`    | Username of the local admin user                                           | `""`    |
| `config.auth.local.password`    | Password of the local admin user                                           | `""`    |
| `config.auth.oidc.enabled`      | Enable OIDC authentication                                                 | `false` |
| `config.auth.oidc.issuer`       | Issuer of the OIDC provider                                                | `""`    |
| `config.auth.oidc.clientId`     | Client ID of the OIDC provider                                             | `""`    |
| `config.auth.oidc.clientSecret` | Client Secret of the OIDC provider                                         | `""`    |
| `config.auth.oidc.publicUrl`    | Public URL of the foreman instance                                         | `""`    |
| `config.gitlab.host`            | Optional: URL of the GitLab instance (if GitLab features should be active) | `""`    |

### Other parameters

| Name                 | Description                  | Value |
|----------------------|------------------------------|-------|
| `replicaCount`       | Number of replicas to deploy | `2`   |
| `serviceAccountName` | Service Account Name         | `""`  |
