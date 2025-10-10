# 💻 Projeto GitOps - Online Boutique

> 🚀 Implementação do **Online Boutique** (microserviços) utilizando **GitOps com ArgoCD** e **Kubernetes (K3s via Rancher Desktop)**.  
> Este projeto demonstra o fluxo completo de deploy automatizado, sincronização contínua e versionamento da infraestrutura.

---

## **🧠 Visão Geral**

O **GitOps** é uma metodologia que utiliza o **Git como a fonte única da verdade** para gerenciar a infraestrutura e aplicações.  
Com o **ArgoCD**, qualquer alteração feita no repositório é automaticamente aplicada no cluster, garantindo **consistência, segurança e rastreabilidade**.

---

## **🧩 Tecnologias Utilizadas**

| Ferramenta | Descrição |
|-------------|------------|
| 🐳 **Rancher Desktop (K3s)** | Cluster Kubernetes local |
| ⚙️ **kubectl** | Gerenciamento de recursos do cluster |
| 🚀 **ArgoCD** | Implementação GitOps |
| 🧱 **GitHub** | Repositório de versionamento (`gitops-microservices`) |
| 🛍️ **Online Boutique** | Aplicação exemplo de microserviços da Google Cloud |

---

## **⚙️ Pré-requisitos**

Antes de iniciar, verifique se possui:

- ✅ **Rancher Desktop** instalado e **Kubernetes habilitado**  
- ✅ **kubectl** configurado (`kubectl get nodes` funcionando)  
- ✅ **ArgoCD** instalado no cluster  
- ✅ **Conta no GitHub** com repositório público  

---

## 🚀 Etapas do Projeto
## **1️⃣ Fork e criação do repositório**

Faça o fork do repositório oficial:  
👉 [GoogleCloudPlatform/microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo)

No seu GitHub, crie um novo repositório público e adicione apenas o arquivo:

```bash
release/kubernetes-manifests.yaml
````
Renomeie a estrutura do projeto para:
```bash
k8s/online-boutique.yaml
````

## 2️⃣ Instalação do ArgoCD no cluster

Execute os comandos abaixo para instalar o ArgoCD:
````bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
````

## 3️⃣ Acessar a interface do ArgoCD

Crie o port-forward:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
````

Acesse em seu navegador:
```bash
https://localhost:8080
Login padrão:
Usuário: admin
Senha:
````
Para pegar a senha utilize
````bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
````

## 4️⃣ Criar o App no ArgoCD

Na interface do ArgoCD:
  - Clique em “NEW APP”
Configure os seguintes campos:
  - Application Name: online-boutique
  - Repository URL: URL do seu repositório GitHub
  - Path: k8s
  - Cluster: https://kubernetes.default.svc
  - Namespace: default
  - Clique em Create
Em seguida, clique em Sync para aplicar as mudanças no cluster local.

## **5️⃣ Acessar o front-end da aplicação**

Como o frontend roda como um serviço **ClusterIP**, execute o comando abaixo para criar o port-forward:

```bash
kubectl port-forward svc/frontend 8081:80
Em seguida, acesse o frontend da aplicação no navegador:
🔗 http://localhost:8081

````
<img width="1347" height="888" alt="argo" src="https://github.com/user-attachments/assets/f1014875-722a-4aa4-837c-da964af5e04a" />

<img width="1501" height="842" alt="site" src="https://github.com/user-attachments/assets/3f34b4f1-6425-4ac5-9f62-193b8844dc40" />


## **✅ Entregas Esperadas**

- [x] **Repositório Git público** com manifests YAML  
- [x] **Deploy do ArgoCD** configurado corretamente  
- [x] **Aplicação criada e sincronizada** no ArgoCD  
- [x] **Pods em execução** no cluster local  
- [x] **Front-end acessível** via `kubectl port-forward`  
- [ ] *(Opcional)* **Customização dos manifests**, como alterar o número de réplicas de um microserviço  


## **🧠 Conceitos-Chave**

| Conceito | Descrição |
|:---------:|------------|
| ⚡ **Kubernetes** | Orquestrador de containers que garante escalabilidade, resiliência e automação. |
| 🔁 **GitOps** | Abordagem declarativa que usa o Git como fonte de verdade para infraestrutura e aplicações. |
| 🧭 **ArgoCD** | Ferramenta de entrega contínua baseada em GitOps para Kubernetes. |

## **🧪 Comandos Úteis**

```bash
# Verificar nós do cluster
kubectl get nodes -o wide

# Listar pods em execução
kubectl get pods -A

# Verificar serviços disponíveis
kubectl get svc -A

# Sincronizar aplicação manualmente via CLI
argocd app sync online-boutique



