# 💺 ArgoCD Setup & GitOps Deployment

This guide walks you through installing ArgoCD on your Kubernetes cluster and setting up GitOps for both development and production environments.

---

## 📦 Step 1: Create Namespace for ArgoCD

```bash
kubectl create namespace argocd
```

---

## ⚙️ Step 2: Install ArgoCD

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

---

## 🔑 Step 3: Get ArgoCD Admin Password

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

---

## 🌐 Step 4: Access the ArgoCD UI

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Open your browser and go to: [http://localhost:8080](http://localhost:8080)  
Log in with:
- **Username:** `admin`
- **Password:** (from step 3)

---

## 🚀 GitOps Setup

### 🧪 Development Environment

1. Go to the ArgoCD UI and click **+ New App**
2. Fill in the following fields:
   - **Application Name:** `dev`
   - **Project Name:** `default`
   - **Sync Policy:** `Automatic`
   - ✅ Enable **Prune Resources**
   - **Repository URL:** `https://github.com/<your-account>/workshop`
   - **Revision:** `main`
   - **Path:** `infra/gitops/dev`
   - **Cluster URL:** `https://kubernetes.default.svc`
3. Click **Create** in the top-left corner

> ⚠️ Make sure your GitHub repository is public: [https://github.com/?tab=packages](https://github.com/?tab=packages)  
> (If it says "private," ArgoCD may not be able to fetch it)

---

### 🏭 Production Environment

1. Go to the ArgoCD UI and click **+ New App**
2. Fill in the following fields:
   - **Application Name:** `prod`
   - **Project Name:** `default`
   - **Sync Policy:** `Automatic`
   - ✅ Enable **Prune Resources**
   - **Repository URL:** `https://github.com/<your-account>/workshop`
   - **Revision:** `main`
   - **Path:** `infra/gitops/prd`
   - **Cluster URL:** `https://kubernetes.default.svc`
3. Click **Create** in the top-left corner

---

## ✅ Done!

Your GitOps setup with ArgoCD is now ready to manage your Kubernetes environments.  
Happy deploying! 🚀
