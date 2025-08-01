# 🚀 Multi-Stage, Multi-Agent Jenkins Pipeline Using Docker

---

## 🚩 **Problem Statement (What's the issue?)**

In real-world DevOps projects, applications are often built using **multiple technologies**, such as:

* Frontend in **React** (Node.js)
* Backend in **Python**
* API Testing with **Postman/Newman**
* Deployment using **AWS CLI**

Now imagine trying to run all these tools on **a single Jenkins agent**. You’ll likely face problems:

* The agent may not have **all the tools** installed.
* Even if you install them all, **version conflicts** may occur.

* Example: Node.js and Python might need **different versions of `libssl`** or other system libraries.
* Updating one tool might **break another**.

So, running everything on one agent becomes **messy, error-prone, and hard to maintain**.

---

## ✅ **Solution: Use Multi-Stage, Multi-Agent Jenkins Pipeline**

**Each pipeline stage runs on its own isolated Docker container** with only the tools it needs.

### 🧱 Example Breakdown

| Stage          | Agent Image Used                   |
| -------------- | ---------------------------------- |
| Build Frontend | `node:16-alpine`                   |
| Build Backend  | `python:3.9-slim` (or Maven image) |
| Test APIs      | `postman/newman` Docker image      |
| Deploy         | AWS CLI installed image            |

Each stage runs in a **clean, self-contained Docker environment**, so there's:

* No tool conflicts
* No dependency issues
* Easy debugging and scalability

---

### 🧠 Why This Approach is Useful

| Problem               | Solved By                                |
| --------------------- | ---------------------------------------- |
| Conflicting tools     | Use different agents (Docker containers) |
| Long-term maintenance | Each container is simpler to manage      |
| Growing project       | Add more stages/agents as needed         |
| Debugging issues      | Errors are isolated to individual stages |

---

## 🧰 **Pre-requisites**

Refer to `commonsteps.md` for full setup. Key requirements:

* Jenkins installed (with **Docker Pipeline** plugin)
* Docker installed and running on Jenkins host
* Jenkins user **added to Docker group** (so it can run Docker)

---

# 🚀 **Step-by-Step Guide to Set Up the Project**

---

### 🔹 Step 1: Open Jenkins in Browser

Open Jenkins UI:

```
http://<your-server-ip>:8080
```

---

### 🔹 Step 2: Create a New Pipeline Job

1. Click **“New Item”**
2. Enter a name like `multi-agent-demo`
3. Select **Pipeline**
4. Click **OK**

---

### 🔹 Step 3: Add Jenkins Pipeline Script

#### ✅ Option 1: Paste Script in Job

* Go to the **Pipeline** section
* Set **Definition** = `Pipeline script`
* Paste the sample script (see below)

#### ✅ Option 2: Load from GitHub (Recommended for teams)

* Set **Definition** = `Pipeline script from SCM`
* Choose **SCM** = `Git`
* Provide:

  * **Repo URL**
  * **Branch** (e.g., `main`)
  * **Script Path** (e.g., `Jenkinsfile`)

---

### ✅ Sample Jenkinsfile Using Docker Agents

```groovy
pipeline {
  agent none
  stages {
    stage('Back-end') {
      agent {
        docker { image 'maven:3.8.1-adoptopenjdk-11' }
      }
      steps {
        sh 'mvn --version'
      }
    }
    stage('Front-end') {
      agent {
        docker { image 'node:16-alpine' }
      }
      steps {
        sh 'node --version'
      }
    }
  }
}
```

---

### 🔹 Step 4: Run the Pipeline

1. Click **Save**
2. Click **Build Now**
3. Watch the pipeline run:

   * Jenkins will **pull each Docker image**
   * Execute stage-specific tasks in **clean containers**
   * **Clean up containers** after each stage

