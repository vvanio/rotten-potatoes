Passo para criação do Cluster:
1. Criar o Dockerfile

2. Construir a imagem v1

    docker build -t vvanio/rotten-potatoes:v1 .

3. Fazer o push para o dockerhub

    docker push vvanio/rotten-potatoes:v1

4. Criar a imagem latest e fazer o push

    docker tag vvanio/rotten-potatoes:v1 vvanio/rotten-potatoes:latest

    docker push vvanio/rotten-potatoes:latest

5. Criar o cluster

    k3d cluster create mycluster --servers 1 --agents 2 -p "8080:30000@loadbalancer"

    kubectl get nodes (para visualizar os nodes criados)

6. Criar os manifests do Kubernets (pasta k8s)

7. Criar a pasta mongodb e o respectivo deployment.yaml

8. Aplicar o deployment

    kubectl apply -f ./k8s/mongodb/deployment.yaml

    kubectl get pods (para visualizar os pods criados)

    kubectl get deployments (para visualizar os deployments)

9. Criar o service.yaml e aplicar o service

    kubectl apply -f ./k8s/mongodb/service.yaml

    kubectl get all (para visualizar todos os objetos)

10. Criar a pasta web e o respectivo deployment.yaml

11. Aplicar o deployment

    kubectl apply -f ./k8s/web/deployment.yaml

12. Criar o service.yaml e aplicar o service

    kubectl apply -f ./k8s/web/service.yaml

13. Escalar a aplicação web para 10 replicas

    kubectl scale deployment movies --replicas 10

14. Mudar a versão do aplicativo (alterar algo no codigo e fazer o rebuild da aplicação) e atualizar o deployment

    docker build -t vvanio/rotten-potatoes:v2 .

  a. Fazer o push para o dockerhub

    docker push vvanio/rotten-potatoes:v2

  b. Criar a imagem latest e fazer o push

    docker tag vvanio/rotten-potatoes:v2 vvanio/rotten-potatoes:latest

    docker push vvanio/rotten-potatoes:latest

  c. Alterar o deployment movies

    adiconar Replicas: 10

  d. Aplicar o deployment
  
    kubectl apply -f ./k8s/web/deployment.yaml