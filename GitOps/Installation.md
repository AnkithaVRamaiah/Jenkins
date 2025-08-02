# 🧠 What You'll Learn in This Project

By practicing this project, you will:

✅ Learn how to set up a local Kubernetes cluster using Minikube
✅ Understand Argo CD and GitOps fundamentals
✅ Practice 3 methods to install Argo CD on Kubernetes (plain manifests, Helm, Operator)
✅ Learn to access and use the Argo CD web UI and CLI
✅ Deploy sample GitOps applications to your cluster
✅ Get hands-on with real-world Argo CD workflows

---

# 🚀 Part 1: Set up Kubernetes Cluster using Minikube

📄 Reference: [minikube.md](https://github.com/AnkithaVRamaiah/Kubernetes/blob/main/Notes/minikube.md)

### ✅ Steps

1. **Start Minikube**

   ```bash
   minikube start --driver=docker
   ```

2. **Check Status**

   ```bash
   minikube status
   ```

3. **Enable the Dashboard (optional but nice)**

   ```bash
   minikube dashboard
   ```

You now have a local Kubernetes cluster running using Docker.

---

# 🔧 Part 2: Argo CD Installation - 3 Ways

We’ll install Argo CD inside our Kubernetes cluster. Argo CD is a GitOps tool to deploy applications to K8s using Git as the source of truth.

---

## 🛠️ Method 1: Install Argo CD using Plain Kubernetes Manifests

📄 Official Docs: [Argo CD Install](https://argo-cd.readthedocs.io/en/stable/)

### 🔹 Step-by-step:

1. **Create Namespace for Argo CD**

   ```bash
   kubectl create namespace argocd
   ```

2. **Install Argo CD Core Components**

   ```bash
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

3. **Verify Argo CD is Running**

   ```bash
   kubectl get pods -n argocd
   ```

4. **Expose Argo CD UI using NodePort**

   By default, `argocd-server` is ClusterIP (internal only). Let’s make it accessible:

   ```bash
   kubectl edit svc argocd-server -n argocd
   ```

   Change:

   ```yaml
   type: ClusterIP
   ```

   to

   ```yaml
   type: NodePort
   ```

5. **Get the Argo CD UI URL**

   ```bash
   minikube service argocd-server -n argocd
   ```

   This opens your browser to the Argo CD login page. If not, just copy the URL shown.

6. **Login to Argo CD Web UI**

   * **Username**: `admin`
   * **Password**:

     ```bash
     kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
     ```

     Copy the `password` value, then decode it:

     ```bash
     echo '<base64-password>' | base64 --decode
     ```

---

## 🧪 Deploy Sample App using Argo CD UI

1. Open the Argo CD Web UI

2. Click **+ NEW APP**

3. Fill in:

   | Field               | Value                                                                                              |
   | ------------------- | -------------------------------------------------------------------------------------------------- |
   | App Name            | guestbook                                                                                          |
   | Project             | default                                                                                            |
   | Sync Policy         | Automatic                                                                                          |
   | Repo URL            | [https://github.com/argoproj/argocd-example-apps](https://github.com/argoproj/argocd-example-apps) |
   | Path                | guestbook                                                                                          |
   | Destination Cluster | [https://kubernetes.default.svc](https://kubernetes.default.svc)                                   |
   | Namespace           | default                                                                                            |

4. Click **Create**

Argo CD will automatically sync and deploy the app!

---

## 💻 CLI Access to Argo CD

📄 Docs:

* [CLI Installation](https://argo-cd.readthedocs.io/en/stable/cli_installation/)
* [CLI Commands](https://argo-cd.readthedocs.io/en/latest/user-guide/commands/argocd/)

1. **Install CLI**

   ```bash
   brew install argocd # or use binary from docs for Linux/Windows
   ```

2. **Login**

   ```bash
   argocd login <ARGOCD_IP>:<PORT> --username admin --password <decoded_password>
   ```

3. **Create App using CLI**

   ```bash
   argocd app create guestbook \
     --repo https://github.com/argoproj/argocd-example-apps \
     --path guestbook \
     --dest-namespace default \
     --dest-server https://kubernetes.default.svc \
     --directory-recurse
   ```

4. **List Apps**

   ```bash
   argocd app list
   ```

5. **Check App Status**

   ```bash
   argocd app get guestbook
   ```

6. **Sync Manually (if needed)**

   ```bash
   argocd app sync guestbook
   ```

---

## 🪄 Method 2: Install Argo CD using Helm

📄 Repo: [argo-helm](https://github.com/argoproj/argo-helm)

### Steps:

1. **Add Helm Repo**

   ```bash
   helm repo add argo https://argoproj.github.io/argo-helm
   helm repo update
   ```

2. **Create Namespace**

   ```bash
   kubectl create namespace argocd
   ```

3. **Install Using Helm**

   ```bash
   helm install argocd argo/argo-cd -n argocd
   ```

4. **Access Argo CD UI (same as Method 1)**

   * Edit service `argocd-server` to NodePort
   * Use `minikube service` to get URL
   * Decode password from secret
   * Login as `admin`

✅ This method is useful when you want more customization using Helm values.

---

## 🧩 Method 3: Install Argo CD using Operator

📄 OperatorHub: [Argo CD Operator](https://operatorhub.io/operator/argocd-operator)

This is a more enterprise-style installation using Operators to manage lifecycle.

### Steps:

1. **Install Operator Lifecycle Manager (OLM)**

   ```bash
   curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.26.0/install.sh | bash
   ```

2. **Apply Argo CD Operator from OperatorHub**

   ```bash
   kubectl apply -f https://operatorhub.io/install/argocd-operator.yaml
   ```

3. **Check Operator Pod**

   ```bash
   kubectl get pods -n operators
   ```

4. **Install Argo CD via ArgoCD CR (Custom Resource)**

   Create a YAML file:

   ```yaml
   apiVersion: argoproj.io/v1alpha1
   kind: ArgoCD
   metadata:
     name: example-argocd
     namespace: argocd
   spec: {}
   ```

   Apply it:

   ```bash
   kubectl create ns argocd
   kubectl apply -f argocd-cr.yaml
   ```

5. Access Argo CD:
   Same method – expose service, get password, login.

✅ Operator method is best for teams who want managed lifecycle via CRDs.

---

# 🧼 Cleanup

To remove all:

```bash
minikube delete
```

