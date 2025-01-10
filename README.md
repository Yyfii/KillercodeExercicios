# KILLERCODE | KUBERNETES | DESAFIO

- :white_check_mark: **1**. Crie um pod chamado "my-pod" usando uma imagem simples como "nginx" e verifique seu estado com os comandos de monitoramento do Kubernetes.
- :white_check_mark: **2**. Implante um Deployment chamado "my-deployment" com três réplicas de uma aplicação baseada na imagem "httpd". Atualize a imagem do Deployment para uma versão mais recente.
- :white_check_mark: **3**. Crie um ConfigMap chamado "app-config" com uma variável de configuração personalizada. Monte o ConfigMap em um pod e verifique se o valor foi aplicado corretamente.
- :white_check_mark: **4**. Crie um Secret chamado "app-secret" contendo informações sensíveis. Injete o Secret como uma variável de ambiente em um pod e teste se está acessível.
- :white_check_mark: **5**. Configure um PersistentVolume de 1Gi de armazenamento local e vincule-o a um PersistentVolumeClaim. Monte o volume em um pod e salve arquivos para verificar a persistência.
- :white_check_mark: **6**. Crie um serviço do tipo ClusterIP para um Deployment chamado "backend" e teste a conectividade interna entre pods usando o nome do serviço.
- :white_check_mark: **7**. Implante um Job chamado "batch-job" que execute um comando simples e termine. Verifique os logs do Job para confirmar sua execução.
- :white_check_mark: **8**. Crie um Horizontal Pod Autoscaler para um Deployment chamado "hpa-deployment" e configure-o para escalar com base no uso de CPU. Aumente a carga e observe o escalonamento.
- :white_check_mark: **9**. Crie um serviço do tipo NodePort para expor externamente um Deployment chamado "webapp". Acesse o serviço usando o endereço IP do Minikube e a porta atribuída.
- :white_check_mark: **10**. Crie um pod chamado "restart-pod" com a política de reinício configurada como "OnFailure". Provoque uma falha no pod e observe seu comportamento.

### 1. Crie um pod chamado "my-pod" usando uma imagem simples como "nginx" e verifique seu estado com os comandos de monitoramento do Kubernetes.

### 2. Implante um Deployment chamado "my-deployment" com três réplicas de uma aplicação baseada na imagem "httpd". Atualize a imagem do Deployment para uma versão mais recente.

### 3. Crie um ConfigMap chamado "app-config" com uma variável de configuração personalizada. Monte o ConfigMap em um pod e verifique se o valor foi aplicado corretamente.

### 4. Crie um Secret chamado "app-secret" contendo informações sensíveis. Injete o Secret como uma variável de ambiente em um pod e teste se está acessível.

### 5. Configure um PersistentVolume de 1Gi de armazenamento local e vincule-o a um PersistentVolumeClaim. Monte o volume em um pod e salve arquivos para verificar a persistência.

### 6. Crie um serviço do tipo ClusterIP para um Deployment chamado "backend" e teste a conectividade interna entre pods usando o nome do serviço.

### 7. Implante um Job chamado "batch-job" que execute um comando simples e termine. Verifique os logs do Job para confirmar sua execução.

### 8. Crie um Horizontal Pod Autoscaler para um Deployment chamado "hpa-deployment" e configure-o para escalar com base no uso de CPU. Aumente a carga e observe o escalonamento.

### 9. Crie um serviço do tipo NodePort para expor externamente um Deployment chamado "webapp". Acesse o serviço usando o endereço IP do Minikube e a porta atribuída.

### 10. Crie um pod chamado "restart-pod" com a política de reinício configurada como "OnFailure". Provoque uma falha no pod e observe seu comportamento.
