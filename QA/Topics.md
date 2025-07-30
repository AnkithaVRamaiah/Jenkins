## **🔹 Topics to Learn in Jenkins for DevOps Engineers**  

### **1️⃣ Basics of Jenkins**  
## **✅ What is Jenkins?**  
Jenkins is an **open-source automation server** used for **Continuous Integration (CI) and Continuous Deployment (CD)**. It automates software development processes like building, testing, and deploying applications, ensuring fast and efficient delivery.  

### **Why Jenkins?**  
🔹 Eliminates manual deployment efforts  
🔹 Speeds up development cycles with automation  
🔹 Detects issues early through automated testing  
🔹 Works well with various DevOps tools (Docker, Kubernetes, AWS, Terraform, Ansible, etc.)  

---

## **✅ Features and Benefits of Jenkins**  

### **📌 Features of Jenkins**  
1️⃣ **Pipeline as Code** – Uses `Jenkinsfile` (written in Groovy) to define CI/CD pipelines.  
2️⃣ **Plugins Support** – Over **1,800+ plugins** to integrate with Git, Docker, Kubernetes, AWS, Terraform, etc.  
3️⃣ **Distributed Builds** – Supports Master-Agent model for parallel execution.  
4️⃣ **Declarative & Scripted Pipelines** – Allows flexibility in automation scripts.  
5️⃣ **Integration with SCM** – Works with GitHub, GitLab, Bitbucket, SVN.  
6️⃣ **Customizable Build Triggers** – Supports webhooks, cron jobs, SCM polling.  
7️⃣ **Security & Access Control** – Supports RBAC (Role-Based Access Control) and credentials management.  
8️⃣ **Cross-Platform Support** – Runs on Windows, Linux, macOS, Docker, Kubernetes.  

### **📌 Benefits of Jenkins**  
✅ **Open-source & Free** – No licensing cost.  
✅ **Highly Extensible** – Supports various DevOps tools via plugins.  
✅ **Automates Everything** – Reduces manual errors in software delivery.  
✅ **Scalable** – Can distribute workloads across multiple agents for faster execution.  
✅ **Strong Community Support** – Large global community for troubleshooting and updates.  

---

## **✅ Jenkins vs. GitHub Actions vs. GitLab CI/CD**  

| **Feature**          | **Jenkins** | **GitHub Actions** | **GitLab CI/CD** |
|----------------------|------------|--------------------|------------------|
| **Type**            | CI/CD Server | GitHub-native CI/CD | GitLab-native CI/CD |
| **Setup**           | Self-hosted | Managed by GitHub | Managed by GitLab |
| **Ease of Use**     | Complex, requires setup | Easier for GitHub users | Easier for GitLab users |
| **Pipeline Language** | Groovy (Jenkinsfile) | YAML (`.github/workflows/`) | YAML (`.gitlab-ci.yml`) |
| **Runner Type**     | Self-hosted | GitHub-hosted & self-hosted | GitLab-hosted & self-hosted |
| **Best for**        | Large-scale, customizable CI/CD | GitHub-based projects | GitLab-based projects |
| **Community Support** | Large & Mature | Growing rapidly | Strong for GitLab users |

**Which One to Use?**  
✔ **Use Jenkins** if you need full control, scalability, and integration with on-prem/self-hosted servers.  
✔ **Use GitHub Actions** if your code is hosted on GitHub and you prefer a fully managed CI/CD solution.  
✔ **Use GitLab CI/CD** if you are using GitLab and want native integration with its features.  

---

## **✅ Jenkins Architecture (Master-Agent Model)**  

### **📌 How Jenkins Works?**  
Jenkins follows a **Master-Agent** (or **Controller-Worker**) architecture where:  
1️⃣ **Jenkins Master (Controller)**  
   - Controls job scheduling and workflow execution  
   - Stores job configurations and build history  
   - Delegates tasks to **agents (workers)**  

2️⃣ **Jenkins Agent (Worker/Node)**  
   - Executes the jobs assigned by the master  
   - Can run on multiple machines to distribute the workload  
   - Supports Linux, Windows, macOS, and Docker-based agents  

### **📌 Workflow in Jenkins Master-Agent Model**  
1. **Developer pushes code** to GitHub/GitLab.  
2. **Jenkins Master triggers a job** (based on webhook, polling, or schedule).  
3. **Jenkins Master assigns the job** to an available agent.  
4. **Agent executes the pipeline** (build, test, deploy).  
5. **Results sent back** to the master, and notifications (email, Slack, etc.) are triggered.  

### **📌 Why Use Agents?**  
✅ **Scalability** – Run multiple jobs in parallel.  
✅ **Load Distribution** – Prevents overload on the master.  
✅ **Platform Independence** – Run different jobs on different environments (Windows, Linux, macOS).  

---

### **2️⃣ Installing & Setting Up Jenkins**  
## **✅ Installing Jenkins (Linux, Windows, Docker)**  

### **1️⃣ Installing Jenkins on Linux (Ubuntu/Debian-based Systems)**  
#### **Step 1: Update System Packages**
```bash
sudo apt update && sudo apt upgrade -y
```
#### **Step 2: Install Java (Jenkins Requires Java)**
```bash
sudo apt install openjdk-11-jdk -y
```
Verify Java installation:
```bash
java -version
```
#### **Step 3: Add Jenkins Repository & Install Jenkins**
```bash
wget -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins -y
```
#### **Step 4: Start and Enable Jenkins**
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```
#### **Step 5: Access Jenkins UI**
- Open browser and go to `http://localhost:8080`
- Retrieve initial admin password:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
- Follow UI setup to install recommended plugins and create an admin user.

---

### **2️⃣ Installing Jenkins on Windows**
#### **Step 1: Download Jenkins**
- Download the Jenkins `.msi` installer from [Jenkins Official Site](https://www.jenkins.io/download/).

#### **Step 2: Install Jenkins**
- Run the `.msi` file and follow the setup wizard.
- Choose an installation path (default: `C:\Program Files\Jenkins`).

#### **Step 3: Start Jenkins Service**
- Open **Services** (`services.msc`) → Locate **Jenkins** → Start the service.

#### **Step 4: Access Jenkins UI**
- Open a browser and visit:  
  ```
  http://localhost:8080
  ```
- Retrieve initial admin password from:
  ```
  C:\Program Files\Jenkins\secrets\initialAdminPassword
  ```

---

### **3️⃣ Installing Jenkins on Docker**
#### **Step 1: Pull Jenkins Docker Image**
```bash
docker pull jenkins/jenkins:lts
```
#### **Step 2: Run Jenkins Container**
```bash
docker run -d -p 8080:8080 -p 50000:50000 --name jenkins -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
```
#### **Step 3: Access Jenkins UI**
- Open `http://localhost:8080`  
- Retrieve admin password:
```bash
docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

---

## **✅ Running Jenkins as a Service**  
### **On Linux (Systemd Service)**
Jenkins is installed as a service by default. To manage it:  
```bash
# Start Jenkins
sudo systemctl start jenkins

# Enable Jenkins to start on boot
sudo systemctl enable jenkins

# Check Jenkins status
sudo systemctl status jenkins

# Restart Jenkins
sudo systemctl restart jenkins
```

### **On Windows (Services)**
- Open **Run (`Win + R`)** → Type `services.msc`
- Locate **Jenkins** service
- Start, Stop, or Restart Jenkins from the GUI.

### **On Docker**
- Stop Jenkins:
```bash
docker stop jenkins
```
- Start Jenkins:
```bash
docker start jenkins
```

---

## **✅ Understanding Jenkins Home Directory & Configurations**  
The **Jenkins Home Directory** stores all Jenkins configurations, jobs, and user data.

### **📌 Jenkins Home Path:**
| Platform  | Path |
|-----------|------------------------|
| Linux     | `/var/lib/jenkins/` |
| Windows   | `C:\Program Files\Jenkins\` |
| Docker    | `/var/jenkins_home/` |

### **📌 Key Files & Folders in Jenkins Home**
| File/Folder       | Description |
|-------------------|-------------|
| `config.xml`      | Main Jenkins configuration file. |
| `jobs/`          | Stores job configurations. |
| `plugins/`       | Stores installed plugins. |
| `secrets/`       | Stores admin password and credentials. |
| `users/`         | Stores user account data. |
| `workspace/`     | Stores job build workspaces. |
| `logs/`          | Stores logs of Jenkins activities. |

#### **Modify Jenkins Configuration**
- Edit the `config.xml` file and restart Jenkins:
```bash
sudo nano /var/lib/jenkins/config.xml
sudo systemctl restart jenkins
```

---

## **✅ Managing Plugins (Jenkins Plugin System)**  

### **📌 Installing Plugins from UI**
1️⃣ Go to **Manage Jenkins** → **Manage Plugins**  
2️⃣ Search for the required plugin under the **Available** tab.  
3️⃣ Click **Install without restart** or **Install and Restart**.

### **📌 Installing Plugins from CLI**
```bash
sudo jenkins-cli install-plugin plugin-name
```
Example:
```bash
sudo jenkins-cli install-plugin kubernetes
```

### **📌 Must-Have Plugins for DevOps**
| Plugin Name         | Purpose |
|---------------------|---------|
| **Pipeline**       | Enables Jenkinsfile support for CI/CD pipelines. |
| **Git**           | Integrates Jenkins with GitHub, GitLab, Bitbucket. |
| **GitHub**        | Supports GitHub webhooks. |
| **Docker Pipeline** | Enables Docker integration for CI/CD. |
| **Kubernetes**    | Deploy Jenkins agents in Kubernetes. |
| **Credentials Binding** | Securely manage secrets in pipelines. |
| **Blue Ocean**    | Provides a modern Jenkins UI for pipelines. |
| **SonarQube Scanner** | Integrates with SonarQube for code analysis. |

### **📌 Updating Plugins**
1. Go to **Manage Jenkins** → **Manage Plugins**  
2. Open **Updates** tab and update the required plugins.  

### **📌 Removing Plugins**
1. Go to **Manage Jenkins** → **Manage Plugins** → **Installed**  
2. Select the plugin to remove and click **Uninstall**.  
3. Restart Jenkins for changes to take effect.

---

## **🎯 Summary**
✅ **Installing Jenkins** – Supported on Linux, Windows, and Docker.  
✅ **Running Jenkins as a Service** – Managed using `systemctl` or Windows services.  
✅ **Jenkins Home Directory** – Stores jobs, plugins, configs, and logs.  
✅ **Managing Plugins** – Install, update, or remove via UI or CLI.  

---

### **3️⃣ Jenkins UI & Core Components**  
## ✅ **Understanding Jenkins Dashboard**  

### **Jenkins Dashboard Overview**  
The **Jenkins Dashboard** is the main interface where you manage Jenkins jobs, configure settings, and monitor builds.

### **Key Components of Jenkins Dashboard**  

1️⃣ **New Item** – Create a new job (Freestyle, Pipeline, Multi-branch, etc.).  
2️⃣ **Build Queue** – Shows pending builds waiting for execution.  
3️⃣ **Build Executor Status** – Displays active Jenkins nodes/executors running builds.  
4️⃣ **Manage Jenkins** – Configure Jenkins, plugins, credentials, nodes, and security.  
5️⃣ **Credentials** – Manage secrets (GitHub tokens, AWS keys, SSH keys).  
6️⃣ **People** – View Jenkins users and permissions.  
7️⃣ **My Views** – Customize and filter job views for better management.  
8️⃣ **Job List** – Shows all Jenkins jobs with their status (Success, Failed, In Progress).  
9️⃣ **Console Output** – View real-time logs of running or completed builds.  

### **Jenkins Dashboard Navigation**
- **Access Jenkins:** `http://localhost:8080`
- **Login with Admin Credentials**
- **Explore Options**: Click on a job → Check **Build History**, **Console Output**, and **Configure** options.

---

## ✅ **Creating & Managing Jobs (Freestyle, Pipeline)**  

### **1️⃣ Creating a Freestyle Job** (Simple Job)
1. Click **New Item**  
2. Enter a job name (e.g., `MyFreestyleJob`)  
3. Select **Freestyle Project** → Click **OK**  
4. Configure the following:
   - **Source Code Management (SCM)** – Connect to GitHub/GitLab.  
   - **Build Triggers** – Define when the job should run.  
   - **Build Steps** – Execute shell scripts, compile code, or run tests.  
   - **Post-Build Actions** – Archive artifacts, send email notifications, etc.  
5. Click **Save** → **Build Now**  

### **2️⃣ Creating a Pipeline Job** (CI/CD Automation)
1. Click **New Item** → Enter job name (e.g., `MyPipelineJob`)  
2. Select **Pipeline** → Click **OK**  
3. Scroll to **Pipeline Definition** section  
4. Choose one:
   - **Pipeline Script** – Write a pipeline script manually.
   - **Pipeline from SCM** – Fetch Jenkinsfile from a Git repository.  
5. Example **Pipeline Script**:
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }
}
```
6. Click **Save** → **Build Now**  

### **3️⃣ Managing Jobs**
- Click on a job → **Configure** to edit settings.  
- Click **Build Now** to trigger a manual build.  
- Click **Delete Project** to remove a job.  
- Monitor builds under **Build History**.  

---

## ✅ **Jenkins Build Triggers** (SCM, Webhook, Polling, Manual, API)  

### **1️⃣ Manual Trigger** (Build Now)
- Open a job → Click **Build Now**  
- Useful for **on-demand execution** of jobs.  

### **2️⃣ Poll SCM (Scheduled Git Polling)**
- Jenkins checks the **Git repository** periodically for changes.  
- Configure it under **Build Triggers**:
  ```
  H/5 * * * *  (Runs every 5 minutes)
  ```
- Not efficient, as Jenkins keeps checking even if no changes exist.  

### **3️⃣ Webhooks (Push-Based Trigger)**
- Best for real-time CI/CD execution when a commit is pushed.  
- Steps:
  1. Go to GitHub Repository → **Settings** → **Webhooks**  
  2. Add **Jenkins URL**:
     ```
     http://<jenkins-server>:8080/github-webhook/
     ```
  3. Select **Just the push event** → Save  
  4. Enable **"GitHub hook trigger for GITScm polling"** in Jenkins job settings.  

### **4️⃣ Build via API**
- Jenkins provides an API to trigger builds remotely.  
- Enable **Trigger builds remotely** under **Build Triggers** and set a token.  
- Use **cURL command** to trigger:
  ```bash
  curl -X POST http://<jenkins-server>:8080/job/MyJob/build?token=my-secret-token
  ```

---

## ✅ **Jenkins Build Executors & Nodes**  

### **1️⃣ What is a Jenkins Build Executor?**  
A **build executor** is a thread that runs builds inside a Jenkins node.  
- By default, the **Jenkins master node** has **one executor**.  
- More executors can be added for parallel builds.

### **2️⃣ Jenkins Master-Agent (Distributed Architecture)**
Jenkins supports a **distributed build system** with:
- **Master Node** – Controls job execution, UI, and configurations.
- **Agent Node (Slave Node)** – Executes build tasks assigned by the master.

### **3️⃣ Adding a New Jenkins Agent (Slave)**
1. Go to **Manage Jenkins** → **Manage Nodes and Clouds**  
2. Click **New Node** → Enter a name (e.g., `agent-node-1`)  
3. Select **Permanent Agent** → Click **OK**  
4. Set **Number of Executors** (e.g., `2` for parallel builds)  
5. Configure **Launch method** (SSH, JNLP, or WebSocket)  
6. Click **Save & Launch**  

### **4️⃣ Running Jobs on Specific Nodes**
- Add a label to the node (e.g., `linux-agent`)  
- Modify Jenkinsfile to use the node:
```groovy
pipeline {
    agent {
        label 'linux-agent'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building on Linux Agent Node'
            }
        }
    }
}
```

---

## 🎯 **Summary**
✅ **Jenkins Dashboard** – Main interface to manage jobs, triggers, and builds.  
✅ **Creating Jobs** – Freestyle (basic) vs. Pipeline (advanced CI/CD automation).  
✅ **Build Triggers** – Manual, Poll SCM, Webhooks, API-based.  
✅ **Build Executors & Nodes** – Master-agent architecture, adding agents for scalability.   

---

### **4️⃣ Jenkins Pipelines (Declarative & Scripted)**  
## ✅ **What is a Jenkins Pipeline?**  

A **Jenkins Pipeline** is a set of steps that define the entire **CI/CD process** in Jenkins. It automates **building, testing, and deploying** applications using a **Jenkinsfile** (pipeline script).  

### **Why Use Jenkins Pipelines?**  
✅ **Automation** – No need to configure builds manually.  
✅ **Version Control** – Pipeline code is stored in Git (Jenkinsfile).  
✅ **Scalability** – Supports parallel execution and multi-stage builds.  
✅ **Flexibility** – Can be customized for any project (Docker, Kubernetes, AWS, etc.).  

---

## ✅ **Creating a Simple Declarative Pipeline (Jenkinsfile)**  

A **Jenkinsfile** is a text file that defines a pipeline in **Groovy syntax**.  

### **Step 1: Create a Pipeline Job**  
1. Open **Jenkins Dashboard** → Click **New Item**  
2. Enter a job name → Select **Pipeline** → Click **OK**  
3. Scroll to the **Pipeline Definition** section  
4. Choose **Pipeline Script** → Paste the below script  

### **Simple Declarative Pipeline Example**
```groovy
pipeline {
    agent any  // Runs on any available node
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }
}
```
5. Click **Save** → Click **Build Now**  

---

## ✅ **Scripted Pipeline vs. Declarative Pipeline**  

| Feature               | Declarative Pipeline | Scripted Pipeline |
|----------------------|--------------------|-------------------|
| Syntax Complexity   | Simple (Structured) | Complex (Flexible) |
| Error Handling      | Built-in support   | Manual handling needed |
| Readability        | Easier to read & maintain | More coding skills required |
| Recommended for    | Beginners & CI/CD standardization | Advanced custom workflows |

✅ **Example of a Scripted Pipeline**  
```groovy
node {
    stage('Build') {
        echo 'Building the application...'
    }
    stage('Test') {
        echo 'Running tests...'
    }
    stage('Deploy') {
        echo 'Deploying the application...'
    }
}
```
- **Use Scripted Pipelines** when you need **complex loops, conditions, or advanced scripting.**  
- **Use Declarative Pipelines** for **simpler and structured workflows.**  

---

## ✅ **Stages & Steps in Jenkinsfile**  

A **Jenkins Pipeline** consists of:  
✅ **Stages** – Logical sections (e.g., Build, Test, Deploy)  
✅ **Steps** – Commands inside a stage (e.g., `echo`, `sh`, `git`)  

### **Example: Pipeline with Git Checkout & Shell Script**
```groovy
pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/user/repository.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
```
- Uses `git` to pull code  
- Uses `sh` to run shell commands  

---

## ✅ **Pipeline Parameters for Dynamic Builds**  

### **Why Use Parameters?**  
- Allow user input before running a job  
- Useful for **custom environments, versions, or feature flags**  

### **Example: Adding User Input in Pipeline**
```groovy
pipeline {
    agent any
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'Git branch to build')
        choice(name: 'DEPLOY_ENV', choices: ['dev', 'staging', 'prod'], description: 'Deployment environment')
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: "${params.BRANCH_NAME}", url: 'https://github.com/user/repository.git'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying to ${params.DEPLOY_ENV} environment..."
            }
        }
    }
}
```
💡 **Before running, Jenkins asks for:**  
- **BRANCH_NAME** (e.g., `feature-xyz`)  
- **DEPLOY_ENV** (Choose `dev`, `staging`, or `prod`)  

---

## ✅ **Handling Build Failures & Notifications**  

### **1️⃣ Error Handling in Jenkins Pipelines**
Use `try-catch` or `post` sections to handle failures gracefully.

#### **Example: Try-Catch for Error Handling**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    try {
                        sh 'mvn clean package'
                    } catch (Exception e) {
                        echo "Build Failed: ${e.getMessage()}"
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
        }
    }
}
```

### **2️⃣ Sending Email or Slack Notifications**
Jenkins supports **email and Slack alerts** when a build succeeds or fails.

#### **Example: Email Notification on Failure**
```groovy
pipeline {
    agent any
    post {
        failure {
            mail to: 'team@example.com',
                 subject: "Build Failed: ${currentBuild.fullDisplayName}",
                 body: "Check the logs at ${env.BUILD_URL}"
        }
    }
}
```

#### **Example: Slack Notification**
- Install the **Slack Notification Plugin**  
- Configure Slack Webhook  
```groovy
pipeline {
    agent any
    post {
        success {
            slackSend channel: '#devops',
                      message: "Build Succeeded: ${env.BUILD_URL}"
        }
        failure {
            slackSend channel: '#devops',
                      message: "Build Failed: ${env.BUILD_URL}"
        }
    }
}
```

---

## 🎯 **Summary**  
✅ **Jenkins Pipeline** – Automates CI/CD workflows using Jenkinsfile.  
✅ **Declarative vs. Scripted Pipelines** – Use **Declarative** for structured workflows, **Scripted** for complex logic.  
✅ **Stages & Steps** – Define pipeline execution flow.  
✅ **Pipeline Parameters** – Accept user inputs dynamically.  
✅ **Handling Failures & Notifications** – Use error handling, email, and Slack alerts.  

---

### **5️⃣ Jenkinsfile & Groovy Scripting**  
## ✅ **Writing Jenkinsfile for CI/CD Automation**  

A **Jenkinsfile** is a script written in **Groovy** that defines a Jenkins pipeline to automate **CI/CD workflows**.  

### **Why Use a Jenkinsfile?**  
✅ **Code as Configuration** – Stored in version control (Git).  
✅ **Repeatability** – Ensures consistent builds across environments.  
✅ **Automation** – No need for manual build configuration.  

### **Basic CI/CD Pipeline Example**
```groovy
pipeline {
    agent any  // Runs on any available node
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/user/repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
```
📌 **Pipeline Breakdown:**  
- **Checkout**: Clones repository from Git.  
- **Build**: Compiles the application.  
- **Test**: Runs unit tests.  
- **Deploy**: Executes the deployment script.  

---

## ✅ **Understanding Groovy Syntax for Jenkins**  

Jenkins pipelines are written in **Groovy DSL**, which provides:  
✅ **Declarative Pipeline Support** (structured syntax)  
✅ **Scripted Pipeline Support** (advanced scripting)  
✅ **Groovy Features** (loops, conditions, functions)  

### **Key Groovy Concepts in Jenkins**
#### **1️⃣ Variables**
```groovy
def appVersion = "1.0.0"
echo "Deploying version ${appVersion}"
```

#### **2️⃣ Conditionals**
```groovy
if (env.BRANCH_NAME == 'main') {
    echo "Deploying to production"
} else {
    echo "Deploying to staging"
}
```

#### **3️⃣ Loops**
```groovy
for (int i = 1; i <= 3; i++) {
    echo "Retrying build attempt ${i}"
}
```

#### **4️⃣ Functions in Groovy**
```groovy
def greet(String name) {
    echo "Hello, ${name}!"
}
greet('DevOps Engineer')
```

---

## ✅ **Using Variables & Environment Variables**  

Jenkins allows the use of:  
✅ **Pipeline Variables** (User-defined values)  
✅ **Environment Variables** (System-defined values)  

### **1️⃣ Using Variables in Jenkinsfile**
```groovy
pipeline {
    agent any
    environment {
        APP_ENV = 'staging'
        BUILD_VERSION = '1.0.0'
    }
    stages {
        stage('Print Variables') {
            steps {
                echo "Environment: ${APP_ENV}"
                echo "Build Version: ${BUILD_VERSION}"
            }
        }
    }
}
```

### **2️⃣ Using Jenkins Environment Variables**
| Variable | Description |
|----------|-------------|
| `env.BUILD_NUMBER` | Current build number |
| `env.JOB_NAME` | Name of the running job |
| `env.BRANCH_NAME` | Git branch name |
| `env.BUILD_URL` | URL of the build |
| `env.WORKSPACE` | Workspace directory path |

```groovy
pipeline {
    agent any
    stages {
        stage('Print Jenkins Variables') {
            steps {
                echo "Job Name: ${env.JOB_NAME}"
                echo "Build Number: ${env.BUILD_NUMBER}"
                echo "Workspace: ${env.WORKSPACE}"
            }
        }
    }
}
```

---

## ✅ **Running Shell Scripts inside Jenkinsfile (`sh` command)**  

Jenkins supports running shell scripts using `sh` for Linux/macOS or `bat` for Windows.

### **1️⃣ Running Simple Shell Commands**
```groovy
pipeline {
    agent any
    stages {
        stage('Run Shell Script') {
            steps {
                sh 'echo "Hello, Jenkins!"'
                sh 'ls -l'
            }
        }
    }
}
```

### **2️⃣ Running a Shell Script File**
```groovy
pipeline {
    agent any
    stages {
        stage('Execute Script') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
```
📌 **Ensure `deploy.sh` has execution permissions:**
```sh
chmod +x deploy.sh
```

### **3️⃣ Capturing Shell Script Output**
```groovy
pipeline {
    agent any
    stages {
        stage('Capture Output') {
            steps {
                script {
                    def output = sh(script: 'date', returnStdout: true).trim()
                    echo "Current Date & Time: ${output}"
                }
            }
        }
    }
}
```

---

## 🎯 **Summary**  

✅ **Jenkinsfile** automates CI/CD workflows using Groovy syntax.  
✅ **Groovy Basics** – Variables, loops, conditionals, and functions are used in Jenkins pipelines.  
✅ **Environment Variables** – Store dynamic values like `env.BRANCH_NAME` and `env.BUILD_NUMBER`.  
✅ **Running Shell Scripts** – Use `sh` for executing commands and scripts in Linux-based builds.  

---

### **6️⃣ Jenkins & Source Code Management (SCM)**  
# ✅ **Integrating Jenkins with GitHub, GitLab, and Bitbucket**  

Jenkins can integrate with version control systems like **GitHub, GitLab, and Bitbucket** to automate builds whenever code is pushed.  

---

## ✅ **1. Integrating Jenkins with GitHub, GitLab, and Bitbucket**  

### 🔹 **Step 1: Install Git Plugin in Jenkins**  
1️⃣ Go to **Jenkins Dashboard** → **Manage Jenkins** → **Manage Plugins**  
2️⃣ Search for **"Git Plugin"** and install it  
3️⃣ Restart Jenkins after installation  

### 🔹 **Step 2: Configure Global Git Settings**  
1️⃣ Navigate to **Manage Jenkins** → **Global Tool Configuration**  
2️⃣ Under **Git**, specify the Git executable path (if not auto-detected)  
3️⃣ Click **Apply & Save**  

### 🔹 **Step 3: Add GitHub, GitLab, or Bitbucket Credentials**  
1️⃣ Go to **Manage Jenkins** → **Manage Credentials**  
2️⃣ Click **(global)** → **Add Credentials**  
3️⃣ Choose **SSH Username with Private Key** or **Username & Password**  
4️⃣ Enter **GitHub/GitLab/Bitbucket credentials**  
5️⃣ Click **Save**  

---

## ✅ **2. Setting Up Webhooks for Automatic Builds**  

Webhooks allow Jenkins to trigger builds automatically when changes are pushed to a repository.  

### 🔹 **For GitHub Webhook Configuration**  
1️⃣ In **GitHub**, go to your repository → **Settings** → **Webhooks**  
2️⃣ Click **"Add Webhook"**  
3️⃣ Enter the **Jenkins URL** (e.g., `http://<jenkins-server>:8080/github-webhook/`)  
4️⃣ Select **"Push event"** as the trigger  
5️⃣ Click **"Add Webhook"**  

### 🔹 **For GitLab Webhook Configuration**  
1️⃣ Go to **GitLab** → **Settings** → **Integrations**  
2️⃣ Enter **Jenkins Webhook URL**: `http://<jenkins-server>:8080/project/<job-name>`  
3️⃣ Select **"Push Events"** and **"Merge Request Events"**  
4️⃣ Click **Add Webhook**  

### 🔹 **For Bitbucket Webhook Configuration**  
1️⃣ In **Bitbucket**, go to **Repository settings** → **Webhooks**  
2️⃣ Click **"Add Webhook"**  
3️⃣ Enter **Jenkins Webhook URL**: `http://<jenkins-server>:8080/bitbucket-hook/`  
4️⃣ Enable **"Repository Push"** events  
5️⃣ Click **Save**  

---

## ✅ **3. Using Git Credentials in Jenkins**  

### 🔹 **Method 1: Using SSH Keys (Recommended)**  
1️⃣ Generate an SSH key (if not already created)  
   ```sh
   ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
   ```
2️⃣ Add the public key (`id_rsa.pub`) to **GitHub/GitLab/Bitbucket** under **SSH keys**  
3️⃣ Add the **private key** to **Jenkins Credentials**  

### 🔹 **Method 2: Using Personal Access Token (GitHub & GitLab)**  
1️⃣ Generate a **Personal Access Token** in **GitHub/GitLab**  
2️⃣ Add the token in **Jenkins Credentials**  
3️⃣ Use the token instead of a password in the Git repository URL  

---

## ✅ **4. Cloning & Checking Out Code from Git Repositories**  

Once Git is configured, Jenkins can **clone and checkout** repositories.  

### **Declarative Pipeline Example**
```groovy
pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'git-credentials-id', url: 'git@github.com:user/repo.git'
            }
        }
    }
}
```
📌 **Breakdown:**  
✔ **`branch: 'main'`** – Specifies the branch to clone  
✔ **`credentialsId: 'git-credentials-id'`** – Uses saved Git credentials  
✔ **`url: 'git@github.com:user/repo.git'`** – Clones the repository  

---

## ✅ **Summary**  

✅ **Jenkins can integrate with GitHub, GitLab, and Bitbucket** to trigger builds  
✅ **Webhooks automate builds** when code is pushed  
✅ **Git credentials (SSH, PAT) allow secure authentication**  
✅ **Jenkinsfile can define pipelines** that clone and build code  

---

### **7️⃣ Jenkins CI/CD Pipeline**  
# ✅ **Jenkins CI/CD Pipeline: Automating Builds, Tests, and Deployment**

Jenkins helps DevOps engineers **automate Continuous Integration (CI) and Continuous Deployment (CD)** by building, testing, and deploying applications automatically.

---

## ✅ **1. Setting Up Continuous Integration (CI)**  

### 🔹 **What is CI?**  
**Continuous Integration (CI)** automates the process of merging code changes frequently into a shared repository and running automated tests to detect issues early.

### 🔹 **Steps to Set Up CI in Jenkins**  
1️⃣ **Install Required Plugins:**  
   - **Git Plugin** (for version control)  
   - **Pipeline Plugin** (for writing Jenkinsfile-based pipelines)  
   - **JUnit Plugin** (for test reporting)  

2️⃣ **Create a New Pipeline Job:**  
   - Go to **Jenkins Dashboard** → **New Item**  
   - Select **Pipeline** → Click **OK**  

3️⃣ **Define a CI Pipeline in Jenkinsfile:**  
   - The pipeline should include **cloning the repository, building the code, running tests, and storing artifacts**.

---

## ✅ **2. Automating Builds, Tests, and Deployment**  

### 🔹 **Jenkinsfile Example for CI**  
```groovy
pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'git-credentials-id', url: 'git@github.com:user/repo.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'  // Example for Java projects
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'  // Runs unit tests
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'  // Publish test results
                }
            }
        }
        stage('Package') {
            steps {
                sh 'docker build -t my-app:latest .'  // Package app into Docker image
            }
        }
    }
}
```
📌 **Breakdown:**  
✔ **Clones the repository**  
✔ **Builds the application**  
✔ **Runs automated tests**  
✔ **Packages the application into a Docker image**  

---

## ✅ **3. Running Unit Tests, Integration Tests & Security Scans**  

### 🔹 **Unit Testing in Jenkins (JUnit Example)**  
- If using **JUnit** for testing, Jenkins can **display test results**.  
- Use `junit 'target/surefire-reports/*.xml'` to publish results.

### 🔹 **Integration Testing in Jenkins**  
- **Selenium** for UI testing  
- **Postman/Newman** for API testing  
- **Mock services** for backend testing

### 🔹 **Security Scans in Jenkins**  
Jenkins can integrate with **security testing tools** like:  
- **SonarQube** (Code quality & security analysis)  
- **Trivy** (Container vulnerability scanning)  
- **Snyk** (Dependency security scanning)

---

## ✅ **4. Deploying Applications to AWS, Kubernetes, Docker Hub**  

### 🔹 **Deploying to Docker Hub**  
To **push a Docker image** to Docker Hub:  
```groovy
stage('Push to Docker Hub') {
    steps {
        withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
            sh 'docker tag my-app:latest my-dockerhub-username/my-app:latest'
            sh 'docker push my-dockerhub-username/my-app:latest'
        }
    }
}
```

### 🔹 **Deploying to Kubernetes**  
To deploy an application to **Kubernetes**:  
```groovy
stage('Deploy to Kubernetes') {
    steps {
        sh 'kubectl apply -f k8s/deployment.yaml'
    }
}
```
- Make sure **kubectl** is configured on the Jenkins server.

### 🔹 **Deploying to AWS EC2**  
To deploy to **AWS EC2**:  
```groovy
stage('Deploy to AWS EC2') {
    steps {
        sshagent(['aws-ec2-credentials']) {
            sh 'scp target/app.jar ec2-user@your-ec2-instance:/opt/app/'
            sh 'ssh ec2-user@your-ec2-instance "sudo systemctl restart my-app"'
        }
    }
}
```

### 🔹 **Deploying to AWS S3 (for Static Websites)**  
```groovy
stage('Deploy to AWS S3') {
    steps {
        sh 'aws s3 sync ./build s3://my-bucket-name --delete'
    }
}
```

---

## ✅ **Summary**  

✅ **Jenkins automates CI/CD by integrating with Git, running tests, and deploying applications**  
✅ **Unit tests, integration tests, and security scans ensure high-quality software**  
✅ **Jenkins can deploy applications to Docker Hub, Kubernetes, and AWS**  

---

### **8️⃣ Jenkins Agents & Distributed Builds**  
# ✅ **Jenkins Agents (Slaves) and Master-Slave Architecture**

Jenkins follows a **Master-Agent (Master-Slave) architecture**, where the **master node** orchestrates jobs, and **agent nodes** execute the jobs. This setup helps in **scalability and parallel execution** of builds.

---

## ✅ **1. What are Jenkins Agents (Slaves)?**  

### 🔹 **Definition**  
A **Jenkins Agent (Slave)** is a remote machine that runs Jenkins jobs. The **Master (Controller) Node** delegates jobs to agents to distribute workloads efficiently.

### 🔹 **Why Use Agents?**  
✅ Run multiple builds in parallel  
✅ Offload resource-heavy tasks from the master  
✅ Use different operating systems for testing  
✅ Scale Jenkins dynamically  

---

## ✅ **2. Jenkins Master-Slave Architecture**  

### 🔹 **Components in Jenkins Master-Agent Setup**  
1️⃣ **Master Node (Controller)**  
   - Manages Jenkins configurations, UI, plugins, and job scheduling  
   - Assigns tasks to agent nodes  

2️⃣ **Agent Nodes (Slaves)**  
   - Executes Jenkins jobs based on Master’s instructions  
   - Can be Linux, Windows, Mac, or even Docker-based  

### 🔹 **How Agents Communicate with Master?**  
✔ **SSH (Linux)** – Agents connect via SSH for job execution  
✔ **JNLP (Java Network Launch Protocol)** – Used for cloud-based agents  
✔ **Docker Containers** – Dynamic agents for isolated builds  

---

## ✅ **3. Setting Up Jenkins Master-Slave Architecture**  

### 🔹 **Step 1: Enable Agent Nodes in Jenkins**  
1. **Go to Jenkins Dashboard** → Manage Jenkins → Configure Global Security  
2. Enable **"TCP port for inbound agents"**  
3. Choose **Fixed port or Random port**  

### 🔹 **Step 2: Add a New Agent Node**  
1. Go to **Jenkins Dashboard** → Manage Jenkins → Manage Nodes and Clouds  
2. Click **New Node** → Enter a name (e.g., `Linux-Agent`)  
3. Choose **Permanent Agent**  
4. Configure:
   - **# of Executors:** Number of parallel jobs it can run  
   - **Remote Root Directory:** e.g., `/home/jenkins`  
   - **Labels:** Used to assign jobs (e.g., `linux`, `docker`, `java`)  

### 🔹 **Step 3: Launch Agent on a Remote Machine**  
#### **For Linux Agent (Using SSH)**
Run on the agent machine:  
```bash
sudo useradd -m jenkins
mkdir /home/jenkins
chown -R jenkins:jenkins /home/jenkins
```
- **Copy the Jenkins SSH Key** from the master to the agent  
- Ensure **Java is installed** (`java -version`)  

#### **For Windows Agent (Using JNLP)**
1. Download the agent `.jnlp` file from **Manage Nodes**  
2. Run the agent:  
   ```cmd
   java -jar agent.jar -jnlpUrl <JENKINS_MASTER_URL>/computer/Linux-Agent/slave-agent.jnlp
   ```

---

## ✅ **4. Using Docker Agents for Jenkins Pipelines**  

### 🔹 **Why Use Docker as an Agent?**  
✅ Provides isolated environments for builds  
✅ Eliminates dependency conflicts  
✅ Ensures consistency across development teams  

### 🔹 **Running Jenkins Agents as Docker Containers**  
1. Pull the Jenkins agent image:  
   ```bash
   docker pull jenkins/inbound-agent
   ```
2. Start an agent container:  
   ```bash
   docker run -d --rm --name jenkins-agent \
     -e JENKINS_URL="http://your-jenkins-master:8080" \
     -e JENKINS_SECRET="your-agent-secret" \
     -e JENKINS_AGENT_NAME="docker-agent" \
     jenkins/inbound-agent
   ```
3. The agent will automatically connect to Jenkins and execute jobs.

---

## ✅ **5. Configuring Self-Hosted Runners in Jenkins**  

A **self-hosted runner** is an agent running on **your own infrastructure** instead of Jenkins-managed cloud agents.

### 🔹 **Steps to Set Up a Self-Hosted Runner**  
1️⃣ **Install Java on the Runner Machine**  
```bash
sudo apt update && sudo apt install openjdk-11-jdk -y
```
2️⃣ **Create a Jenkins User on the Runner Machine**  
```bash
sudo useradd -m jenkins
sudo passwd jenkins
```
3️⃣ **Add the Runner to Jenkins**  
- Navigate to **Manage Nodes and Clouds**  
- Click **New Node** → Configure Agent Details  

4️⃣ **Launch the Runner**  
```bash
java -jar agent.jar -jnlpUrl <JENKINS_MASTER_URL>/computer/Runner/slave-agent.jnlp
```

---

## ✅ **Summary**  
✔ **Jenkins Master-Agent model distributes workloads for scalability**  
✔ **Agents can be set up on Linux, Windows, or Docker**  
✔ **Docker agents provide a lightweight and scalable CI/CD solution**  
✔ **Self-hosted runners allow running jobs on custom infrastructure**  

---

### **9️⃣ Jenkins Plugins & Extensions**  
# ✅ **Must-Have Plugins in Jenkins**

Jenkins plugins enhance the functionality of Jenkins by adding integrations, automation features, and support for various tools. Below are some of the **must-have plugins** for DevOps engineers.

---

## 🔹 **1. Essential Plugins for CI/CD**
### ✅ **Pipeline Plugin**  
- Enables **Jenkins Pipelines** (Declarative & Scripted)  
- Required for writing `Jenkinsfile`  
- **Installation:** Comes pre-installed with Jenkins  

### ✅ **Git Plugin**  
- Integrates Jenkins with **GitHub, GitLab, and Bitbucket**  
- Supports cloning, fetching, and pushing repositories  
- **Installation:** Available in **Manage Plugins**  

### ✅ **Blue Ocean**  
- Provides a **modern UI** for Jenkins Pipelines  
- Helps visualize builds, stages, and failures  
- **Installation Command:**  
  ```bash
  jenkins-plugin-cli --plugins blueocean
  ```

### ✅ **SonarQube Scanner**  
- Performs **code quality analysis** and reports issues  
- Used for **static code analysis & security scans**  
- **Integration:** Connects with SonarQube Server  

### ✅ **Kubernetes Plugin**  
- Enables Jenkins to use **Kubernetes Pods as Agents**  
- Useful for **scalable, containerized CI/CD**  
- **Installation:** Available via **Manage Plugins**  

---

## 🔹 **2. Installing & Managing Plugins in Jenkins**
### ✅ **Using the Jenkins UI**  
1. Go to **Jenkins Dashboard** → Manage Jenkins → Manage Plugins  
2. Search for the plugin in the **Available** tab  
3. Click **Install without restart**  

### ✅ **Using Jenkins CLI**
Run the following command inside the Jenkins container or system:  
```bash
jenkins-plugin-cli --plugins git pipeline blueocean sonar sonar-coverage
```

### ✅ **Using Jenkins Plugin Manager (Jenkinsfile)**
You can define plugins in a `Jenkinsfile`:
```groovy
plugins {
    id 'git'
    id 'pipeline'
    id 'blueocean'
    id 'sonarqube'
}
```

---

## 🔹 **3. Extending Jenkins with Custom Plugins**
Jenkins allows you to **create custom plugins** to extend its functionality.

### ✅ **How to Develop a Custom Jenkins Plugin?**
1️⃣ Install the Jenkins Plugin Development Kit:  
```bash
mvn hpi:create -DgroupId=com.mycompany.jenkins -DartifactId=my-plugin
```
2️⃣ Navigate to the Plugin Directory:  
```bash
cd my-plugin
```
3️⃣ Build the Plugin:  
```bash
mvn package
```
4️⃣ Install the Plugin in Jenkins:  
- Copy the generated `.hpi` file to `JENKINS_HOME/plugins/`  
- Restart Jenkins  

---

## ✅ **Summary**
✔ **Jenkins plugins extend functionality for SCM, CI/CD, and security**  
✔ **Essential plugins:** Pipeline, Git, Blue Ocean, SonarQube, Kubernetes  
✔ **Plugins can be installed via UI, CLI, or Jenkinsfile**  
✔ **Custom plugins can be developed using Java and Maven**  

---

### **🔟 Jenkins Security & User Management**  
# 🔒 **Jenkins Security & Access Control Guide**  

Jenkins is a powerful automation tool, but securing it is crucial to prevent unauthorized access and maintain CI/CD integrity. Below are key security concepts every DevOps engineer should know:

---

## ✅ **1. Creating Users & Roles in Jenkins**  
Jenkins allows administrators to create multiple users and assign different roles based on their responsibilities.

### 🔹 **How to Create Users in Jenkins?**  
1️⃣ **Go to**: Jenkins Dashboard → Manage Jenkins → Manage Users  
2️⃣ Click **Create User**  
3️⃣ Fill in the details (**Username, Password, Full Name, Email**)  
4️⃣ Click **Create User**  

---

## ✅ **2. Configuring Role-Based Access Control (RBAC)**  
By default, Jenkins allows **full access** to all users. To **restrict permissions**, use the **Role-Based Access Control (RBAC) Plugin**.

### 🔹 **Steps to Enable RBAC in Jenkins**  
1️⃣ Install **Role-Based Authorization Strategy Plugin**  
2️⃣ Navigate to: **Manage Jenkins → Configure Global Security**  
3️⃣ Select **Role-Based Strategy** under "Authorization"  
4️⃣ Go to **Manage Jenkins → Manage and Assign Roles**  
5️⃣ Define roles with **specific permissions**  
6️⃣ Assign users to **appropriate roles**  

### 🔹 **Common Roles in Jenkins**  
| Role | Permissions |
|------|------------|
| **Admin** | Full control over Jenkins |
| **Developer** | Can run jobs but cannot modify configurations |
| **Tester** | Can view and trigger test jobs |
| **Viewer** | Read-only access |

---

## ✅ **3. Using Jenkins Credentials Store Securely**  
Jenkins **stores passwords, SSH keys, API tokens, and secret text** in the **Credentials Store**.

### 🔹 **How to Add Credentials in Jenkins?**  
1️⃣ **Go to**: Manage Jenkins → Manage Credentials  
2️⃣ Select the appropriate scope (**Global, System, Folder, Job**)  
3️⃣ Click **Add Credentials**  
4️⃣ Choose **Type (Username/Password, Secret File, AWS Keys, SSH Key, etc.)**  
5️⃣ Save and **use the credential ID** in pipelines  

### 🔹 **Using Credentials in a Jenkins Pipeline (`Jenkinsfile`)**  
```groovy
pipeline {
    agent any
    environment {
        GITHUB_TOKEN = credentials('github-token-id')
    }
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token-id', url: 'https://github.com/myrepo.git'
            }
        }
    }
}
```

---

## ✅ **4. Enabling Security & Authentication**  
Jenkins provides **various authentication mechanisms** to secure user logins.

### 🔹 **Authentication Methods in Jenkins**
| Method | Description |
|--------|-------------|
| **Jenkins Built-in User Database** | Default authentication system |
| **LDAP (Lightweight Directory Access Protocol)** | Integrates with Active Directory (AD) |
| **OAuth & SSO (GitHub, Google, SAML, Okta)** | Uses external identity providers |
| **SSH-Based Authentication** | Uses SSH keys for authentication |

### 🔹 **Setting Up LDAP Authentication**  
1️⃣ Install the **LDAP Plugin**  
2️⃣ Navigate to: **Manage Jenkins → Configure Global Security**  
3️⃣ Select **LDAP** and configure:  
   - Server: `ldap://ldap.company.com`
   - Root DN: `dc=company,dc=com`
   - User Search Base: `ou=users`
4️⃣ Save and apply  

### 🔹 **Enabling GitHub OAuth Authentication**  
1️⃣ Install **GitHub Authentication Plugin**  
2️⃣ Navigate to: **Manage Jenkins → Configure Global Security**  
3️⃣ Select **GitHub OAuth** and enter GitHub Client ID & Secret  
4️⃣ Configure **allowed users & organizations**  
5️⃣ Save and apply  

---

## ✅ **Summary**  
✔ **Create & manage users in Jenkins**  
✔ **Use RBAC for granular access control**  
✔ **Secure credentials using Jenkins Credentials Store**  
✔ **Enable authentication using LDAP, OAuth, or AD**  

---

### **1️⃣1️⃣ Jenkins & Infrastructure as Code (IaC)**  
# 🚀 **Jenkins for Infrastructure Automation & Cloud Deployments**  

Jenkins is widely used to **automate infrastructure provisioning** and **deploy applications** across cloud platforms like AWS, Kubernetes, Azure, and GCP. It also integrates with **Terraform** and **Ansible** for Infrastructure as Code (IaC) and configuration management.

---

## ✅ **1. Using Jenkins with Terraform for Infrastructure Provisioning**  
**Terraform** is an IaC tool used to provision infrastructure automatically. Jenkins can trigger Terraform workflows for cloud deployments.

### 🔹 **Steps to Integrate Terraform with Jenkins**
1️⃣ **Install Terraform in Jenkins Node**
   - On Linux:  
     ```bash
     wget https://releases.hashicorp.com/terraform/1.6.0/terraform_1.6.0_linux_amd64.zip
     unzip terraform_1.6.0_linux_amd64.zip
     sudo mv terraform /usr/local/bin/
     terraform -version
     ```
2️⃣ **Install Terraform Plugin in Jenkins**  
   - Navigate to: **Manage Jenkins → Plugin Manager → Install Terraform Plugin**  
3️⃣ **Create a Terraform Pipeline in Jenkins**  
4️⃣ **Store AWS credentials securely** using Jenkins Credentials Store  
5️⃣ **Write a `Jenkinsfile` for Terraform automation**  

### 🔹 **Jenkinsfile Example: Terraform Apply**
```groovy
pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
    }
    stages {
        stage('Checkout Code') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/user/terraform-repo.git'
            }
        }
        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }
        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }
}
```
🔹 **This Pipeline:**  
✔ Clones Terraform code  
✔ Initializes Terraform  
✔ Plans and applies the infrastructure changes  

---

## ✅ **2. Automating AWS, Kubernetes, Azure, and GCP Deployments**  
Jenkins can deploy applications to **cloud platforms** and **Kubernetes clusters**.

### 🔹 **Deploying to AWS from Jenkins**
1️⃣ Install AWS CLI on Jenkins:  
   ```bash
   sudo apt install awscli
   aws configure
   ```
2️⃣ Use Jenkins to automate:  
   - **Deploying to S3, Lambda, EC2**  
   - **Updating EKS Kubernetes Clusters**  
   - **Infrastructure management with Terraform**  

### 🔹 **Jenkinsfile for AWS Deployment**
```groovy
pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
    }
    stages {
        stage('Deploy to S3') {
            steps {
                sh 'aws s3 cp ./app s3://my-bucket --recursive'
            }
        }
    }
}
```

### 🔹 **Deploying to Kubernetes using Jenkins**
1️⃣ Install **Kubernetes CLI (`kubectl`)** in Jenkins  
2️⃣ Authenticate with the cluster using **Kubeconfig**  
3️⃣ Deploy using a **Jenkinsfile**  
```groovy
pipeline {
    agent any
    environment {
        KUBECONFIG = credentials('kubeconfig-id')
    }
    stages {
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
}
```

---

## ✅ **3. Running Ansible Playbooks from Jenkins**  
**Ansible** automates server configuration and application deployment.

### 🔹 **How to Integrate Ansible with Jenkins?**
1️⃣ Install Ansible on Jenkins Node:  
   ```bash
   sudo apt install ansible -y
   ```
2️⃣ Store SSH keys for **remote server access** in Jenkins Credentials Store  
3️⃣ Create a Jenkins Pipeline to **run Ansible Playbooks**  

### 🔹 **Jenkinsfile for Running Ansible Playbook**
```groovy
pipeline {
    agent any
    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }
    stages {
        stage('Run Ansible Playbook') {
            steps {
                sh 'ansible-playbook -i inventory.ini site.yml'
            }
        }
    }
}
```

🔹 **This Pipeline:**  
✔ Runs an **Ansible Playbook** to configure remote servers  
✔ Uses **inventory.ini** for dynamic host selection  

---

## ✅ **Summary**  
✔ **Use Terraform with Jenkins for Infrastructure Automation**  
✔ **Deploy applications to AWS, Kubernetes, Azure, and GCP**  
✔ **Run Ansible Playbooks from Jenkins Pipelines**  

---

### **1️⃣2️⃣ Jenkins & Docker Integration**  
# 🚀 **Jenkins with Docker for CI/CD**  

Jenkins integrates with **Docker** to build, test, and deploy applications in **containerized environments**. Using Docker in Jenkins allows for **consistent build environments, scalability, and efficient CI/CD workflows**.  

---

## ✅ **1. Running Jenkins in Docker Containers**  

### 🔹 **Why Run Jenkins in Docker?**  
✔ No need to install Jenkins manually on a machine  
✔ Easy to manage & upgrade versions  
✔ Can run isolated Jenkins instances  

### 🔹 **Steps to Run Jenkins in Docker**  

#### **📌 Step 1: Install Docker**  
Install Docker on your system (Linux/macOS/Windows):  
```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

#### **📌 Step 2: Run Jenkins Container**  
```bash
docker run -d -p 8080:8080 -p 50000:50000 \
  --name jenkins \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:lts
```

🔹 **Explanation:**  
- `-p 8080:8080`: Exposes Jenkins UI  
- `-p 50000:50000`: Allows agents to connect  
- `-v jenkins_home:/var/jenkins_home`: Stores Jenkins data  
- `-v /var/run/docker.sock:/var/run/docker.sock`: Allows Jenkins to use Docker  

#### **📌 Step 3: Access Jenkins**  
- Open **http://localhost:8080**  
- Retrieve the initial admin password:  
  ```bash
  docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
  ```
- Complete the **Jenkins setup**.

---

## ✅ **2. Building & Pushing Docker Images from Jenkins**  

Jenkins can automate **Docker image builds** and push them to **Docker Hub / AWS ECR / GCR**.

### 🔹 **Prerequisites**  
1️⃣ Install Docker inside Jenkins container:  
   ```bash
   docker exec -it jenkins apt update && apt install docker.io -y
   ```
2️⃣ Store Docker credentials in Jenkins (**Manage Jenkins → Credentials**)  
3️⃣ Create a **Jenkinsfile** for Docker build & push  

---

### 🔹 **Jenkinsfile for Building & Pushing Docker Images**  

```groovy
pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = credentials('dockerhub-user')
        DOCKERHUB_PASSWORD = credentials('dockerhub-password')
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/user/repository.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app:latest .'
            }
        }
        stage('Login to DockerHub') {
            steps {
                sh 'echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin'
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                sh 'docker tag my-app:latest my-dockerhub-username/my-app:latest'
                sh 'docker push my-dockerhub-username/my-app:latest'
            }
        }
    }
}
```

🔹 **This Pipeline:**  
✔ Clones code from GitHub  
✔ Builds a Docker image  
✔ Logs in to DockerHub  
✔ Pushes the image to DockerHub  

---

## ✅ **3. Using Docker Agents in Jenkins Pipelines**  

Instead of running Jenkins builds on the master node, we can use **Docker-based agents**.

### 🔹 **Steps to Use Docker Agents**  

#### **📌 Step 1: Install the Docker Pipeline Plugin**  
- Go to **Manage Jenkins → Plugin Manager → Install Docker Pipeline Plugin**  

#### **📌 Step 2: Use Docker Agents in Jenkinsfile**  
```groovy
pipeline {
    agent {
        docker {
            image 'maven:3.8.1'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}
```
🔹 **This Pipeline:**  
✔ Runs the build inside a `maven:3.8.1` Docker container  
✔ No need to install Maven on Jenkins  

---

## ✅ **Summary**  
✔ **Run Jenkins in Docker for easy setup**  
✔ **Automate Docker image builds & push to registries**  
✔ **Use Docker agents for isolated Jenkins builds**  


### **1️⃣3️⃣ Jenkins & Kubernetes Integration**  
# 🚀 **Jenkins with Kubernetes for CI/CD**  

Jenkins can be deployed on **Kubernetes** to manage CI/CD workflows efficiently. Using **Helm**, we can install Jenkins in a Kubernetes cluster and integrate it with Jenkins Pipelines for application deployment.

---

## ✅ **1. Running Jenkins in Kubernetes (`helm install jenkins`)**  

### 🔹 **Why Run Jenkins in Kubernetes?**  
✔ Scalable & Highly Available  
✔ Runs as a Kubernetes Pod (flexible resource allocation)  
✔ Uses Persistent Storage for data retention  

### 🔹 **Steps to Install Jenkins on Kubernetes**  

#### **📌 Step 1: Install Helm**  
```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

#### **📌 Step 2: Add the Jenkins Helm Repository**  
```bash
helm repo add jenkins https://charts.jenkins.io
helm repo update
```

#### **📌 Step 3: Install Jenkins using Helm**  
```bash
helm install jenkins jenkins/jenkins --namespace jenkins --create-namespace
```

#### **📌 Step 4: Get Jenkins Admin Password**  
```bash
kubectl get secret --namespace jenkins jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode
```

#### **📌 Step 5: Access Jenkins UI**  
```bash
kubectl port-forward svc/jenkins 8080:8080 -n jenkins
```
- Open **http://localhost:8080** in the browser.
- Login with **admin** and the retrieved password.

---

## ✅ **2. Deploying Apps to Kubernetes from Jenkins Pipelines**  

### 🔹 **Prerequisites**  
✔ **Kubernetes Cluster** (EKS, GKE, AKS, Minikube)  
✔ Install **kubectl** inside Jenkins  
✔ Store **Kubeconfig** in Jenkins credentials  

---

### 🔹 **Jenkinsfile for Deploying an App to Kubernetes**  

```groovy
pipeline {
    agent any
    environment {
        KUBECONFIG = credentials('kubeconfig-credentials-id')
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/user/repository.git'
            }
        }
        stage('Build & Push Docker Image') {
            steps {
                sh 'docker build -t my-app:latest .'
                sh 'docker tag my-app:latest my-dockerhub-username/my-app:latest'
                sh 'docker push my-dockerhub-username/my-app:latest'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl rollout status deployment my-app'
            }
        }
    }
}
```

🔹 **This Pipeline:**  
✔ Clones source code  
✔ Builds & pushes Docker image  
✔ Deploys the app using Kubernetes manifests  

---

## ✅ **3. Using Jenkins X for Kubernetes-Native CI/CD**  

### 🔹 **What is Jenkins X?**  
Jenkins X is a **Kubernetes-native CI/CD** tool that automates application delivery using GitOps.  

### 🔹 **Key Features**  
✔ Automated CI/CD for Kubernetes  
✔ Uses Helm & Kustomize for deployments  
✔ GitOps workflow for version control  

---

### 🔹 **Installing Jenkins X**  

#### **📌 Step 1: Install Jenkins X CLI**  
```bash
curl -L https://github.com/jenkins-x/jx/releases/download/v3.2.0/jx-linux-amd64.tar.gz | tar xzv
sudo mv jx /usr/local/bin/
```

#### **📌 Step 2: Bootstrap Jenkins X in Kubernetes**  
```bash
jx boot
```

#### **📌 Step 3: Create a New CI/CD Pipeline**  
```bash
jx create quickstart
```

---

## ✅ **Summary**  
✔ Install Jenkins in **Kubernetes using Helm**  
✔ Use Jenkins to **deploy apps to Kubernetes**  
✔ Leverage **Jenkins X for GitOps-driven CI/CD**   

---

### **1️⃣4️⃣ Monitoring & Logging in Jenkins**  
# 📌 **Monitoring & Debugging in Jenkins**  

A **DevOps Engineer** must be skilled in monitoring and debugging Jenkins to ensure smooth CI/CD operations. This includes viewing **build logs, system logs, and integrating monitoring tools** like Prometheus and Grafana.

---

## ✅ **1. Viewing Console Output & Build Logs**  

### 🔹 **What is Console Output?**  
- Displays real-time logs of a Jenkins job execution  
- Helps debug errors in **build, test, or deployment** stages  

### 🔹 **How to View Console Output?**  
1. **Go to Jenkins Dashboard**  
2. **Open the Job** you want to check  
3. Click on **Build Number (#) → Console Output**  

### 🔹 **Using the Jenkins CLI to Fetch Logs**  
```bash
java -jar jenkins-cli.jar -s http://jenkins-url/ console JOB_NAME
```

### 🔹 **Saving Console Logs for Analysis**  
```bash
jenkins_url/job/my-pipeline/lastBuild/consoleText > build.log
```

---

## ✅ **2. Using Jenkins System Logs for Debugging**  

### 🔹 **Where are Jenkins Logs Stored?**  
📂 **Linux (Ubuntu/Debian):**  
```bash
/var/log/jenkins/jenkins.log
```
📂 **Windows:**  
```bash
C:\ProgramData\Jenkins\.jenkins\logs
```
📂 **Docker:**  
```bash
docker logs <jenkins-container-id>
```

### 🔹 **How to View System Logs from Jenkins UI?**  
1. Navigate to **Manage Jenkins**  
2. Click **System Log**  
3. View detailed logs for Jenkins errors and warnings  

### 🔹 **Checking Jenkins Logs via CLI**  
```bash
tail -f /var/log/jenkins/jenkins.log
```

---

## ✅ **3. Monitoring Jenkins Performance with Prometheus & Grafana**  

### 🔹 **Why Monitor Jenkins?**  
✔ Identify slow builds  
✔ Track system resource usage (CPU, Memory)  
✔ Detect pipeline failures  

---

### 🔹 **Integrating Prometheus with Jenkins**  

#### **📌 Step 1: Install the Prometheus Plugin**  
- Go to **Manage Jenkins → Plugin Manager**  
- Install **Prometheus Metrics Plugin**  

#### **📌 Step 2: Enable Prometheus Metrics Endpoint**  
1. Go to **Manage Jenkins → Configure System**  
2. Find **Prometheus Metrics**  
3. Enable **‘Expose metrics to Prometheus’**  
4. Restart Jenkins  

#### **📌 Step 3: Verify the Metrics Endpoint**  
```bash
curl http://jenkins-url:8080/prometheus
```

---

### 🔹 **Setting Up Grafana Dashboard for Jenkins**  

#### **📌 Step 1: Install Grafana**  
```bash
sudo apt-get install grafana
```
#### **📌 Step 2: Configure Prometheus as a Data Source**  
1. Open Grafana UI (`http://localhost:3000`)  
2. Add **Prometheus Data Source**  
3. Enter Prometheus URL: `http://jenkins-url:8080/prometheus`  

#### **📌 Step 3: Import a Jenkins Dashboard**  
- Use a prebuilt **Jenkins Grafana Dashboard** (ID: `9964`)  

---

## ✅ **Summary**  
✔ View **Console Logs** & **System Logs** for debugging  
✔ Monitor Jenkins with **Prometheus & Grafana**  
✔ Track **CI/CD Performance & Pipeline Failures**  

---

### **1️⃣5️⃣ Jenkins Best Practices**  
# 📌 **Best Practices for Using Jenkins in DevOps**  

A **DevOps Engineer** must follow best practices to ensure Jenkins pipelines are **secure, scalable, and maintainable**. Below are key recommendations to optimize Jenkins usage.

---

## ✅ **1. Keep Jenkins Updated for Security**  

### 🔹 **Why Update Jenkins?**  
✔ Fixes **security vulnerabilities**  
✔ Enhances **performance & stability**  
✔ Supports **new plugins & integrations**  

### 🔹 **How to Update Jenkins?**  

📂 **For Linux (Debian/Ubuntu):**  
```bash
sudo systemctl stop jenkins
sudo apt update && sudo apt upgrade jenkins
sudo systemctl start jenkins
```

📂 **For Windows:**  
1. Download the latest `.war` file from [Jenkins](https://www.jenkins.io/download/)  
2. Replace the existing `jenkins.war`  
3. Restart the Jenkins service  

📂 **For Docker Users:**  
```bash
docker pull jenkins/jenkins:lts
docker stop my-jenkins
docker run -d -p 8080:8080 --name my-jenkins jenkins/jenkins:lts
```

---

## ✅ **2. Use Declarative Pipelines for Better Maintainability**  

### 🔹 **Why Prefer Declarative Pipelines?**  
✔ **Easier to read & write**  
✔ Supports **built-in validation**  
✔ Improves **pipeline standardization**  

### 🔹 **Example: Simple Declarative Pipeline (`Jenkinsfile`)**  
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
```

---

## ✅ **3. Store Jenkinsfiles in Git Repositories**  

### 🔹 **Why Store Pipelines in Git?**  
✔ Enables **version control** for pipelines  
✔ Allows **team collaboration**  
✔ Supports **code review & rollback**  

### 🔹 **How to Connect Jenkins with GitHub?**  
1. Install **Git Plugin** in Jenkins  
2. Add **GitHub Credentials** under `Manage Jenkins → Credentials`  
3. Configure your job to fetch `Jenkinsfile` from GitHub  

Example: **Pipeline Job Configuration**  
```groovy
pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/user/repo.git'
            }
        }
    }
}
```

---

## ✅ **4. Use Parameterization for Reusable Pipelines**  

### 🔹 **Why Use Parameters?**  
✔ Makes pipelines **flexible & reusable**  
✔ Allows users to **dynamically input values**  

### 🔹 **Example: Parameterized Pipeline**  
```groovy
pipeline {
    agent any
    parameters {
        string(name: 'ENV', defaultValue: 'dev', description: 'Environment to deploy')
    }
    stages {
        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENV} environment"
            }
        }
    }
}
```

---

## ✅ **5. Implement CI/CD Best Practices**  

### 🔹 **1️⃣ Use Webhooks for Faster Builds**  
- Instead of polling, **trigger builds on GitHub push**  
- Configure **GitHub Webhooks** to notify Jenkins  

### 🔹 **2️⃣ Run Security Scans in CI/CD**  
- Use **SonarQube Plugin** for code analysis  
- Run **Snyk or Trivy** for security scanning  

### 🔹 **3️⃣ Use Build Agents for Scalability**  
- Avoid running builds on the **Jenkins Master**  
- Use **Docker Agents** for isolated environments  

### 🔹 **4️⃣ Store Secrets Securely**  
- Use **Jenkins Credentials Store**  
- Avoid hardcoding **AWS Keys, API Tokens** in Jenkinsfiles  

### 🔹 **5️⃣ Automate Infrastructure Deployment**  
- Integrate with **Terraform** for Infrastructure as Code  
- Use **Ansible** to manage server configurations  

---

## ✅ **Summary**  
✔ Keep **Jenkins updated** for security  
✔ Use **Declarative Pipelines** for maintainability  
✔ Store **Jenkinsfiles in Git** for version control  
✔ Use **Pipeline Parameters** for flexibility  
✔ Follow **CI/CD Best Practices** for reliability  

---

## **🎯 Where to Go from Here?**  
📌 Start with **Basic Pipelines** → Move to **Advanced CI/CD**  
📌 Experiment with **Docker & Kubernetes Pipelines**  
📌 Learn about **Jenkins Shared Libraries**  

