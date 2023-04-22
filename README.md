# Microsserviço ChatService

O microsserviço ChatService interage com o ChatGPT através da API da OpenAI, fazendo o armazenamento do histórico de mensagens dos chats no MySQL.

## Instalando os pré-requisitos

Go 1.20\
https://go.dev/dl/

Docker\
https://docs.docker.com/get-docker/

sqlc
```bash
sudo snap install sqlc
```

migrate para Go
```bash
curl -s https://packagecloud.io/install/repositories/golang-migrate/migrate/script.deb.sh | sudo bash
sudo apt-get update
sudo apt-get install migrate
```

protoc\
https://grpc.io/docs/protoc-installation/

## Como executar o projeto

Faça uma cópia do arquivo `env.example` com o nome de `.env` dentro da pasta `chatservice`. Informe a sua API Key da OpenAI em `OPENAI_API_KEY` dentro do arquivo `.env`. Você pode obter uma API Key da OpenAI [clicando aqui](https://platform.openai.com/account/api-keys).

### Usando o Docker

```bash
cd pasta/do/projeto/chatservice
docker-compose up -d
```
> *Se você optar por executar o microserviço chatservice utilizando o Docker, certifique-se de alterar o valor de DB_HOST para `DB_HOST=mysql` dentro do seu arquivo `.env`*

### Executando localmente

```bash
cd pasta/do/projeto/chatservice
go run .\cmd\chatservice\main.go
```

> *Se você optar por executar o microserviço chatservice localmente, certifique-se de alterar o valor de DB_HOST para `DB_HOST=localhost` dentro do seu arquivo `.env`*

### migrate

Na primeira execução será necessário aplicar o `migrate` para fazer a criação das tabelas no banco de dados MySQL, através do `Makefile`.

```bash
cd pasta/do/projeto/chatservice
make migrate
```
> *Ao fazer `make migrate` certifique-se de que a connection string do MySQL dentro do arquivo `Makefile` aponta para *mysql:3306* quando o chatservice estiver executando no Docker, ou *localhost:3306* quando o chatservice estiver executando localmente.*

### Sobre o pacote tiktoken-go

Será necessário compilar o tiktoken-go dentro do projeto caso rode localmente.
