<h1 align="center">Lizz compatible Cluster Issuer application</h1>

Lizz compatible application to add the [Cluster Issuer application](https://cert-manager.io/docs/configuration/) to a lizz managed Kubernetes cluster.
The Cluster Issuer application is simply a Cluster Issuer resource that is added to the cluster.
Therefore it can be added only if the Cert-manager application is already added.

To learn more about Lizz, see the [documentation](https://openlizz.com).

## Requirements

To add the application, you first need to have a [Kubernetes cluster initialized with Lizz](https://openlizz.com/docs/guides/init).
You also need to have the [Lizz CLI installed](https://openlizz.com/docs/installation).

## Add the application

To add the application to your cluster, run the following:

```bash
lizz add github \
    --owner=$GITHUB_USER  \
    --fleet=fleet \
    --origin-url=https://github.com/openlizz/application-cert-manager \
    --path=./ca or ./selfsigned_ca or ./http01 or ./http01_staging \
    --destination=cert-manager \
    --cluster-role \
    --personal
```

> **Note**
> The `--path` you choose will define the type of Cluster Issuer created. Depending on what you choose, you might need to set values with the `--set-value` flag.

Check the [guide](https://openlizz.com/docs/guides/add) to understand how works the lizz add command.


> **Note**
> You can adapt the command depending on your use case. See the [command API](https://openlizz.com/docs/cli/lizz_add_github) for more information.

Reconcile the fleet repository to deploy the application using [Flux](https://fluxcd.io/):

```
flux reconcile source git flux-system
```

