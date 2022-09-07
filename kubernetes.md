# Kubernetes Cheat Sheet

List all port forwards across all services:

```bash
kubectl get svc -o json | jq '.items[] | {name:.metadata.name, p:.spec.ports[] } | select( .p.nodePort != null ) | "\(.name): localhost:\(.p.nodePort) -> \(.p.port) -> \(.p.targetPort)"'

"web1: localhost:30329 -> 8080 -> 8080"
"web2: localhost:30253 -> 8080 -> 8080"

```

Source: [Stack Overflow](https://stackoverflow.com/questions/58878764/kubectl-list-all-port-forwards-across-all-services)
