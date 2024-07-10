# Contane Helm Charts

A collection of Helm charts for open-source applications developed by Contane, designed to simplify the deployment on Kubernetes.

## Features

- **Ready to Use**: All Helm Charts in this repository are pre-configured for immediate use. They can be deployed with default settings, making it easy to get started.
- **Customizable**: For production environments, we highly recommend configuring the charts to suit your specific needs. Each chart provides various configuration options to tailor the deployment.
- **Consistent Updates**: Our charts are regularly updated to ensure compatibility with the latest versions of Kubernetes and Helm, as well as to include new features and bug fixes.

## Prerequisites

Before you begin, ensure you have the following:

- Kubernetes: refer to the Kubernetes [getting started guide](https://kubernetes.io/docs/setup/)
- Helm 3.x: refer to the [Helm install guide](https://helm.sh/docs/intro/install/)

## Installation of Contane Helm Charts

Follow these steps to get started:

### Using the OCI Registry

1. **Install a chart**:
   Replace `<chart-name>` with the name of the chart:
    ```bash
    helm install my-custom-release oci://ghcr.io/contane/charts/<chart-name>
    ```

2. **Verify the installation**:
    ```bash
    helm list
    kubectl get all -l app.kubernetes.io/instance=my-custom-release
    ```

### Using the Helm Chart Repository

1. **Add the repository**:
    ```bash
    helm repo add contane https://contane.github.io/charts
    helm repo update
    ```

2. **Install a chart**:
    Replace `<chart-name>` with the name of the chart:
    ```bash
    helm install my-custom-release contane/<chart-name>
    ```

3. **Verify the installation**:
    ```bash
    helm list
    kubectl get all -l app.kubernetes.io/instance=my-custom-release
    ```

## Verifying Charts

### Using the OCI Registry

If you are using our OCI registry you need to use the [helm-sigstore](https://github.com/sigstore/helm-sigstore) plugin to verify the downloaded artifact.

1. **Install the [Helm sigstore](https://github.com/sigstore/helm-sigstore) plugin**
   ```bash
   helm plugin install https://github.com/sigstore/helm-sigstore
   ```

2. **Verify the chart's integrity**:
    ```bash
    helm sigstore verify <chart-name>-<version>.tgz
    ```

### Using the Helm Chart Repository

To ensure the integrity and authenticity of the Helm charts, you can verify them by checking their provenance files, which contain digital signatures that confirm the chart's origin and contents. Follow these steps to verify a chart:

1. **Download the chart and its provenance file**:
    ```bash
    helm fetch contane/<chart-name> --prov
    ```

2. **Verify the chart's integrity**:
    ```bash
    helm verify <chart-name>-<version>.tgz
    ```

This command will check the chart against its provenance file and confirm whether the verification was successful. Verifying charts helps ensure they have not been tampered with and are from a trusted source. For more detailed information on chart verification, refer to the [Helm documentation](https://helm.sh/docs/topics/provenance/).

## Configuration

You can customize the charts by creating a `values.yaml` file and providing it during installation:

```bash
helm install my-custom-release contane/<chart-name> -f values.yaml
```

Refer to the `README.md` file in each chart's directory for detailed information on the available configuration options.

## Upgrading Charts

To upgrade an existing release to a newer version of the chart, use the following command:

```bash
helm upgrade my-custom-release contane/<chart-name>
```

## Uninstallation

To uninstall a release and remove all associated Kubernetes resources, use:

```bash
helm uninstall my-custom-release
```

## Contributing

We welcome contributions from the community! If you have suggestions, find a bug, or want to add new features, please open an issue or submit a pull request.
