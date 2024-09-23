# k8s

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

