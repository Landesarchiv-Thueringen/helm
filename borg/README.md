# Helm Chart for BorgFormat

Repository of BorgFormat: https://github.com/Landesarchiv-Thueringen/borg

## Docker Images

Currently there are no public Docker images available for BorgFormat.

You need your own container registry to use this chart.

Follow these steps to build and locally publish the required images:

- Download BorgFormat from https://github.com/Landesarchiv-Thueringen/borg
- In the repository, copy `.env.example` to `.env` and provide the following values:
    - `IMAGE_PREFIX`:  
      Your registry + a prefix you would like to use for all image, e.g., `your.docker.registry:5001/lath/borg`
    - `IMAGE_VERSION`:  
      Version tag for all images. Can be `appVersion` as declared in `Chart.yaml` or a custom tag like `dev`.
- Run `scripts/publish-images.sh`

## Configuration

For a working installation, you need to configure at least some values.

Create a file at the root level of this repository and fill adjust to your environment:

```yaml
# The registry you used to upload the docker images above (host+port).
imageRegistry: your.docker.registry:5001
# The repository prefix you chose for `IMAGE_PREFIX` above.
imageRootRepository: lath/borg
# You probably need to create a secret for your registry credentials. Refer to Kubernetes documentation for further information.
imagePullSecrets:
  - name: my-reg-cred

# Useful when updating Docker images behind a static tag.
imagePullPolicy: Always
# In case you chose a custom tag for `IMAGE_VERSION` above, use the same value here.
imageTag: "dev"

# Domain for making the installation available.
ingress:
  enabled: true
  hosts:
    - host: borg.my-k8s-cluster.de
      paths:
        - path: /
          pathType: Prefix
  tls:
    - hosts:
        - borg.my-k8s-cluster.de
```

## Installation

See [../README.md](../README.md#installation).