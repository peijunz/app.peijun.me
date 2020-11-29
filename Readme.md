# Setting up cluster

```sh
sudo ufw default allow routed
sudo iptables -P FORWARD ACCEPT

sudo snap remove microk8s && sudo snap install microk8s --classic

microk8s config > .kube/config 

microk8s.enable rbac
microk8s enable ingress
microk8s enable dns

helm install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.1.0 --set installCRDs=true
```

Reference: https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes
