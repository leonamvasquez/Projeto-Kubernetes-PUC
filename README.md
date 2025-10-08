# Projeto Kubernetes

## Índice
- [Pré-requisitos](#pré-requisitos)
- [Iniciar o Cluster Kubernetes](#iniciar-o-cluster-kubernetes)
- [Implantar os Recursos](#implantar-os-recursos)
- [Verificar os Recursos Criados](#verificar-os-recursos-criados)
- [Acessar o Frontend](#acessar-o-frontend)
- [Testar o Autoscaling do Backend](#testar-o-autoscaling-do-backend)

## Pré-requisitos

Verifique se você possui as seguintes ferramentas instaladas e configuradas:
- Minikube ou outro cluster Kubernetes (Kind, EKS, GKE, etc.)
- `kubectl`
- Helm (opcional, caso use charts no futuro)

## Iniciar o Cluster Kubernetes

### Usando Minikube:
```bash
minikube start
```
Isso inicializa um cluster Kubernetes local.

### Usando outro cluster:
Siga as instruções de configuração específicas do provedor que você utiliza, como Kind, EKS ou GKE.

## Implantar os Recursos

Clone o repositório:
```bash
git clone https://github.com/leonamvasquez/Projeto-Kubernetes
cd Projeto-Kubernetes
```

Instale os recursos usando Helm:

```bash
helm install myapp ./
```
Isso instalará todos os recursos do seu chart Helm no cluster Kubernetes.

## Verificar os Recursos Criados

Listar Pods:
```bash
kubectl get pods
```

Listar Services:
```bash
kubectl get svc
```

Verificar o HPA (Horizontal Pod Autoscaler):
```bash
kubectl get hpa
```

## Acessar o Frontend

### Usando Minikube:
```bash
minikube service frontend
```

### Usando port-forward:
```bash
kubectl port-forward svc/frontend 3000:3000
```

Acesse no navegador:
```
http://localhost:3000
```

## Testar o Autoscaling do Backend

Gere carga no backend usando um pod de teste:
```bash
kubectl run -i --tty load-generator --image=busybox --restart=Never -- /bin/sh
```

Dentro do pod, execute um loop para gerar tráfego:
```bash
while true; do wget -q -O- http://backend-service:5000/health; done
```

Monitore o comportamento do HPA:
```bash
kubectl get hpa
```

Verifique o escalonamento dos pods:
```bash
kubectl get pods
```