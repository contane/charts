# Contane Helm Charts
Welcome to the Contane Helm Charts repository! Here, you'll find a collection of Helm Charts for all the open-source projects developed by Contane. These charts are designed to simplify the deployment and management of applications on Kubernetes clusters.

## Features
- **Ready to Use**: All Helm Charts in this repository are pre-configured for immediate use. They can be deployed with default settings, making it easy to get started.
- **Customizable**: For production environments, we highly recommend configuring the charts to suit your specific needs. Each chart provides various configuration options to tailor the deployment.
- **Consistent Updates**: Our charts are regularly updated to ensure compatibility with the latest versions of Kubernetes and Helm, as well as to include new features and bug fixes.

## Prerequisites
Before you begin, ensure you have the following:

- **A Running Kubernetes Cluster**: A functional Kubernetes cluster is required to deploy the Helm Charts. You can set up a cluster using Minikube, Kubernetes in Docker (Kind), or any cloud provider like GKE, EKS, or AKS.
- **Helm 3.x Installed**: Ensure that you have Helm version 3.x installed on your local machine. You can follow the official Helm installation guide for detailed instructions.

## Installation of Contane Helm Charts
Installing a Contane Helm Chart is straightforward. Follow these steps to get started:

### Using the Helm Chart Repository

1. **Add the Repository**:
    ```bash
    helm repo add contane https://ghcr.io/contane/charts
    helm repo update
    ```

2. **Install a Chart**:
    Replace `<chart-name>` with the name of the chart:
    ```bash
    helm install my-custom-release contane/<chart-name>
    ```

3. **Verify the Installation**:
    ```bash
    helm list
    kubectl get all -l app.kubernetes.io/instance=my-custom-release
    ```

### Using the OCI Registry

1. **Install a Chart**:
    Replace `<chart-name>` with the name of the chart:
    ```bash
    helm install my-custom-release oci://ghcr.io/contane/charts/<chart-name>
    ```

2. **Verify the Installation**:
    ```bash
    helm list
    kubectl get all -l app.kubernetes.io/instance=my-custom-release
    ```

## Configuration
While the charts come with sensible defaults, you can customize their behavior by providing your own values. To do this, you can create a `values.yaml` file and pass it during installation:

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

## License
This repository is licensed under the Apache-2.0 license. Feel free to use and modify the charts as per the terms of the license.

## Support
If you encounter any issues or have any questions, please open an issue in this repository. Our team and the community are here to help!

Thank you for using Contane Helm Charts!
