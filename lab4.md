# Install ISTIO

## Installing demo profile

```bash
istioctl install -f samples/bookinfo/demo-profile-no-gateways.yaml -y
```

## Add Namespace

```bash
kubectl label namespace default istio-injection=enabled
```

![Install Succesful](./assets/Screenshots/istioinstall)

---

# Install the Kubernetes Gateway API CRDs

1. Install the Gateway API CRDs, if they are not already present:
```bash
kubectl get crd gateways.gateway.networking.k8s.io &> /dev/null || \
{ kubectl kustomize "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v1.3.0-rc.1" | kubectl apply -f -; }
```

# Deploy the sample application

1. Deploy the Bookinfo sample application
```bash
kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml
```

2. Validate that the app is running inside the cluster by checking for the page title in the response
```bash
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage | grep -o "<title>.*</title>"
```

**Output:**

![Install Succesful](./assets/Screenshots/bookinfo)


