# Helm Chart for x-man

## Docker Images

Currently there are no public Docker images available for x-man.

You need your own container registry to use this chart.

Follow these steps to build and locally publish the required images:

- Download x-man from https://github.com/Landesarchiv-Thueringen/x-man
- In the repository, copy `.env.example` to `.env` and provide the following values:
    - `IMAGE_PREFIX`:  
      Your registry + a prefix you would like to use for all image, e.g., `your.docker.registry:5001/lath/x-man`
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
imageRootRepository: lath/x-man
# You probably need to create a secret for your registry credentials. Refer to Kubernetes documentation for further information.
imagePullSecrets:
  - name: my-reg-cred

# Useful when updating Docker images behind a static tag.
imagePullPolicy: Always
# In case you chose a custom tag for `IMAGE_VERSION` above, use the same value here.
imageTag: "dev"

# Domain for making the installation available.
ingress:
  host: x-man.my-k8s-cluster.de
```

See [values.yaml](./values.yaml) for further configuration values.

## Transfer Directories

This chart does not contain a service to transfer xdomea messegas.

The following methods can be used.

### Using a Local Volume

You can add entries to `.server.volumes` and `.server.volumeMounts` and find
some means to make the mounted directory available.

In the x-man UI, you can then add a "Abgebende Stelle", pointing its transfer
dir to the mounted volume using a file:// URL.

### Deploy a WebDav Server

You can use your Kubernetes installation to deploy a WebDav server, for example
https://github.com/danuk/k8s-webdav. Note the URL you configured for its
ingress.

In the x-man UI, you can then add a "Abgebende Stelle", pointing its transfer
dir to this URL using dav:// or davs://.