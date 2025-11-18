# Tempo Tenant RBAC Configuration

## Deployment

To deploy these resources to OpenShift, run:

```bash
oc apply -f cluster-role-reader.yaml cluster-role-binding-reader.yaml
```

## Fetching Resources from Cluster

To retrieve the ClusterRole and ClusterRoleBinding from the cluster as YAML:

```bash
oc get clusterrole tempostack-traces-reader -o yaml
oc get clusterrolebinding tempostack-traces-reader -o yaml
```

To retrieve TempoMonolithic resources from the observability namespace:

```bash
oc get tempomonolithic -n observability -o yaml
```

Or get a specific TempoMonolithic resource by name:

```bash
oc get tempomonolithic <name> -n observability -o yaml
```

## Prerequisites

- OpenShift CLI (`oc`) installed and configured
- Logged in to the target OpenShift cluster
- Sufficient permissions to create ClusterRole and ClusterRoleBinding resources

## What This Does

The ClusterRole `tempostack-traces-reader` grants read access (`get` verb) to:
- Resources: `dev` and `prod` (Tempo tenant resources)
- Resource names: `traces`
- API group: `tempo.grafana.com`

The ClusterRoleBinding binds this role to all authenticated users in the cluster, allowing any authenticated user to read traces from the `dev` and `prod` Tempo tenants.

