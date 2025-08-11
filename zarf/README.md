### `zarf`

This directory contains the necessary Zarf configuration and artifacts to initialize a cluster and deploy a bundled application.

-----

### `artifacts`

This folder holds all the application binaries, images, and any other files required for deployment. All artifacts will be packaged into the final Zarf bundle.

**Note:** For development purposes, a symlink is currently used to point to the host file system for nginx deployment.

```bash
ln -s /home/bastiyan/Documents/git/seeder/zarf/artifacts /opt/hci-provisioner/web/
```

-----

### `init`

This folder contains the Zarf `init` configuration. Before deploying any packages, you must first initialize your cluster.

1.  **Download the `init` package:**

    ```bash
    zarf tools download init
    ```

2.  **Initialize the `k3s` cluster:**

    This will initialize the cluster with the default `k3s` configuration.

    ```bash
    sudo zarf init
    ```
    and accept defaults

-----

### `deploy`

This folder will contain the final Zarf package and its corresponding Software Bill of Materials (SBOM).

1.  **Create the Zarf package:**

    From the `zarf/` directory, run the following command to create your deployment package. The final package and its SBOM will be placed in the `deploy/` folder.

    ```bash
    zarf package create -o ./deploy/ --sbom-out ./deploy/sbom
    ```

2.  **Deploy the package:**

    Once the cluster is initialized, you can deploy the package to it.

    ```bash
    cd deploy
    sudo zarf package deploy ./deploy/<your-package-name>.tar.zst
    ```

-----

### Directory Structure

```text
zarf/
├── artifacts/
├── deploy/
└── init/
```