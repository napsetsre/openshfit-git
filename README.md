# GitOps

GitOps is a declarative way to implement continuous deployment helping you automate the following tasks:

* Multi-cluster consistency
* Git managed configurations
* Configuration as code

## GitOps Operator

### Assumptions

* Access to an OpenShift Container Platform cluster using an account with cluster-admin permissions.

* Assume the oc command is installed on your local system.

### Operator Installation

Verify that the operator is available to the cluster from OperatorHub:
```shell
oc get packagemanifests -n openshift-marketplace | grep openshift-gitops-operator
```

Inspect the operator version:
```shell
oc describe packagemanifests openshift-gitops-operator -n openshift-marketplace
```

```shell
oc get subscriptions.operators.coreos.com -n openshift-operators
```

```shell
oc apply -n openshift-operators -f- <<EOF

EOF
```

## Argo CD Features

* Resource requests and limits configured in Argo CD workloads.
* Argo CD authentication integrated with Red Hat SSO(keycloak).

