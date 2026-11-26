# oswapdevops-sec

## Kubernetes

The manifests use Kustomize. From the repository root, preview the development resources with:

```sh
kubectl kustomize k8s/overlays/dev
```

Apply them to a cluster with:

```sh
kubectl apply -k k8s/overlays/dev
```

The manifests create the `oswapdevops-sec` namespace. The frontend is exposed through a NodePort on port `30080`; access it at `http://<node-address>:30080` when your cluster permits NodePort traffic.

### Before using outside a disposable development cluster

`k8s/base/secret.yaml` currently contains a placeholder JWT signing value and is included in the manifests. Replace it with a strong, unique value before deploying, and do not commit real credentials. For production, manage secrets through your cluster's secret-management solution rather than keeping secret values in Git. MongoDB and Redis currently use ephemeral container storage; data will not survive pod replacement.

The backend image uses the `latest` tag. For repeatable deployments, publish and pin an immutable image tag or digest in the development overlay.
