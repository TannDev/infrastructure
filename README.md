# TannDev Infrastructure

This repository contains the base Kubernetes configuration for Tanndev.com.

## Initial Setup
(Most notes in this section taken from the Digital Ocean tutorial on [setting up an nginx ingress](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes).)

After setting up a Kubernetes cluster in DigitalOcean, the following commands are used to set up the necessary load balancer and certificate issuer:
```shell script
# Set up the manditory resources for Nginx Ingress Controller.
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.26.1/deploy/static/mandatory.yaml

# Create a LoadBalancer Service.
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.26.1/deploy/static/provider/cloud-generic.yaml

# Wait for the LoadBalancer to finish setting up, and note the IP.
watch kubectl get svc --namespace=ingress-nginx

# Set up cert-manager namespace and install the cert-manager with its CRDs.
kubectl create namespace cert-manager
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.12.0/cert-manager.yaml

# Apply the cert-issuer from this repo.
kubectl apply -f cert-issuer.yaml

# Deploy the initial "cert-test" app from this repo.
kubectl apply -f cert-test.yaml

# Wait for the certificate to be issued.
watch kubectl describe certificate cert-test-tls
```
