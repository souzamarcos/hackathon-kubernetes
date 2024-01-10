# Tech Challenge Kubernetes
Repositório com a configuração do kubernetes

# Repositórios relacionados
* [Aplicação](https://github.com/souzamarcos/tech-challenge-fast-food)
* [Infraestrutura Terraform](https://github.com/souzamarcos/tech-challenge-terraform)
* [Configuração do Kubernetes](https://github.com/souzamarcos/tech-challenge-kubernetes)
* [Lambda de Autenticação](https://github.com/souzamarcos/tech-challenge-authentication-lambda)

# Deploy
Processo de deploy do kubernetes nos ambientes de [Produção](#produção) ou [Local](#local).


## Produção
Para atualizar o ambiente de prod basta atualizar os arquivos na pasta [prod](/prod/) e mergear a PR na branch `main`.


### Configuração Inicial
É necessário as seguintes etapas para configurar o cluster Kubernetes para o funcionamento da aplicação:

1 - Criação da secret `mysql-secret` com as informações de conexão com a base de dados RDS. Obs: credenciais omitidas por questão de segurança 

```bash
kubectl create secret generic mysql-secret --from-literal=url=jdbc:mysql://<HOST>:3306/burger --from-literal=username=<USER> --from-literal=password=<PASSWORD>
```


## Local
Para configurar a aplicação no kubernetes local **execute os comandos abaixo na raiz do projeto**:

1 - Iniciar base de dados através do comando abaixo na raíz do projeto [tech-challenge-fast-food](https://github.com/souzamarcos/tech-challenge-fast-food).
Para mais informações basta executar depedências presentes no [README.md](https://github.com/souzamarcos/tech-challenge-fast-food/blob/main/README.md#executando-somente-depend%C3%AAncias).

``` bash
docker-compose -f docker-compose-without-application.yml up --build
```

2 - Procurar o IP da máquina através do comando:

Windows
```bash
ipconfig
```
Linux | Mac
```bash
ifconfig
```


3 - Crie as as secrets e defina a URL da base de dados. **No comando abaixo substitua o texto `<HOST>` pelo ip da máquina consultado na etapa acima**. Caso decida usar uma base MySql em outro local, coloque o endereço da mesma.
```bash
kubectl create secret generic mysql-secret --from-literal=url=jdbc:mysql://<HOST>:3306/burger --from-literal=username=user --from-literal=password=password
```

4 - Aplique os outros recursos do kubernetes
```bash
kubectl apply -f prod -R
```

A aplicação estará disponível no endereço [http://localhost/swagger](http://localhost/swagger).


> Obs: Caso queira remover todos os recursos criados execute os comandos abaixo:
>```bash
>kubectl apply -f prod -R
>kubectl delete secret mysql-secret 
>```
