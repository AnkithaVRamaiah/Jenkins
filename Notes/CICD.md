# CI/CD and Jenkins

## 🔄 What is CI/CD?

CI/CD is just a fancy term for **automating how we deliver code** to users.

Here’s how I understand it:

- **CI (Continuous Integration)**: Every time a developer pushes code (like to GitHub), it automatically goes through checks — like tests, code quality scans, and builds.
- **CD (Continuous Delivery/Deployment)**: After a successful build, the code is automatically deployed to environments like dev, staging, or even production.

So instead of manually building, testing, and deploying every time, **CI/CD tools like Jenkins handle everything in the background**. It saves time and reduces human error.

---

## 🤖 How CI/CD Works with Jenkins (Real-World Flow)

Let’s say I’m working on a project with my team:

1. A developer pushes code to GitHub.
2. A **webhook** is already set up, so it tells Jenkins: “Hey, something changed!”
3. Jenkins starts a **pipeline** – think of this as a list of tasks:
   - Run unit tests
   - Check code quality (maybe with SonarQube)
   - Scan for vulnerabilities
   - Build a Docker image
   - Push the image to Docker Hub or ECR
   - Deploy the app to a dev/test/prod environment

Jenkins handles all this automatically. If something fails, it can send an email or Slack message to the team.

So now, I don’t have to say, “Hey, did we run the tests?” or “Did we deploy the latest version?” — CI/CD already did it.

---

## 🧠 But Wait... Where Do These Steps Actually Run?

This is something I was confused about in the beginning too.

You might wonder:

> “Where does Jenkins run these pipeline steps?”

Well, Jenkins needs a **worker machine** (called an "agent") where it can execute these jobs. This agent could be:

- A Virtual Machine (VM)
- Or a Docker container (which is what most people use nowadays)

Now let me explain **why Docker agents are preferred over traditional VMs in Jenkins**.

---

## 🐳 Why I Prefer Docker Agents Over Virtual Machines in Jenkins Pipelines

This was a game-changer for me once I understood it.

### 🔴 Back Then – Jenkins Used Virtual Machines (VMs):
- Jenkins master would trigger a job.
- The job would run on a dedicated **VM agent**.
- But here’s the problem:
  - VMs are heavy (slow to boot, use a lot of RAM/CPU)
  - If I needed Node.js 18 and someone else needed Java 17, managing versions on the same VM caused conflicts
  - VMs just sit idle when not in use — total waste of resources

### ✅ Now – We Use Docker Containers as Agents:
- Instead of launching a full-blown VM, Jenkins spins up a **Docker container** on demand.
- Why that’s better:
  - 💡 It’s super lightweight and fast to start
  - 🧪 Each job gets a clean, isolated environment (no version conflicts!)
  - 🧹 After the job finishes, the container is automatically deleted — no mess, no leftovers

### 🧪 Simple Example:
Let’s say I need Python 3.11 just for one job.
- Jenkins pulls the `python:3.11` Docker image
- Runs my job inside that container
- Deletes the container once done

That’s it — I didn’t have to install Python manually or maintain any VM for it.

