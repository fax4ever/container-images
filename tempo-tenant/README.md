# Tempo Tenant RBAC Configuration

This directory contains Kubernetes RBAC resources for granting read access to Tempo traces for authenticated users.

## Files

- **cluster-role.yaml**: Defines a ClusterRole that grants `get` permissions on Tempo traces for `dev` and `prod` tenants
- **cluster-role-binding.yaml**: Binds the ClusterRole to all authenticated users (`system:authenticated` group)

## Deployment

To deploy these resources to OpenShift, run:

```bash
oc apply -f cluster-role.yaml cluster-role-binding.yaml
```

Or apply them separately:

```bash
oc apply -f cluster-role.yaml
oc apply -f cluster-role-binding.yaml
```

## Fetching Resources from Cluster

To retrieve the ClusterRole and ClusterRoleBinding from the cluster as YAML:

```bash
oc get clusterrole tempostack-traces-reader -o yaml
oc get clusterrolebinding tempostack-traces-reader -o yaml
```

Or save them to files:

```bash
oc get clusterrole tempostack-traces-reader -o yaml > cluster-role.yaml
oc get clusterrolebinding tempostack-traces-reader -o yaml > cluster-role-binding.yaml
```

To retrieve TempoMonolithic resources from the default namespace:

```bash
oc get tempomonolithic -n default -o yaml
```

Or get a specific TempoMonolithic resource by name:

```bash
oc get tempomonolithic <name> -n default -o yaml
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

