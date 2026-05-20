````md
# KEDA AKS Queue Autoscaler

This project demonstrates event-driven autoscaling in Azure Kubernetes Service (AKS) using KEDA and Azure Queue Storage.

---

## Azure Login from VS Code

```powershell
az login --tenant "tenant-id"
```

---

## Connect to AKS Cluster

```powershell
az aks get-credentials --resource-group "test-keda-v" --name "keda-aks"
```

---

## Verify Kubernetes Nodes

```powershell
kubectl get nodes
```

---

## Deploy Application

```powershell
kubectl apply -f deployment.yml
```

---

## Install Helm

Install Helm (Kubernetes package manager) and add it to Environment Variables.

Example path:

```powershell
$env:Path += ";C:\helm"
```

Verify Helm installation:

```powershell
helm version
```

---

## Add KEDA Helm Repository

```powershell
helm repo add kedacore https://kedacore.github.io/charts
```

Verify repository:

```powershell
helm repo list
```

---

## Install KEDA

```powershell
helm install keda kedacore/keda `
  --namespace keda `
  --create-namespace
```

---

## Deploy KEDA ScaledObject

```powershell
kubectl apply -f scaledobject.yml
```

---

## Create Kubernetes Secret

Here, `azure-storage-secret` is the secret name referenced in the YAML file.

```powershell
kubectl create secret generic azure-storage-secret `
  --from-literal=connection="YOUR_CONNECTION_STRING"
```

---

## Verify Autoscaling

Get scaled objects:

```powershell
kubectl get scaledobject
```

Describe scaled object:

```powershell
kubectl describe scaledobject azure-queue-scaledobject
```
````
