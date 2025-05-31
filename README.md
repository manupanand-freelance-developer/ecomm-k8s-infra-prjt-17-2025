
# 🛒 AWS  3-Tier Infrastructure for eCommerce Microservices - Kubernetes -EKS

This repository contains the infrastructure-as-code setup to deploy a production-ready **3-tier architecture** for an **eCommerce microservices application** on AWS using **K3s (lightweight Kubernetes)**. It leverages **Terraform**, **Ansible**, and **HashiCorp Vault** to automate infrastructure provisioning, configuration management, and secrets handling.

---

## 🔧 Tech Stack

- **Infrastructure**: AWS (EC2, VPC, NAT Gateway, Subnets, EIP, Security Groups)
- **Provisioning**: Terraform
- **Configuration Management**: Ansible
- **Secrets Management**: HashiCorp Vault
- **Container Orchestration**: K3s Kubernetes
- **Microservices (Languages)**:
  - Node.js (e.g., Product Service)
  - Python (e.g., Recommendation Service)
  - Java (e.g., Order/Inventory Service)
  - Go (e.g., Payment or Auth Service)
- **Messaging**: RabbitMQ

---

## 🏗️ Architecture Overview

- **3-Tier VPC Layout**:
  - **Public Subnet**: Bastion host, NAT gateway, Internet gateway
  - **App Tier**: K3s server nodes (control plane), microservices
  - **Data Tier**: Databases, RabbitMQ, Vault (private subnets)

- **K3s Cluster**:
  - Deployed on EC2 instances across multiple AZs
  - Lightweight and ideal for microservices workloads
  - Automated via Ansible

- **Vault**:
  - Used to manage secrets (DB creds, app secrets, TLS)
  - Integrated with K3s via Kubernetes Auth method

---

## 🚀 Getting Started

### 1. Clone Repository
```bash
git clone https://github.com/your-org/aws-k3s-ecommerce.git
cd aws-k3s-ecommerce
````

### 2. Provision Infrastructure

```bash
cd terraform
terraform init
terraform apply
```

### 3. Configure Instances & Install K3s

```bash
cd ../ansible
ansible-playbook site.yml -i inventory/aws_ec2.yml
```

### 4. Access K3s

```bash
kubectl --kubeconfig ~/.kube/config get nodes
```

---

## 🔐 Secrets Management

* Vault is bootstrapped using Ansible
* Dynamic secrets for databases
* K8s service account-based authentication for pods

---

## 📦 Microservices Deployment

Each service has its own Helm chart or Kubernetes manifest:

* `/services/product/`
* `/services/payment/`
* `/services/order/`
* etc.

Deploy via:

```bash
kubectl apply -f services/product/
```

---

## 📬 Messaging Queue

RabbitMQ is deployed internally for async communication:

* Auth → Payment
* Cart → Inventory
* Order → Shipping

---

## 🧪 Future Enhancements

* CI/CD using GitHub Actions or ArgoCD
* Service Mesh (Istio or Linkerd)
* Observability: Prometheus, Grafana, Loki, Jaeger

---

## 📁 Repo Structure

```
.
├── terraform/         # VPC, EC2, Networking
├── ansible/           # K3s install, Vault, RabbitMQ, system setup
├── services/          # Microservices (Node.js, Go, Java, Python)
├── vault/             # Vault configuration
└── README.md
```

---

## 👤 Author

**Your Name**
DevOps Engineer | Cloud Architect | Open Source Contributor
[LinkedIn](https://www.linkedin.com/in/manupanand) · [GitHub](https://github.com/manupanand)

---
## 🧾 License

GNU Public license v3 2025. See `LICENSE` file for more information.

