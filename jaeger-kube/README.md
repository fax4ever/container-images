# Custom Jaeger All in One

```bash
oc delete project obs
oc new-project obs
```

```bash
kubectl -n obs apply -f jaeger.yaml
```

```bash
kubectl -n obs port-forward svc/jaeger-query 16686:16686
```