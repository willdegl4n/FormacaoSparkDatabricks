# 🐋 Intensivão Docker 🐳
- [Docker](#docker)
	- [Principais benefícios do Docker](#principais-benefícios-do-docker)
	- [Dockerfile](#dockerfile)
	- [Principais comandos do Docker](#principais-comandos-do-docker)
		- [Gerenciamento de Imagens](#gerenciamento-de-imagens)
		- [Gerenciamento de Containers](#gerenciamento-de-Containers)
  		- [Logs e Debugging](#logs-e-Debugging)
     		- [Opções comuns do docker run](#opcoes-comuns-do-docker-run)
       - [Dockerhub](#Dockerhub)
         	- [Como publicar imagens do Docker Hub](#Como-publicar-imagens-no-Docker-Hub)
- [Docker Compose](#Docker-Compose)
	- [Networks](#Networks)
	- [Principais comandos](#Principais-comandos)
		- [Flags comuns:](#Flags-comuns:)
	- [Adicionando comandos na inicialização](#Adicionando-comandos-na-inicialização)
   		1. [Usando o comando command](#Usando-o-comando-command)
   		2. [Usando entrypoint](#Usando-entrypoint)
   		3. [Usando scripts de inicialização](#Usando-scripts-de-inicialização)
   		4. [Usando depends_on com condition](#Usando-depends_on-com-condition)

## Docker

Docker é uma plataforma de virtualização de containers que permite empacotar, distribuir e executar aplicações de forma isolada e consistente. 
Diferente das máquinas virtuais tradicionais, containers Docker compartilham o kernel do sistema operacional host, tornando-os mais leves e eficientes.

## Principais benefícios do Docker

- **Isolamento**: Cada container roda de forma isolada, com seus próprios processos, redes e sistemas de arquivos
- **Portabilidade**: "Build once, run anywhere" - containers podem ser executados em qualquer ambiente que tenha Docker instalado
- **Eficiência**: Containers são mais leves que VMs tradicionais e iniciam mais rapidamente
- **Escalabilidade**: Facilita a criação e gerenciamento de múltiplas instâncias da aplicação

## Dockerfile

Dockerfile é um arquivo de texto que contém todas as instruções necessárias para criar uma imagem Docker.

- A imagem base a ser utilizada
- Comandos a serem executados durante a construção
- Arquivos a serem copiados para dentro da imagem
- Portas a serem expostas
- Comando padrão a ser executado quando o container iniciar

```dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]

```

## Principais comandos do Docker
Aqui estão os comandos mais utilizados no dia a dia com Docker:

## Gerenciamento de Imagens
* `docker build .` - Constrói uma imagem a partir de um Dockerfile
* `docker pull [imagem]` - Baixa uma imagem do Docker Hub
* `docker images` - Lista todas as imagens locais
* `docker rmi [imagem]` - Remove uma imagem específica

## Gerenciamento de Containers
* `docker run [imagem]` - Cria e inicia um novo container
* `docker ps` - Lista containers em execução
* `docker ps -a` - Lista todos os containers (incluindo parados)
* `docker start [container]` - Inicia um container existente
* `docker stop [container]` - Para um container em execução
* `docker rm [container]` - Remove um container

## Logs e Debugging
* `docker logs [container]` - Exibe logs do container
* `docker exec -it [container] bash` - Acessa o terminal do container

## Opções comuns do docker run
* `-d` - Executa em modo detached (background)
* `-p [host-port]:[container-port]` - Mapeia portas
* `-v [host-path]:[container-path]` - Monta volumes
* `--name [nome]` - Define um nome para o container
* `-t` - Define uma tag/nome para a imagem durante o build ou execução

## Dockerhub
[hub.docker.com](https://hub.docker.com/search?badges=official)
​

O Docker Hub é o registro público oficial de imagens Docker - um repositório centralizado onde você pode encontrar, compartilhar e distribuir 
imagens Docker. Funciona de forma similar ao GitHub, mas para imagens Docker.
* Repositório oficial de imagens base e populares
* Possibilidade de criar repositórios públicos e privados
* Integração com sistemas de CI/CD
* Controle de versões de imagens através de tags

## Como publicar imagens no Docker Hub
Para publicar suas próprias imagens no Docker Hub, siga estes passos:
1. Crie uma conta no Docker Hub [hub.docker.com](hub.docker.com)
2. Faça login via terminal: `docker login`
3. Tagueie sua imagem: `docker tag local-image:tag username/repository:tag`
4. Envie a imagem: `docker pushusername/repository:tag`

````dockerfile
docker build -t minha-app .
docker tag minha-app fernandakipper/minha-app:1.0
docker push fernandakipper/minha-app:1.0
````

Após o push, sua imagem estará disponível no Docker Hub e poderá ser baixada por outros usuários usando o comando `docker pull username/repository:tag`.

## Docker Compose
Docker Compose é uma ferramenta para orquestrar aplicações multi-containers, permitindo definir e executar múltiplos containers Docker de forma declarativa 
através de um único arquivo YAML. Com ele, você pode configurar todos os serviços, redes e volumes necessários para sua aplicação em um único lugar, facilitando
o gerenciamento e deploy de aplicações complexas
```
services:
# Aqui a gente bota o nome do serviço (como ele vai aparecer la no terminal depois)
  backend:
    # Caminho para o dockerfile desse serviço
    build: ./nodejs-ping-pong
    # Define o mapeamento de portas que vamos fazer
    ports:
      - "3000:3000"
    # Qual o nome da rede que vamos usar
    networks:
      - app-network

  frontend:
    build: ./frontend
    ports:
      - "4200:4200"
    networks:
      - app-network

# Aqui definimos a rede que vamos usar
networks:
	# Chamando ela de app-network
  app-network:
    driver: bridge
```
​

## Networks
No Docker Compose, as networks (redes) são mecanismos que permitem que containers se comuniquem entre si. Quando você coloca dois ou mais containers na mesma rede:
* Os containers podem se comunicar diretamente usando o nome do serviço como hostname
* Eles ficam isolados de containers que estão em outras redes
* A comunicação entre eles é mais segura e eficiente
  
Por exemplo, no arquivo docker-compose.yml acima, tanto o frontend quanto o backend estão na rede 'app-network'. Isso significa que:

* O frontend pode fazer requisições para o backend usando simplesmente "http://backend:3000"
* A comunicação entre eles é isolada de outros containers que não estão nessa rede
* Não é necessário expor portas internamente entre os serviços da mesma rede
  
O driver 'bridge' é o tipo de rede padrão do Docker, criando uma rede virtual isolada para comunicação entre containers.


## Principais comandos
* `docker-compose up` - Inicia todos os serviços definidos no arquivo docker-compose.yml
* `docker-compose up --build` - Força o rebuild das imagens antes de iniciar os serviços
* `docker-compose down` - Para e remove todos os containers, redes e volumes definidos
* `docker-compose ps` - Lista todos os containers em execução do compose
* `docker-compose logs` - Exibe os logs de todos os serviços
* `docker-compose logs` [serviço] - Exibe os logs de um serviço específico
* `docker-compose stop` - Para todos os serviços sem remover os containers
* `docker-compose start` - Inicia serviços que foram parados
* `docker-compose restart` - Reinicia todos os serviços
* `docker-compose exec [serviço] [comando]` - Executa um comando em um serviço específico
* `docker-compose run [serviço] bash` - Acessa o terminal bash de um serviço específico

## Flags comuns:
* `-d` - Executa em modo detached (background)
* `--build` - Força o rebuild das imagens
  
Quando você executa o `docker-compose build` ou usa a flag `--build`, o Docker Compose irá construir todas as imagens definidas no arquivo docker-compose.yml 
que têm a instrução 'build' especificada. É similar ao comando `docker build`, mas com algumas diferenças importantes:
* O Docker Compose automaticamente constrói todas as imagens necessárias em um único comando
* Ele mantém um cache das imagens construídas e só reconstrói o que foi modificado
* O contexto de build é definido no docker-compose.yml, não sendo necessário especificar o caminho do Dockerfile manualmente

Por exemplo, no nosso docker-compose.yml acima, quando executamos `docker-compose up --build`, ele irá construir automaticamente as imagens tanto do backend 
quanto do frontend, usando os Dockerfiles especificados em seus respectivos diretórios.
* `--force-recreate` - Força a recriação dos containers
* `-f` - Especifica um arquivo compose alternativo

## Adicionando comandos na inicialização
No Docker Compose, existem várias maneiras de executar comandos durante a inicialização de um container. As principais são:

### 1. Usando o comando command
O comando 'command' substitui o CMD definido no Dockerfile:

````yaml
services:
  app:
    build: .
    command: ["npm", "run", "dev"]
````

### 2. Usando entrypoint
O 'entrypoint' permite definir um script que será executado quando o container iniciar:

````yaml
services:
  app:
    build: .
    entrypoint: ["./init-script.sh"]
````

### 3. Usando scripts de inicialização
Você pode criar um script shell e configurá-lo como entrypoint:

````yaml
#!/bin/bash
# init-script.sh
npm install
npm run migrations
npm start
````

E no docker-compose.yml:
````yaml
services:
  app:
    build: .
    entrypoint: ["./init-script.sh"]
    volumes:
      - ./init-script.sh:/init-script.sh
````
​

### 4. Usando depends_on com condition
Para garantir que serviços iniciem em uma ordem específica:
````yaml
services:
  app:
    build: .
    depends_on:
      db:
        condition: service_healthy
    command: ["npm", "start"]
  
  db:
    image: postgres
    healthcheck:
      test: ["CMD-SHELL", "pg_isready"]
      interval: 10s
      timeout: 5s
      retries: 5
````
....
