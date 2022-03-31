# Running OpenProject on Kubernetes

This repository aims to provide a simple way to run [OpenProject](https://www.openproject.org/) on Kubernetes.

## Requirements

You will need to have access to a Kubernetes cluster. You will also need enough rights to create and manage resources in the cluster.

You will also need to create a postgres database.

## Assumptions

- This installation assumes you want to create all the resources into a namespace called 'openproject'.
- This installation assumes you want to use 'op.jaep.ch' as the domain name.

## Installation

### Database access

You will need to create a secret that contains the database url to the postgres database.
This secret could be defined by:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: database-url
  namespace: openproject
type: Opaque
data:
  database-url: <base64 encoded database url>
```

### Namespace

Note that you will need to create the namespace 'openproject' before running this.

`kubectl create namespace openproject`

You may create another namespace, but this change will have to be reflected in the yaml files (see below).

### Namespace (optional)

As the default namespace is 'openproject', you'll need to replace this word by the name of your namespace.

### Ingress

The current configuration assumes that you will use the 'op.jaep.ch' domain name. Change the ingress at will to reflect your needs.

### OpenProject

```shell
kubectl apply -f <path_of_the_repository> --recursive
```
