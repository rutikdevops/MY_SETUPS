- Go to AWS account -> launc instance -> ubuntu 18.04-> t2.medium (2CPU)
- Now access via putty-> login as "ubuntu"
```bash
sudo su
apt update && apt -y install docker.io
// install Kubectl
- curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl

// install Minikube
- curl -Lo minikube https://storage.googleapis.com/miniku... && chmod +x minikube && sudo mv minikube /usr/local/bin/

apt instll conntrack
minikube start --vm-driver=none
minikube status
kubectl version
kubectl get nodes
kubectl describe node (paste here ublic ip)
```

- Create Manifest file
```bash
kind: Pod                              
apiVersion: v1                     
metadata:                           
  name: testpod                  
spec:                                    
  containers:                      
    - name: c00                     
      image: ubuntu              
      command: ["/bin/bash", "-c", "while true; do echo Hello-Bhupinder; sleep 5 ; done"]
  restartPolicy: Never         # Defaults to Always

```
- Run the file
```bash
kubectl apply -f pod1.yml
```



















