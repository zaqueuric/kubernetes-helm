
https://eduardomatos.dev/fazendo-seu-primeiro-deploy-no-kubernetes/

1 - Buildar o app e enviar para o dockerhub
    docker build . -t zaqueur/visit-counter:1.0
    docker push zaqueur/visit-counter:1.0

2 - Enviar as configurações para o k8s
    kubectl apply -f .\visit-counter-deployment.yaml
    kubectl apply -f .\visit-counter-service.yaml

3 - kubectl get pods,svc

4 - Port-forward para acessar a aplicação visit-counter
kubectl port-forward service/visit-counter-service 2000:3000

5 - Testar a app localmente: http://localhost:2000/

6 - Acesso externo (LOAD BALANCER) da aplicação -> é usado o objeto ingress para o minikube por 
possuir somente um NODE, para cluster em produção além do ingress é necessário configurar 
um load balancer de modo que todo trafego passe por ele antes de chegar ao ingress.

7 - INGRESS: é dividido em duas partes -> CONFIGURAÇÕES E CONTROLLER.
    CONFIGURAÇÕES: Responsável pelas rotas, diz para qual "svc" uma req deve ser roteada
    CONTROLLER: É um "deployment" que roda uma aplicação responsável por fazer o roteamento de fato,
                Nginx e Traefik são duas opções... 
    
    7.1 - minikube addons enable ingress
    7.2 - configurar o yaml das rotas