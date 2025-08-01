# common steps: Configure Jenkins with Docker Agents on Ubuntu EC2 for CI/CD Pipelines

These are my personal notes while learning how to set up Jenkins and use Docker agents on a single Ubuntu EC2 instance.

---

## ✅ Step 1: Launch Ubuntu EC2 Instance
- Go to AWS Console → Launch an **Ubuntu EC2** instance.
- In the **Security Group**, allow:
  - Port 22 (SSH) – for logging in
  - Port 8080 (Custom TCP) – for accessing Jenkins

---

## 🔐 Step 2: Connect to EC2 via SSH
```bash
ssh -i "your-key.pem" ubuntu@<your-ec2-public-ip>
````

---

## ☕ Step 3: Install Java (Jenkins Prerequisite)

Jenkins requires Java to run.

```bash
sudo apt update
sudo apt install -y openjdk-17-jdk
java --version
```

---

## ⚙️ Step 4: Install Jenkins

📖 [Optional: Jenkins Docs](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu)

```bash
# Add Jenkins key
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

# Add Jenkins repo
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

# Update and install Jenkins
sudo apt-get update
sudo apt-get install -y jenkins
```

---

## ▶️ Step 5: Start & Enable Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Check if Jenkins is running:

```bash
ps -ef | grep jenkins
```

---

## 🌐 Step 6: Access Jenkins Web Interface

* Open browser and go to:

```
http://<your-ec2-public-ip>:8080
```

* If Jenkins doesn’t load:

  * Make sure port 8080 is open in the EC2 security group
  * Ensure Jenkins service is running

---

## 🔑 Step 7: Get Jenkins Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

* Paste the password into the Jenkins UI
* Install **Suggested Plugins**
* Create your **Admin Username & Password**

✅ Jenkins is now ready to use!

---

## 🐳 Step 8: Install Docker on the Same Server

We are using the same EC2 instance for Jenkins and Docker.

```bash
# Install Docker
sudo apt install -y docker.io

# Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker
```

---

## 👥 Step 9: Allow Jenkins and Ubuntu Users to Use Docker

> By default, Docker runs only for the root user. Add `jenkins` and `ubuntu` users to the Docker group.

```bash
sudo usermod -aG docker jenkins
sudo usermod -aG docker ubuntu
sudo systemctl restart docker
```

🔁 This allows Jenkins jobs to run Docker commands without permission issues.

---

## 🔌 Step 10: Install Docker Plugins in Jenkins

1. Go to:
   `Jenkins Dashboard > Manage Jenkins > Manage Plugins`

2. Under the **Available** tab, search and install:

   * `Docker Pipeline`

3. Restart Jenkins:

* From UI:
  `Manage Jenkins > Reload Configuration from Disk`

* Or from terminal:

```bash
sudo systemctl restart jenkins
```

---

✅ **Done! Jenkins is now integrated with Docker.**

You’re ready to start creating Docker-based pipelines in Jenkins.

Next steps:

* Connect Jenkins to GitHub (webhook)
* Write a Jenkinsfile
* Use Docker agents in the pipeline

---
