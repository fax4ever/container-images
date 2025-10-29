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

# Custom Jaeger 2

```bash
oc delete project obs2
oc new-project obs2
```

```bash
kubectl -n obs2 apply -f jaeger2.yaml
```

```bash
kubectl -n obs2 port-forward svc/jaeger-query 16686:16686
```

```bash
kubectl -n obs2 port-forward svc/jaeger-collector 4318:4318
```