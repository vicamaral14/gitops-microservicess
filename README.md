# 💻 Projeto GitOps - Online Boutique

> 🚀 Implementação do **Online Boutique** (microserviços) utilizando **GitOps com ArgoCD** e **Kubernetes (K3s via Rancher Desktop)**.  
> Este projeto demonstra o fluxo completo de deploy automatizado, sincronização contínua e versionamento da infraestrutura.

---

## 🧠 Visão Geral

O **GitOps** é uma metodologia que utiliza o **Git como a fonte única da verdade** para gerenciar a infraestrutura e aplicações.  
Com o **ArgoCD**, qualquer alteração feita no repositório é automaticamente aplicada no cluster, garantindo consistência e controle total.

---

## 🧩 Tecnologias Utilizadas

| Ferramenta | Descrição |
|-------------|------------|
| 🐳 **Rancher Desktop (K3s)** | Cluster Kubernetes local |
| ⚙️ **kubectl** | Gerenciamento de recursos do cluster |
| 🚀 **ArgoCD** | Implementação GitOps |
| 🧱 **GitHub** | Repositório de versionamento (`gitops-microservicess`) |
| 🛍️ **Online Boutique** | Aplicação exemplo de microserviços da Google Cloud |

---

## ⚙️ Etapas Realizadas

### 🧱 1. Criação do Cluster

Criação e verificação do cluster local usando o **Rancher Desktop (K3s)**:

```bash
kubectl get nodes -o wide
