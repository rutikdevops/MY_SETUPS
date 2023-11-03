- Install Docker
```bash
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER   #my case is ubuntu
newgrp docker
sudo chmod 777 /var/run/docker.sock
```

- After the docker installation, we create a sonarqube container (Remember to add 9000 ports in the security group).
```bash
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
```
- Now our sonarqube is up and running

- Enter username and password, click on login and change password
```bash
username admin
password admin
```

- - Configure Sonar Server in Manage Jenkins
- - Grab the Public IP Address of your EC2 Instance, Sonarqube works on Port 9000, so <Public IP>:9000. Goto your Sonarqube Server. Click on Administration → Security → Users → Click on Tokens and Update Token → Give it a name → and click on Generate Token

- <img width="612" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/ada8904c-ab20-4b56-bc42-91c302a4fd32">

- - Create a token with a name and generate
 
  - <img width="629" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/6a9ca9b5-4607-4bd8-895e-154a28af9586">

- copy Token
- Goto Jenkins Dashboard → Manage Jenkins → Credentials → Add Secret Text. It should look like this
<img width="629" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/8e779cf2-907f-46f7-bcc3-4652ca62dfc0">


- You will this page once you click on create
<img width="627" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/98ae0ecf-18b6-4727-887f-cff834d29d87">

- Now, go to Dashboard → Manage Jenkins → System and Add like the below image.
<img width="637" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/1af612a1-a016-41d7-82c0-2cc7aafa2c80">

- Click on Apply and Save
- The Configure System option is used in Jenkins to configure different server
- Global Tool Configuration is used to configure different tools that we install using Plugins
- We will install a sonar scanner in the tools.

<img width="643" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/268365ef-ce9f-4f93-ae66-a0a27a4c9f3e">

- In the Sonarqube Dashboard add a quality gate also
- Administration--> Configuration-->Webhooks

<img width="609" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/c66dda59-78f1-49a6-aa1f-8d98a24f88c4">

- Click on Create
<img width="614" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/11c64a38-01bf-4458-8958-5dc7c547043d">

- Add details
#in url section of quality gate
```bash
<http://jenkins-public-ip:8080>/sonarqube-webhook/
```


<img width="615" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/9d5661a1-227d-4565-af1e-7188cb88f604">
- Let's go to our Pipeline and add the script in our Pipeline Script.


```bash
pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/Aj7Ay/Netflix-clone.git'
            }
        }
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Netflix \
                    -Dsonar.projectKey=Netflix '''
                }
            }
        }
```

- To see the report, you can go to Sonarqube Server and go to Projects.

<img width="634" alt="image" src="https://github.com/rutikdevops/MY_SETUPS/assets/109506158/b32f36d0-a43f-4af8-8838-13fb2d94f17b">


- You can see the report has been generated and the status shows as passed. You can see that there are 3.2k lines it scanned. To see a detailed report, you can go to issues.



# Reference:- 
- https://youtu.be/Rj9oQHC12c4?feature=shared
- https://mrcloudbook.hashnode.dev/devsecops-netflix-clone-ci-cd-with-monitoring-email














