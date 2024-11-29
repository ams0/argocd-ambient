# argocd-ambient

An ArgoCD ApplicationSet to deploy Istio Ambient Mesh with ArgoCD. Tested on AKS, where the `MutatingWebhookConfiguration` and the `ValidatingWebhookConfiguration` need to ignore Azure-specific namespace labels. It combines public Istio Helm charts with locally-specified `values.yaml` files, as described in the [docs](https://argo-cd.readthedocs.io/en/latest/user-guide/multiple_sources/#helm-value-files-from-external-git-repository).

A second ApplicationSet deploys Gateway API's gateway

Note:
When the CiliumIdentity makes ArgoCD flaps on gateway creation:    l

```bash
kubectl edit cm argocd-cm -n argocd

data:
  resource.exclusions: |
    - apiGroups:
      - cilium.io
      kinds:
      - CiliumIdentity
      clusters:
      - "*"
```