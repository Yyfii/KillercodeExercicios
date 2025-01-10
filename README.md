# KILLERCODE | KUBERNETES | DESAFIO

- :white_check_mark: [**1**. Crie um pod chamado "my-pod" usando uma imagem simples como "nginx" e verifique seu estado com os comandos de monitoramento do Kubernetes.](#1-crie-um-pod-chamado-my-pod-usando-uma-imagem-simples-como-nginx-e-verifique-seu-estado-com-os-comandos-de-monitoramento-do-kubernetes)
- :white_check_mark: [**2**. Implante um Deployment chamado "my-deployment" com três réplicas de uma aplicação baseada na imagem "httpd". Atualize a imagem do Deployment para uma versão mais recente.](#2-implante-um-deployment-chamado-my-deployment-com-tr%C3%AAs-r%C3%A9plicas-de-uma-aplica%C3%A7%C3%A3o-baseada-na-imagem-httpd-atualize-a-imagem-do-deployment-para-uma-vers%C3%A3o-mais-recente)
- :white_check_mark: [**3**. Crie um ConfigMap chamado "app-config" com uma variável de configuração personalizada. Monte o ConfigMap em um pod e verifique se o valor foi aplicado corretamente.](#3-crie-um-configmap-chamado-app-config-com-uma-vari%C3%A1vel-de-configura%C3%A7%C3%A3o-personalizada-monte-o-configmap-em-um-pod-e-verifique-se-o-valor-foi-aplicado-correta...)
- :white_check_mark: [**4**. Crie um Secret chamado "app-secret" contendo informações sensíveis. Injete o Secret como uma variável de ambiente em um pod e teste se está acessível.](#4-crie-um-secret-chamado-app-secret-contendo-informa%C3%A7%C3%B5es-sens%C3%ADveis-injete-o-secret-como-uma-vari%C3%A1vel-de-ambiente-em-um-pod-e-teste-se-est%C3%A1-acess%C3%ADvel)
- :white_check_mark: [**5**. Configure um PersistentVolume de 1Gi de armazenamento local e vincule-o a um PersistentVolumeClaim. Monte o volume em um pod e salve arquivos para verificar a persistência.](#5-configure-um-persistentvolume-de-1gi-de-armazenamento-local-e-vincule-o-a-um-persistentvolumeclaim-monte-o-volume-em-um-pod-e-salve-arquivos-para-verificar-a-persist%C3%AAncia)
- :white_check_mark: [**6**. Crie um serviço do tipo ClusterIP para um Deployment chamado "backend" e teste a conectividade interna entre pods usando o nome do serviço.](#6-crie-um-servi%C3%A7o-do-tipo-clusterip-para-um-deployment-chamado-backend-e-teste-a-conectividade-interna-entre-pods-usando-o-nome-do-servi%C3%A7o)
- :white_check_mark: [**7**. Implante um Job chamado "batch-job" que execute um comando simples e termine. Verifique os logs do Job para confirmar sua execução.](#7-implante-um-job-chamado-batch-job-que-execute-um-comando-simples-e-termine-verifique-os-logs-do-job-para-confirmar-sua-execu%C3%A7%C3%A3o)
- :white_check_mark: [**8**. Crie um Horizontal Pod Autoscaler para um Deployment chamado "hpa-deployment" e configure-o para escalar com base no uso de CPU. Aumente a carga e observe o escalonamento.](#8-crie-um-horizontal-pod-autoscaler-para-um-deployment-chamado-hpa-deployment-e-configure-o-para-escalar-com-base-no-uso-de-cpu-aumente-a-carga-e-observe-o-escalonamento)
- :white_check_mark: [**9**. Crie um serviço do tipo NodePort para expor externamente um Deployment chamado "webapp". Acesse o serviço usando o endereço IP do Minikube e a porta atribuída.](#9-crie-um-servi%C3%A7o-do-tipo-nodeport-para-expor-externamente-um-deployment-chamado-webapp-acesse-o-servi%C3%A7o-usando-o-endere%C3%A7o-ip-do-minikube-e-a-porta-atribu%C3%ADda)
- :white_check_mark: [**10**. Crie um pod chamado "restart-pod" com a política de reinício configurada como "OnFailure". Provoque uma falha no pod e observe seu comportamento.](#10-crie-um-pod-chamado-restart-pod-com-a-pol%C3%ADtica-de-rein%C3%ADcio-configurada-como-onfailure-provoque-uma-falha-no-pod-e-observe-seu-comportamento)

### Instalando o Minikube no Windows (opcional)

- requisitos : Kubectl
  Entre com o PowerShell no modo administrador:

```
>Invoke-WebRequest -Uri "https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe" -OutFile "minikube.exe"
> move .\minikube.exe C:\Windows\System32
> minikube version
> minikube delete
> minikube start
> minikube status
>kubectl get nodes﻿
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   64s   v1.31.0﻿
> minikube dashboard

#Manage your minikube cluster

> minikube pause

> minikube unpause﻿
```

### [1. Crie um pod chamado "my-pod" usando uma imagem simples como "nginx" e verifique seu estado com os comandos de monitoramento do Kubernetes.]

```bash
> code first-pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-pod
spec:
  containers:
    - name: my-pod
      image: nginx:latest
```

```bash
> kubectl get all

> kubectl apply -f first-pod.yaml

> kubectl get all

> minikube ip
```

> Pods are not intended to be visible outside the cluster!By default, the Pod is only accessible by its internal IP address within the Kubernetes cluster. To make the hello-node Container accessible from outside the Kubernetes virtual network, you have to expose the Pod as a Kubernetes Service.

```bash
> kubectl describe pod my-pod
> kubectl exec my-pod -- ls
> kubectl exec my-pod -- curl localhost
> kubectl -it exec my-pod -- sh
> curl localhost
> exit
> kubectl logs my-pod
```

##### Extra(opcional): Um Pod é acessível apenas dentro do cluster, por isso termos um componente chamado de Service que ajuda a expor grupos de pods na internet.

```bash
> code first-pod.yaml﻿
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-pod
spec:
  containers:
    - name: my-pod
      image: nginx:latest
```

```bash
> code my-first-service.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-pod #the same label used in the pod
  ports:
    - name: http
      port: 80
      nodePort: 30090
  type: NodePort
```

```bash
>kubectl apply -f first-pod.yaml

>kubectl apply -f my-first-service.yaml

> kubectl get all

> minikube service my-service
```

> Uma página vai se abrir no seu navegador.

```bash
>kubectl delete po my-pod

>kubectl delete svc my-service﻿
```

### [2. Implante um Deployment chamado "my-deployment" com três réplicas de uma aplicação baseada na imagem "httpd". Atualize a imagem do Deployment para uma versão mais recente.]

### [3. Crie um ConfigMap chamado "app-config" com uma variável de configuração personalizada. Monte o ConfigMap em um pod e verifique se o valor foi aplicado corretamente.]

### [4. Crie um Secret chamado "app-secret" contendo informações sensíveis. Injete o Secret como uma variável de ambiente em um pod e teste se está acessível.]

### [5. Configure um PersistentVolume de 1Gi de armazenamento local e vincule-o a um PersistentVolumeClaim. Monte o volume em um pod e salve arquivos para verificar a persistência.]

### [6. Crie um serviço do tipo ClusterIP para um Deployment chamado "backend" e teste a conectividade interna entre pods usando o nome do serviço.]

### [7. Implante um Job chamado "batch-job" que execute um comando simples e termine. Verifique os logs do Job para confirmar sua execução.]

### [8. Crie um Horizontal Pod Autoscaler para um Deployment chamado "hpa-deployment" e configure-o para escalar com base no uso de CPU. Aumente a carga e observe o escalonamento.]

### [9. Crie um serviço do tipo NodePort para expor externamente um Deployment chamado "webapp". Acesse o serviço usando o endereço IP do Minikube e a porta atribuída.]

### [10. Crie um pod chamado "restart-pod" com a política de reinício configurada como "OnFailure". Provoque uma falha no pod e observe seu comportamento.]
