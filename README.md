<!DOCTYPE html>
<html lang="pt">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>KILLERCODE | KUBERNETES | DESAFIO</title>
  <style>
    ul li a {
      color: inherit; /* Remove a cor padrão de link */
      text-decoration: none; /* Remove o sublinhado */
    }
    ul li a:hover {
      text-decoration: underline; /* Adiciona sublinhado quando o mouse passar por cima */
    }

  </style>
</head>
<body>

  <h1>KILLERCODE | KUBERNETES | DESAFIO</h1>

  <ul>
    <li><a href="#section1">:white_check_mark: 1. Crie um pod chamado "my-pod" usando uma imagem simples como "nginx" e verifique seu estado com os comandos de monitoramento do Kubernetes.</a></li>
    <li><a href="#section2">2. Implante um Deployment chamado "my-deployment" com três réplicas de uma aplicação baseada na imagem "httpd". Atualize a imagem do Deployment para uma versão mais recente.</a></li>
    <li><a href="#section3">3. Crie um ConfigMap chamado "app-config" com uma variável de configuração personalizada. Monte o ConfigMap em um pod e verifique se o valor foi aplicado corretamente.</a></li>
    <li><a href="#section4">4. Crie um Secret chamado "app-secret" contendo informações sensíveis. Injete o Secret como uma variável de ambiente em um pod e teste se está acessível.</a></li>
    <li><a href="#section5">5. Configure um PersistentVolume de 1Gi de armazenamento local e vincule-o a um PersistentVolumeClaim. Monte o volume em um pod e salve arquivos para verificar a persistência.</a></li>
    <li><a href="#section6">6. Crie um serviço do tipo ClusterIP para um Deployment chamado "backend" e teste a conectividade interna entre pods usando o nome do serviço.</a></li>
    <li><a href="#section7">7. Implante um Job chamado "batch-job" que execute um comando simples e termine. Verifique os logs do Job para confirmar sua execução.</a></li>
    <li><a href="#section8">8. Crie um Horizontal Pod Autoscaler para um Deployment chamado "hpa-deployment" e configure-o para escalar com base no uso de CPU. Aumente a carga e observe o escalonamento.</a></li>
    <li><a href="#section9">9. Crie um serviço do tipo NodePort para expor externamente um Deployment chamado "webapp". Acesse o serviço usando o endereço IP do Minikube e a porta atribuída.</a></li>
    <li><a href="#section10">10. Crie um pod chamado "restart-pod" com a política de reinício configurada como "OnFailure". Provoque uma falha no pod e observe seu comportamento.</a></li>
  </ul>

  <div id="section1">
    <h2>1. Crie um pod chamado "my-pod"</h2>
    <p>Conteúdo da seção 1...</p>
  </div>
  <div id="section2">
    <h2>2. Implante um Deployment chamado "my-deployment"</h2>
    <p>Conteúdo da seção 2...</p>
  </div>
  <div id="section3">
    <h2>3. Crie um ConfigMap chamado "app-config"</h2>
    <p>Conteúdo da seção 3...</p>
  </div>
  <div id="section4">
    <h2>4. Crie um Secret chamado "app-secret"</h2>
    <p>Conteúdo da seção 4...</p>
  </div>
  <div id="section5">
    <h2>5. Configure um PersistentVolume de 1Gi</h2>
    <p>Conteúdo da seção 5...</p>
  </div>
  <div id="section6">
    <h2>6. Crie um serviço do tipo ClusterIP</h2>
    <p>Conteúdo da seção 6...</p>
  </div>
  <div id="section7">
    <h2>7. Implante um Job chamado "batch-job"</h2>
    <p>Conteúdo da seção 7...</p>
  </div>
  <div id="section8">
    <h2>8. Crie um Horizontal Pod Autoscaler</h2>
    <p>Conteúdo da seção 8...</p>
  </div>
  <div id="section9">
    <h2>9. Crie um serviço do tipo NodePort</h2>
    <p>Conteúdo da seção 9...</p>
  </div>
  <div id="section10">
    <h2>10. Crie um pod chamado "restart-pod"</h2>
    <p>Conteúdo da seção 10...</p>
  </div>

</body>
</html>
