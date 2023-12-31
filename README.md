# Istio

This repo has all necessaries helms to deploy istio and kiali

```bash
helm repo add istio https://istio-release.storage.googleapis.com/charts     
helm repo update
helm pull istio/base --untar --destination istio-system
helm pull istio/istiod --untar --destination istio-system
helm pull istio/gateway --untar --destination istio-system
```

Argo will show this names and could be easy to see on argocd.

## base

values.yaml is used as a reference to create the overlay-values.yaml.

Copy the values.yaml file to overlay-values.yaml as argocd will always look for overlay-values. Do not change anything on this chart.

## istiod

values.yaml is used as a reference to create the overlay-values.yaml.

Copy the values.yaml file to overlay-values.yaml as argocd will always look for overlay-values. Do not change anything on this chart.

## gateway

values.yaml is used as a reference to create the overlay-values.yaml.

Copy the values.yaml file to overlay-values.yaml as argocd will always look for overlay-values.

Replace service on overlay-values.yaml:

```yaml
service:
  type: NodePort
  ports:
  - name: status-port
    port: 15021
    protocol: TCP
    targetPort: 15021
    nodePort: 31021
  - name: http2
    port: 80
    protocol: TCP
    targetPort: 80
    nodePort: 31080
  - name: https
    port: 443
    protocol: TCP
    targetPort: 443
    nodePort: 31443
```
