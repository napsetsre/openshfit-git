# GitOps

GitOps is a declarative way to implement continuous deployment helping you automate the following tasks:

* Multi-cluster consistency
* Git managed configurations
* Configuration as code

## Assumptions

* Access to an OpenShift Container Platform cluster using an account with cluster-admin permissions.

* Assume the oc command is installed on your local system.

## Installing GitOps Operator

Verify that the operator is available to the cluster from OperatorHub:
```shell
oc get packagemanifests -n openshift-marketplace | grep openshift-gitops-operator
```

Inspect the operator version:
```shell
oc describe packagemanifests openshift-gitops-operator -n openshift-marketplace
```

Install the openshift-gitops-operator:
```shell
oc apply -f cluster/gitops/subscription.yaml -n openshift-operators
```

> Note that a OperatorGroup already exists in the openshift-operators namespace.

## Cluster Argo CD Default Instance
OpenShift GitOps by default installs an Argo CD instance for the cluster.

Verify the default instance is installed:
```shell
oc get argocds.argoproj.io -n openshift-gitops
```

### Argo CD Project
Argo CD projects provide a logical grouping of Argo CD applications. 

Features:
- Manages source repositories
- Controls application deployments
- Defines application roles 

```shell
oc apply -k cluster/
```

### Additional Argo CD Instances
however additional instances maybe installed.

