# Docker-and-Jenkins-setup

Certainly, here's a complete set of commands to install Docker and set up Jenkins using Docker on an Amazon Linux 2 instance in AWS:

**Step 1: Update the Package Repository**

```bash
sudo yum update -y
```

**Step 2: Install Docker**

```bash
sudo yum install docker -y
```

**Step 3: Start and Enable the Docker Service**

```bash
sudo service docker start
```

```
service docker status
```

**Step 4: Add Your User to the Docker Group**

```bash
sudo usermod -a -G docker ec2-user
```

**Step 5: Log Out and Log Back In (or use su)**

```bash
su - ec2-user
```

**Step 6: Verify Docker Installation**

```bash
docker --version
```

**Step 7: Pull and Run Jenkins Docker Container**

```bash
docker pull jenkins/jenkins
docker run -d -p 8080:8080 -p 50000:50000 jenkins/jenkins
```

**Step 8: Access Jenkins**

1. Find the public IP address of your AWS EC2 instance:

   ```bash
   curl http://checkip.amazonaws.com
   ```

2. Open a web browser and go to `http://<Your-EC2-Public-IP>:8080`. You will be prompted to unlock Jenkins.

3. 
![Screenshot 2023-10-24 193648](https://github.com/vishal815/Docker-and-Jenkins-setup/assets/83393190/82afc61a-e0ee-4117-a0aa-d42e996c5c46)

4. Retrieve the initial admin password by running the following command on your EC2 instance:

   ```bash
   docker exec $(docker ps -q --filter "ancestor=jenkins/jenkins") cat /var/jenkins_home/secrets/initialAdminPassword
   ```

   This command will display the initial admin password. Copy it.

5. Paste the initial admin password into the Jenkins web interface to unlock Jenkins.
![Screenshot 2023-10-24 195106](https://github.com/vishal815/Docker-and-Jenkins-setup/assets/83393190/85e9a4b3-bb0e-451a-9707-f09a22a88a01)

![Screenshot 2023-10-24 195430](https://github.com/vishal815/Docker-and-Jenkins-setup/assets/83393190/ba3750e9-08d3-4556-8616-e5bc7a79d8e4)



**Step 9: Jenkins Setup**

1. Follow the Jenkins setup wizard to install recommended plugins and create an admin user.

2. Once the setup is complete, you can start using Jenkins to create and manage your CI/CD pipelines.
