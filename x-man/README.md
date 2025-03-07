# Helm Chart for x-man

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