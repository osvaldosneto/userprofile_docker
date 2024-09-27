# Guia para Subir os Containers com Docker e Docker Compose

## Descrição

Este projeto inclui uma aplicação frontend Angular e um backend Spring Boot, ambos configurados para serem executados em containers Docker. O Docker Compose é utilizado para facilitar o gerenciamento dos serviços, permitindo subir a aplicação completa com um único comando.

## Requisitos

Para executar os containers, certifique-se de ter os seguintes softwares instalados:

- **Docker**: [Instale o Docker](https://docs.docker.com/get-docker/)
- **Docker Compose**: Normalmente já vem incluído com o Docker Desktop, mas você pode verificar a instalação separadamente [aqui](https://docs.docker.com/compose/install/).

## Estrutura dos Containers

O projeto está configurado com os seguintes serviços:

- **Frontend (Angular)**: Executa o frontend da aplicação usando Nginx para servir os arquivos estáticos.
- **Backend (Spring Boot)**: Executa o backend da aplicação, fornecendo a API RESTful para comunicação com o frontend.

## Configuração do Docker Compose

Os serviços são definidos no arquivo `docker-compose.yml`. Abaixo está um exemplo simplificado da configuração:

```yaml
version: '3.3'

services:
  backend:
    restart: always
    image: osvaldosneto/userprofile-back:latest
    container_name: userprofile-back
    ports:
      - "8080:8080"
    networks:
      - userprofile-network

  frontend:
    restart: always
    image: osvaldosneto/userprofile-front:latest
    container_name: userprofile-front
    ports:
      - "80:80"
    networks:
      - userprofile-network
    deploy:
      resources:
        limits:
          memory: 1g
          cpus: "0.5"
    environment:
      - NODE_OPTIONS=--max_old_space_size=512

networks:
  userprofile-network:
    driver: bridge
```

## Como Subir os Containers

### Clone o Repositório:

Se ainda não tiver o repositório, clone-o usando:
```bash
git clone https://github.com/osvaldosneto/userprofile_docker.git
cd seu-repositorio
```

### Suba os Containers com Docker Compose:

Com o Docker Compose, você pode subir todos os serviços definidos no docker-compose.yml com um único comando:

```bash
docker-compose up -d
```

### Verificar o Status dos Containers:

Para garantir que os containers subiram corretamente, utilize:

```bash
docker-compose ps
```

### Acessar a Aplicação:

Frontend: Acesse o frontend em http://localhost ou http://seu-ip na porta 80.
Backend: O backend estará acessível em http://localhost:8080 ou http://seu-ip:8080.
