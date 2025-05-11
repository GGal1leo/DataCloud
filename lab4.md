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

---

# Open the application to outside traffic

1. Create a Kubernetes Gateway for the Bookinfo application:
```bash
kubectl apply -f samples/bookinfo/gateway-api/bookinfo-gateway.yaml
``` 
2. Change the service type to ClusterIP by annotating the gateway:
```bash
kubectl annotate gateway bookinfo-gateway networking.istio.io/service-type=ClusterIP --namespace=default
```
3. To check the status of the gateway, run:
```bash
kubectl get gateway
```

**Access the application:**

![Bookinfo Application](./assets/Screenshots/portforward)

---

# View the dashboard

1. Install Kiali and the other addons and wait for them to be deployed.
```bash
kubectl apply -f samples/addons
kubectl rollout status deployment/kiali -n istio-system
```
2. Access the Kiali dashboard:
```bash
istioctl dashboard kiali
```

