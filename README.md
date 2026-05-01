# JupyterLab DataMount Extension

[![Documentation](https://img.shields.io/badge/Documentation-passed-green)](https://jsc-jupyter.github.io/jupyterlab-data-mount/)
[![PyPI](https://img.shields.io/pypi/v/jupyterlab-data-mount)](https://pypi.org/project/jupyterlab-data-mount/)
[![npm](https://img.shields.io/npm/v/jupyterlab-data-mount)](https://www.npmjs.com/package/jupyterlab-data-mount)

A JupyterLab extension that enables users to securely mount external data storage locations directly into their running JupyterLab environment.

It is designed for JupyterHub deployments that want to provide users with seamless access to external storage systems such as B2DROP, S3-compatible object storage, AWS S3, or other rclone-supported services — without requiring users to manually configure mounts inside their notebooks.

The extension provides:

- A JupyterLab frontend for configuring and managing data mounts
- A server extension that handles secure communication and mount orchestration
- Support for reusable storage templates for common providers
- Integration with JupyterHub deployments for centrally managed and pre-configured mounts
- Secure handling of credentials without requiring elevated privileges inside user environments

This allows users to access external datasets as if they were local files inside JupyterLab, improving reproducibility, reducing manual setup, and simplifying workflows across distributed research infrastructures.

This extension is composed of:

- A Python package named `jupyterlab_data_mount` for the server extension
- A NPM package named `jupyterlab-data-mount` for the frontend extension

For detailed deployment options, configuration examples, and JupyterHub integration, see the full documentation:

https://jsc-jupyter.github.io/jupyterlab-data-mount/

![JupyterLab](https://jsc-jupyter.github.io/jupyterlab-data-mount/images/jupyterlab.png)

## Requirements

- JupyterLab >= 4.0.0

## Install

This extension must be configured in a JupyterHub Deployment. Please check documentation:

https://jsc-jupyter.github.io/jupyterlab-data-mount/spawner/installation/

## Troubleshoot

If you are seeing the frontend extension, but it is not working, check
that the server extension is enabled:

```bash
jupyter server extension list
```

If the server extension is installed and enabled, but you are not seeing
the frontend extension, check the frontend extension is installed:

```bash
jupyter labextension list
```

## Contributing

### Development install

Note: You will need NodeJS to build the extension package.

The `jlpm` command is JupyterLab's pinned version of
[yarn](https://yarnpkg.com/) that is installed with JupyterLab. You may use
`yarn` or `npm` in lieu of `jlpm` below.

```bash
# Clone the repo to your local environment
# Change directory to the jupyterlab_data_mount directory
# Install package in development mode
pip install -e ".[test]"
# Link your development version of the extension with JupyterLab
jupyter labextension develop . --overwrite
# Server extension must be manually installed in develop mode
jupyter server extension enable jupyterlab_data_mount
# Rebuild extension Typescript source after making changes
jlpm build
```

You can watch the source directory and run JupyterLab at the same time in different terminals to watch for changes in the extension's source and automatically rebuild the extension.

```bash
# Watch the source directory in one terminal, automatically rebuilding when needed
jlpm watch
# Run JupyterLab in another terminal
jupyter lab
```

With the watch command running, every saved change will immediately be built locally and available in your running JupyterLab. Refresh JupyterLab to load the change in your browser (you may need to wait several seconds for the extension to be rebuilt).

By default, the `jlpm build` command generates the source maps for this extension to make it easier to debug using the browser dev tools. To also generate source maps for the JupyterLab core extensions, you can run the following command:

```bash
jupyter lab build --minimize=False
```

### Development uninstall

```bash
# Server extension must be manually disabled in develop mode
jupyter server extension disable jupyterlab_data_mount
pip uninstall jupyterlab_data_mount
```

In development mode, you will also need to remove the symlink created by `jupyter labextension develop`
command. To find its location, you can run `jupyter labextension list` to figure out where the `labextensions`
folder is located. Then you can remove the symlink named `jupyterlab-data-mount` within that folder.

### Packaging the extension

See [RELEASE](RELEASE.md)
