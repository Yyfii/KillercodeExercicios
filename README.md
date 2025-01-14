# KILLERCODE | KUBERNETES | DESAFIO

<p align="center">
  <img src="hello.png" alt="Project Header" width="1000">
</p>

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)](https://nginx.org/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)

![alt text](container_hello_diagram.jpeg)

Requisitos:

- Docker desktop instalado.
  Run : `docker --version`
- Kubernetes ativado.
  Run : `kubectl get all`
- Minikube ativado.
  Run : `minikube status`

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

```bash
> code deployments.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
  labels:
    app: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels: #match selector wich connects the pods to this deployment resource
      app: my-pod
  template: #defines the pod that it will be deploying.
    metadata:
      labels:
        app: my-pod
    spec:
      containers:
        - name: my-pod
          image: httpd:2
          ports:
            - containerPort: 80
```

```bash
> kubectl get all
..
NAME                            READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/my-deployment   3/3     3            3           23s

NAME                                      DESIRED   CURRENT   READY   AGE
replicaset.apps/my-deployment-dd9f64cb8   3         3         3       23s﻿
> code deployments.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
  labels:
    app: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels: #match selector wich connects the pods to this deployment resource
      app: my-pod
  template: #defines the pod that it will be deploying.
    metadata:
      labels:
        app: my-pod
    spec:
      containers:
        - name: my-pod
          image: httpd:latest
          ports:
            - containerPort: 80
```

```bash
> kubectl apply -f deployments.yaml
> kubectl describe deployments
  Containers:
   my-pod:
    Image:         httpd:latest
> kubectl delete -f deployments.yaml
```

### [3. Crie um ConfigMap chamado "app-config" com uma variável de configuração personalizada. Monte o ConfigMap em um pod e verifique se o valor foi aplicado corretamente.]

```bash
> code cm.yml
```

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  configValue: "Hello, i´m a config value."
```

```bash
> kubectl apply -f cm.yml

> kubectl get cm

> kubectl describe cm app-config

> code cm-deployment.yml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cm-deployment
  labels:
    app: cm-deployment
spec:
  replicas: 2
  selector:
    matchLabels: #match selector wich connects the pods to this deployment resource
      app: cm-pod
  template: #defines the pod that it will be deploying.
    metadata:
      labels:
        app: cm-pod
    spec:
      containers:
        - name: cm-pod
          image: httpd:2
          env:
            - name: app-config
              valueFrom:
                configMapKeyRef:
                  name: app-config
                  key: configValue
          ports:
            - containerPort: 80
```

```bash
> kubectl exec -it cm-deployment-647545586-bp55b -- /bin/bash

>env | grep app-config

app-config=Hello, i´m a config value.
```

### [4. Crie um Secret chamado "app-secret" contendo informações sensíveis. Injete o Secret como uma variável de ambiente em um pod e teste se está acessível.]

```bash
> kubectl create secret generic app-secret --from-literal=secretValue="masterkey"

>kubectl get secrets

> kubectl describe secret app-secret

> kubectl edit secret app-secret #copy the secret value

> echo bWFzdGVya2V5 | base64 --decode

masterkeyroot

> code secret-deployment.yml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: secret-deployment
  labels:
    app: secret-deployment
spec:
  replicas: 2
  selector:
    matchLabels: #match selector wich connects the pods to this deployment resource
      app: secret-pod
  template: #defines the pod that it will be deploying.
    metadata:
      labels:
        app: secret-pod
    spec:
      containers:
        - name: secret-pod
          image: httpd:2
          env:
            - name: app-secret
              valueFrom:
                secretKeyRef:
                  name: app-secret
                  key: secretValue
          ports:
            - containerPort: 80
```

```bash
> kubectl get all

> kubectl get deploy

> kubectl exec -it secret-deployment-99cd6dd4d-d6s2m -- /bin/bash

>  env | grep app-secret

app-secret=masterkey
```

### [5. Configure um PersistentVolume de 1Gi de armazenamento local e vincule-o a um PersistentVolumeClaim. Monte o volume em um pod e salve arquivos para verificar a persistência.]

```bash
> code pv.yaml #PersistentVolume
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: task-pv-volume
  labels:
    type: local
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/hostpath-vol0-source-path"
    type: DirectoryOrCreate
```

```bash
> code pvc.yaml #PersistentVolumeClaim
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pv-claim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

```bash
> code pvc-pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: task-pv-pod
spec:
  volumes:
    - name: task-pv-storage
      persistentVolumeClaim:
        claimName: task-pv-claim
  containers:
    - name: task-pv-container
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: task-pv-storage
```

```bash
> kubectl exec -it task-pv-pod -- /bin/bash

> cd /usr/share/nginx/html

> df -h

> cat > index.html <<EOF <html> <body> <h1>It works! Hello from PersistentVolume</h1> </body> </html> EOF

> curl localhost

> exit

> kubectl delete -f pvc-pod.yaml

> kubectl apply -f pvc-pod.yaml

> kubectl exec -it task-pv-pod -- curl localhost

> kubectl exec -it task-pv-pod -- ls /usr/share/nginx/html
```

### [6. Crie um serviço do tipo ClusterIP para um Deployment chamado "backend" e teste a conectividade interna entre pods usando o nome do serviço.]

```bash
>code svc-deploy.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend
  labels:
    app: backend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-backend
  template:
    metadata:
      labels:
        app: my-backend
    spec:
      containers:
        - name: my-backend
          image: httpd:latest
          ports:
            - containerPort: 80
```

```bash
> code svc-clusterip.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  selector:
    app: my-backend
  ports:
    - name: http
      port: 80
  type: ClusterIP
```

```bash
> kubectl apply -f svc-deploy.yaml

> kubectl apply -f svc-clusterip.yaml

> kubectl get svc

> kubectl get all

> kubectl exec -it backend-67b6fcf59-4585r -- /bin/bash

> apt-get update

> apt-get install curl iputils-ping

> ping localhost

>  curl localhost

> curl 10.98.23.199 #clusterip do serviço
> curl http://backend-service:80

<html><body><h1>It works!</h1></body></html>

#testando em outro pod

> kubectl exec -it backend-67b6fcf59-xqcxs -- /bin/bash

> apt-get update

> apt-get install curl iputils-ping

> curl http://backend-service:80
```

### [7. Implante um Job chamado "batch-job" que execute um comando simples e termine. Verifique os logs do Job para confirmar sua execução.]

```bash
> code job.yaml
```

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: batch-job
spec:
  schedule: "* * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: batch-job
              image: busybox
              command: ["echo", "Hello from the kubernetes cluster!"]
          restartPolicy: OnFailure
```

```bash
> kubectl apply -f job.yaml

> kubectl get cronjon batch-job

> kubectl get jobs --watch

> kubectl describe cronjob batch-job

> kubectl get all

> kubectl logs batch-job-28942383-4xstf

Hello from the kubernetes cluster!
```

### [8. Crie um Horizontal Pod Autoscaler para um Deployment chamado "hpa-deployment" e configure-o para escalar com base no uso de CPU. Aumente a carga e observe o escalonamento.]

```bash
> kubectl get nodes
> code deploy.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php-apache
spec:
  selector:
    matchLabels:
      run: php-apache
  template:
    metadata:
      labels:
        run: php-apache
    spec:
      containers:
        - name: php-apache
          image: registry.k8s.io/hpa-example
          ports:
            - containerPort: 80
          resources:
            limits:
              cpu: 500m
            requests:
              cpu: 200m
---
apiVersion: v1
kind: Service
metadata:
  name: php-apache
  labels:
    run: php-apache
spec:
  ports:
    - port: 80
  selector:
    run: php-apache
```

```bash
> kubectl apply -f deploy.yaml
> kubectl get po
#create the hpa object
> kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
> kubectl edit deployment metrics-server -n kube-system

containers:
- args:
  - --cert-dir=/tmp
  - --secure-port=10250
  - --kubelet-preferred-address-types=InternalIP,Hostname,ExternalIP
  - --kubelet-use-node-status-port
  - --metric-resolution=15s
  - --kubelet-insecure-tls

> kubectl get pods -n kube-system
> kubectl top nodes
> kubectl top pods
> kubectl get hpa
> kubectl autoscale deploy php-apache --cpu-percent=50 --min=1 --max=10
> kubectl delete hpa php-apache
>kubectl get hpa
#simulate the load in this application
#open other terminal window
> kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"
```

> Em outra janela cmd:

```bash
>kubectl get hpa --watch

> kubectl get po

C:\Development\Tools\KillercodeExercicios>kubectl get hpa --watch

NAME         REFERENCE               TARGETS         MINPODS   MAXPODS   REPLICAS   AGE

php-apache   Deployment/php-apache   cpu: 119%/50%   1         10        1          16m

C:\Development\Tools\KillercodeExercicios>kubectl get po

NAME                         READY   STATUS    RESTARTS   AGE

load-generator               1/1     Running   0          32s

php-apache-d87b7ff46-2rq99   1/1     Running   0          18s

php-apache-d87b7ff46-5fspk   1/1     Running   0          18s

php-apache-d87b7ff46-5pg48   1/1     Running   0          26m

php-apache-d87b7ff46-tns5l   1/1     Running   0          3s

Ctrl + c na outra janela

> kubectl delete -f deploy.yaml

> kubectl delete hpa php-apache

> kubectl delete po load-generator
```

### [9. Crie um serviço do tipo NodePort para expor externamente um Deployment chamado "webapp". Acesse o serviço usando o endereço IP do Minikube e a porta atribuída.]

```bash
> code first-pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
  labels:
    app: webapp
spec:
  containers:
    - name: webapp
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
    app: webapp #the same label used in the pod
  ports:
    - name: http
      port: 80
      nodePort: 30090
  type: NodePort
```

```bash
> kubectl apply -f first-pod.yaml
> kubectl apply -f my-first-service.yaml
> kubectl get all
> minikube service webapp
```

> A page will be opened in the browser:ex: http://127.0.0.1:62753/

- Usando o minkube no windows, esse foi o primeiro problema que enfrentei. Por que a rede é limitada ao usar o driver do docker no windows, e o NodeIP não pode ser acessado diretamente, como por exemplo http:<minikubei_p>:30080.

### [10. Crie um pod chamado "restart-pod" com a política de reinício configurada como "OnFailure". Provoque uma falha no pod e observe seu comportamento.]

```bash
> code restart.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: restart-pod
spec:
  containers:
    - name: restart-pod
      image: busybox
      command: ["sh", "-c", "exit 1"]
  restartPolicy: OnFailure
```

```bash
>kubectl get po

#O pod vai continuar reiniciando

NAME                      READY   STATUS             RESTARTS      AGE

restart-pod               0/1     CrashLoopBackOff   3 (24s ago)   77s

>kubectl delete po restart-pod
```
