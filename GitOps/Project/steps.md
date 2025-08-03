# Project Title: Multi-Cluster Deployment using Argo CD (Hub-Spoke Model)

---

### 🧠 Why this project?

In real-world DevOps environments:

* **Multiple teams use different Kubernetes clusters** (like `dev`, `qa`, `staging`, `prod`, `feature`, etc.).
* Traditionally, apps were deployed using **shell scripts or Ansible**. But:

  * They are **manual and error-prone**.
  * If a developer directly changes something in the cluster, it can **crash the application**.
* You want a **safer**, **automated**, and **declarative** way to manage apps across all clusters.

That's where **Argo CD** comes in.

---

### 🌟 What is Argo CD?

Argo CD is a GitOps tool for Kubernetes.
It ensures your cluster state (deployments, services, configs) is always in **sync with your Git repo**.

---

### 📦 What You'll Learn

By doing this project, you'll learn:

* 🔹 GitOps concepts with Argo CD
* 🔹 Argo CD installation using manifests
* 🔹 Differences between **Standalone** vs **Hub-Spoke**
* 🔹 How to manage **multiple clusters from one Argo CD instance**
* 🔹 Deploying apps across clusters using the Argo CD UI
* 🔹 Adding clusters using CLI

---

## 🌐 Architecture: Hub-Spoke Model

```
                       ┌────────────┐
                       │ Argo CD UI │
                       └────┬───────┘
                            │
             ┌──────────────┼──────────────┐
             ▼                              ▼
   ┌────────────────┐           ┌────────────────┐
   │ Spoke Cluster 1│           │ Spoke Cluster 2│
   │ (EKS - dev)    │           │ (EKS - prod)   │
   └────────────────┘           └────────────────┘
```

* One cluster (Hub) has Argo CD installed.
* Other clusters (Spokes) are managed remotely.
* App is deployed from **GitHub → via Argo CD → to multiple clusters**.

---

## 🔧 Prerequisites

Install the following on your local machine:

| Tool        | Purpose                      | Link                                                                                     |
| ----------- | ---------------------------- | ---------------------------------------------------------------------------------------- |
| kubectl     | Control Kubernetes clusters  | [Install kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html) |
| eksctl      | Create/manage EKS clusters   | [Install eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html)           |
| AWS CLI     | Interact with AWS            | [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)   |
| Argo CD CLI | Control Argo CD via terminal | [Install Argo CD CLI](https://argo-cd.readthedocs.io/en/stable/cli_installation/)        |

---

## 🚀 Step-by-Step Guide

---

### 🏗️ Step 1: Create 3 EKS Clusters

```bash
eksctl create cluster --name hub-cluster --region us-west-1
eksctl create cluster --name spoke-cluster-1 --region us-west-1
eksctl create cluster --name spoke-cluster-2 --region us-west-1
```

Check and switch context to hub:

```bash
kubectl config get-contexts
kubectl config use-context <hub-cluster-name>
kubectl config current-context
```

---

### 🧠 Step 2: Install Argo CD on Hub Cluster

```bash
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Wait and check:

```bash
kubectl get pods -n argocd
```

---

### 🌐 Step 3: Expose Argo CD UI (NodePort, Insecure)

Edit config to disable TLS:

```bash
kubectl edit configmap argocd-cmd-params-cm -n argocd
```

Add this:

```yaml
data:
  server.insecure: "true"
```

Then expose service via NodePort:

```bash
kubectl edit svc argocd-server -n argocd
```

Change type to:

```yaml
type: NodePort
```

Now get the URL:

```bash
kubectl get svc -n argocd
```

Visit: `http://<public-ip>:<nodeport>`
(Allow the port in EC2 security group!)

---

### 🔐 Step 4: Login to Argo CD

```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o yaml

# Decode:
echo '<base64-password>' | base64 --decode
```

Use `admin` as username and decoded password.

---

### 🛠️ Step 5: Add Spoke Clusters to Argo CD

Install Argo CD CLI:

[Argo CD CLI Installation](https://argo-cd.readthedocs.io/en/stable/cli_installation/)

Login to Argo CD:

```bash
argocd login <argocd-ip>:<port>
```

Get contexts:

```bash
kubectl config get-contexts
```

Add clusters:

```bash
kubectl config use-context <hub-cluster-context>
argocd cluster add <spoke-cluster-1-context>

argocd cluster add <spoke-cluster-2-context>
```

---

### 🚀 Step 6: Deploy Sample App to Spoke Clusters

From the Argo CD Web UI:

* Click **+ NEW APP**
* Fill in details:

| Field               | Value                                                                                                              |
| ------------------- | ------------------------------------------------------------------------------------------------------------------ |
| App Name            | guestbook                                                                                                          |
| Project             | default                                                                                                            |
| Sync Policy         | Automatic                                                                                                          |
| Repo URL            | [https://github.com/iam-veeramalla/argocd-hub-spoke-demo](https://github.com/iam-veeramalla/argocd-hub-spoke-demo) |
| Path                | manifests/guest-book                                                                                               |
| Destination Cluster | First Spoke Cluster                                                                                                |
| Namespace           | default                                                                                                            |

Repeat again for second spoke cluster.

---

## 📈 Final Result

* One Argo CD instance managing multiple clusters
* Apps deployed from Git, synced automatically
* No manual shell scripting
* Full GitOps workflow using hub-spoke model


