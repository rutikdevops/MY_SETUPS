- Go to AWS account -> launc instance -> ubuntu 18.04-> t2.medium (2CPU)
- Now access via putty-> login as "ubuntu"
```bash
sudo su
apt update && apt -y install docker.io
// install Kubectl
- curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl

// install Minikube
- curl -Lo minikube https://storage.googleapis.com/miniku... && chmod +x minikube && sudo mv minikube /usr/local/bin/ 
```




