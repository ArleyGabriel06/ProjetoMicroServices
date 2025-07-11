# Projeto Micro Services Kubernete GitOps/ArgoCD

## Objetivo:

**Executar um conjunto de microserviços (Online Boutique) em Kubernetes
local usando Rancher Desktop, controlado por GitOps com ArgoCD, a partir de
um repositório público no GitHub**

### Tecnologias usadas:

* Rancher Desktop
* Kubernete
* Docker
* GitHub
* ArgoCD

### Etapa 1 - Fork e repositório GitHub:

**1. Fork do repositório oficial:**
**a. https://github.com/GoogleCloudPlatform/microservices-demo**

**2. Criar um repositório no GitHub com:**

**a. Apenas o arquivo release/kubernetes-manifests.yaml**

**b. Estrutura recomendada:**

```
gitops-microservices/
└── k8s/
 └── online-boutique.yaml
```

### Etapa 2 - Instalar ArgoCD no cluster local.

**Vá até o terminal e coloque os seguintes comenados:**

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argocd/stable/manifests/install.yaml
```

**Para rodar o argoCD localmente na sua maquina use o comando:**

```
kubectl port-forward svc/argocd-server -n argocd 8080:80 
```

**Depois vai em seu navegador e coloque localhost:8080. Vai aparecer essa área de login.**

**No login você irá colocar ```admin``` e na senha terá que voltar no terminal e digitar o seguinte comando:** 

```
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | ForEach-Object { [System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($_)) } 
```

 **isso caso estiver usando Windons, caso seja linux você irá colocar este:**

```
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
```

**Agora que tenhos o login completo, acesse o argoCD e vai em ```NEW APP``` dentro coloque as seguintes opções:**

![](/img/NEWAPP1.png)

![](/img/NEWAPP2.png)

![](/img/NEWAPP3.png)

**Após isso pode ir em ```CREATE``` e ver os microserviços subindo:**

![](/img/FUNCIONAMENTO2.png)

![](/img/FUNCIONAMENTO1.png)

**Volte ao terminal e coloque o seguinte comando para acessar a pagina web:**

```
kubectl port-forward svc/frontend-external -n default 8081:80 
```
![](/img/website.png)

## Entregas Esperadas

• ✅ Criar um repositório Git público com a estrutura de manifests [YAML](./k8s/online-boutique.yaml).

• ✅ Fazer o deploy do ArgoCD corretamente.

• ✅ Criar o App no ArgoCD apontando para o repositório Git

• ✅ Sincronizar a aplicação e garantir que os pods estejam rodando.

• ✅ Acessar o frontend da aplicação via kubectl port-forward.

• ✅ (Opcional) Customizar o manifest (ex: mudar número de réplicas de
algum microserviço).