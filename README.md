# k8s

## installing docker
### source: https://docs.docker.com/engine/install/ubuntu/

for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update

sudo apt-get install ca-certificates curl

sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL \https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo groupadd docker

sudo usermod -aG docker $USER

newgrp docker

## installing minikube
### source: https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download

curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

minikube start

minikube kubectl -- get po -A

minikube dashboard

## installing kubectl
### source: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

kubectl version --client

kubectl get po -A

## installing helm
### source: https://platform9.com/learn/v1.0/tutorials/helm-cli

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3

chmod 700 get_helm.sh

./get_helm.sh

## installing NGINX Ingress Controller using Helm
### source: https://platform9.com/learn/v1.0/tutorials/helm-cli

helm repo add nginx-stable https://helm.nginx.com/stable

helm repo update

helm install nginx-ingress nginx-stable/nginx-ingress --set rbac.create=true

kubectl get pods -A

kubectl get services -A

## installing NGINX Ingress Controller using minikube addon

minikube addons enable ingress

## isntalling Prometheus
### source: https://prometheus.io/docs/introduction/first_steps/

wget https://github.com/prometheus/prometheus/releases/download/v2.54.1/prometheus-2.54.1.linux-amd64.tar.gz

tar xvfz prometheus-2.54.1.linux-amd64.tar.gz

cd prometheus-2.54.1.linux-amd64

./prometheus --config.file=prometheus.yml

### source: https://prometheus.io/docs/prometheus/latest/installation/

docker pull prom/prometheus

## isntalling Grafana
### source: https://grafana.com/grafana/download

sudo apt-get install -y adduser libfontconfig1 musl

wget https://dl.grafana.com/enterprise/release/grafana-enterprise_11.2.0_amd64.deb

sudo dpkg -i grafana-enterprise_11.2.0_amd64.deb

#### or

wget https://dl.grafana.com/enterprise/release/grafana-enterprise-11.2.0.linux-amd64.tar.gz

tar -zxvf grafana-enterprise-11.2.0.linux-amd64.tar.gz
