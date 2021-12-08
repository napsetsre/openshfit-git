# GitOps

GitOps is a declarative way to implement continuous deployment.

## Assumptions

* Access to an OpenShift Container Platform.
* Access to an account with cluster-admin permissions.
* Access the oc command on your local system.

## Installing GitOps Operator

Verify that the GitOps Operator is available to your cluster from OperatorHub:
```shell
oc get packagemanifests -n openshift-marketplace | grep openshift-gitops-operator
```

Inspect the operator version:
```shell
oc describe packagemanifests openshift-gitops-operator -n openshift-marketplace
```

Install the operator named `openshift-gitops-operator`:
```shell
kustomize build operators/overlays/openshift-gitops | oc apply -f-
```

> Note that a OperatorGroup already exists in the `openshift-operators` namespace.


Give the serviceAccount permission to admin the cluster.
```shell
oc adm policy add-cluster-role-to-user cluster-admin -z openshift-gitops-argocd-application-controller -n openshift-gitops
```
## Cluster Argo CD Default Instance
OpenShift GitOps by default installs an Argo CD instance for the cluster.

Verify the default instance is installed:
```shell
oc get argocds.argoproj.io -n openshift-gitops
```

### Argo CD Application

Install Argo CD application configurations:
```shell
kustomize build configurations/pricelist | oc apply -f-
```

```shell
kustomize build configurations/quarkus-app | oc apply -f-
```

#### Application Deployment
ArgoCD references your application deployment in GitHub.