# Tiny k8s cluster
## How to add your app

### Example 1
Python flask rest app to solve lights off puzzle: [src](https://github.com/peijunz/lightsoff), [healthCheck](https://service.peijun.me/lightsoff/healthCheck)

Example API call
```sh
curl 'https://service.peijun.me/lightsoff/' \
  -H 'content-type: application/json' \
  --data-raw '[[1,1,0],[0,0,1],[1,1,1]]' -w "\n" 
```

Output:
```json
{"answer": [[0, 1, 1], [0, 1, 0], [1, 0, 1]], "status": "success"}
```


### Example 2
Lightsoff React app: [src](https://github.com/peijunz/lightsoff-react), [webpage](https://app.peijun.me/lightsoff/)

## Setup microk8s for `app.peijun.me`

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
