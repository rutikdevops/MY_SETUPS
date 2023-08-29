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

sudo curl -s https://packages.cloud.google.com/apt... | sudo apt-key add 
```bash
sudo curl -s https://packages.cloud.google.com/apt... | sudo apt-key add     // we can able to connect master to node
nano /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
apt-get update
apt-get install -y kubelet kubeadm kubectl kubernetes-cni
```


- BOOTSTRAPPING THE MASTER NODE (IN MASTER)









