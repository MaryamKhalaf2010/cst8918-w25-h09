# CST8918 - DevOps: Infrastructure as Code  
### Hybrid-H09: Azure Kubernetes Service (AKS) Cluster with Terraform  
**Student:** Maryam Khalaf  
**Professor:** Robert McKenney  

---

## Overview  
This project provisions an Azure Kubernetes Service (AKS) cluster using Terraform and deploys a multi-tier sample application including:
-  RabbitMQ (message broker)  
-  Order Service (Node.js backend)  
-  Product Service (Rust backend)  
-  Store Front (Vue.js frontend)

---

##  Terraform Setup  

### Resources Created:
- Azure Resource Group (`aks-h09-rg`)
- AKS Cluster (`aks-h09-cluster`)
- Auto-scaling node pool (1–3 nodes, Standard_B2s)
- System-assigned managed identity

### Commands Used:
```bash
terraform init
terraform apply
```

### Output:
`kubeconfig` file for connecting with `kubectl`.

---

##  Kubernetes Deployment  

### Connect to AKS:
```bash
echo "$(terraform output -raw kube_config)" > kubeconfig
export KUBECONFIG=./kubeconfig
kubectl get nodes
```

### Deploy Sample App:
```bash
kubectl apply -f sample-app.yaml
```

### Validate:
```bash
kubectl get pods
kubectl get services
```

### Access App:
- External IP: [http://130.107.172.21](http://130.107.172.21)

---

##  Clean Up  
```bash
kubectl delete -f sample-app.yaml
terraform destroy
```

---

##  Files in Repo
- `main.tf` – Terraform config for AKS and resource group
- `outputs.tf` – Outputs kubeconfig
- `variables.tf` – Placeholder for future variables
- `sample-app.yaml` – Multi-tier app deployment
- `.gitignore` – Excludes terraform state and kubeconfig

---

##  Submission  
GitHub Repo: [https://github.com/MaryamKhalaf2010/cst8918-w25-h09](https://github.com/MaryamKhalaf2010/cst8918-w25-h09)
