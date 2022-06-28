# Sizing NGINX Ingress Controller with App Protect on AKS

##Overview

You can use this repository to replicate the testing environment we used for sizing the NGINX Ingress Controller with App Protect on a managed AKS (Azure Kubernetes Service)

## Requirements

NGINX App Protect WAF is only available with NGINX Plus. Before moving forward, make sure you have the NGINX Plus Ingress Controller with App Protect already installed and running in your Kubernetes cluster. You can get started with a [30 day free trial](https://www.nginx.com/free-trial-request-nginx-ingress-controller/) and following the [documentation](https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/) for installation steps.

## Deployment

Apply the backend app deployment

```
$ kubectl apply -f volumes.yaml
$ kubectl apply -f backend-deployment.yaml

Install and configure the NGINX Plus Ingress Controller. Replace the fields with <> brackets

```
$ kubectl apply -f nginx-config.yaml
$ kubectl apply -f nginx-ingress.yaml
$ kubectl apply -f nodeport.yaml
$ kubectl apply -f app-virtual-server.yaml
```

Enable App Protect on the NGINX Ingress Controller

```
$ kubectl apply -f app-protect/ap-banana-uds.yaml
$ kubectl apply -f app-protect/ap-dataguard-alarm-policy.yaml
$ kubectl apply -f app-protect/ap-logconf.yaml
$ kubectl apply -f app-protect/syslog.yaml
$ kubectl apply -f app-protect/waf.yaml
```

Uncomment the fields in the app-virtual-server.yaml and apply the updated VirtualServer resource.

```$ kubectl apply -f app-virtual-server.yaml```


## Author information

[Amir Rawdat](https://github.com/rawdata123)
