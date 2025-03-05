# Helm

Helm charts for projects of Landesarchiv Thüringen.

## Warning

The contents of this repository are in an **experimental** state. We have not
tested these charts against clusters that are configured for production use.
Configuration values might not work for some environments or might not work at
all.

## Requirements

- Working Kubernetes cluster
- Installed and configured `kubectl`
- `helm`

## Configuration

You can create configuration files on the root level of this repository.
Contents will override values of the files `values.yaml` in charts. Refer to
`values.yaml` for available values and documentation. For example:

```sh
touch borg-values.yaml
$EDITOR borg-values.yaml
```

## Installation

Use Helm to install these charts into your Kubernetes cluster. For example

```sh
# Install new release
helm install -f borg-values.yaml borg ./borg
# Upgrade existing release
helm upgrade -f borg-values.yaml borg ./borg
```