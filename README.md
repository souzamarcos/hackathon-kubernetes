# Tech Challenge Kubernetes
Repositório com a configuração do kubernetes


# Deploy
Para realizar um novo deploy basta mergear a PR na branch `main`.


# Info
Foram executado os seguintes etapas para configurar o cluster Kubernetes para o funcionamento da aplicação:

1 - Criação da secret `mysql-secret` com as informações de conexão com a base de dados RDS. Obs: credenciais omitidas por questão de segurança 

```bash
kubectl create secret generic mysql-secret --from-literal=url='jdbc:mysql://<HOST>:3306/burger' --from-literal=username='<USER>' --from-literal=password='<PASSWORD>'
```
