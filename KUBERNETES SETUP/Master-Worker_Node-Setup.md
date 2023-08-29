# Video Reference :-
https://youtu.be/ftrAFHL6w2c?feature=shared

- Create 3 ec2 instance
- Here I will user free tier Ubuntu server
1 ec2 for Master = t2.medium
2 ec2 for Node = t2.micro

- Run these commands in all 3 instance :-
```bash
apt install docker.io -y
docker --version
systemctl start docker
systemctl enable docker
```

- sudo curl -s https://packages.cloud.google.com/apt... | sudo apt-key add                       // Go to doc-> apt-key.gpg-> copy address
- https://packages.cloud.google.com/apt/doc/apt-key.gpg
// both the links are same
```bash
sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add           // we can able to connect master to node
nano /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main                                            // paste this in nano file & ntrl-X & capital Y for exit
apt-get update
apt-get install -y kubelet kubeadm kubectl kubernetes-cni
```


- BOOTSTRAPPING THE MASTER NODE (IN MASTER NODE ONLY)
```bash
kubeadm init
//COPY THE COMMAND TO RUN IN NODES & SAVE IN NOTEPAD
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
```


- copy the command and paste it in notepad
![image](https://github.com/rutikdevops/MY_SETUPS/assets/109506158/b025aadf-899c-4f99-af6c-802a8445e1d6)

```bash
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-rbac.yml
```

- CONFIGURE WORKER NODES (IN NODES)
- COPY LONG CODE PROVIDED MY MASTER WHICH IS PRESENT IN NOTEPAD -> AND PASTE IT IN NODES
- e.g- kubeadm join 172.31.6.165:6443 --token kl9fhu.co2n90v3rxtqllrs --discovery-token-ca-cert-hash sha256:b0f8003d23dbf445e0132a53d7aa1922bdef8d553d9eca06e65c928322b3e7c0



- GO TO MASTER AND RUN THIS COMMAND
```bash
kubectl get nodes
```
















