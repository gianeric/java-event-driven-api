# Java Event-Driven API
Backend application built with Java and Spring Boot to study **event-driven architecture**, **RabbitMQ producers and consumers**, and data persistence using **MongoDB and SQL Server**.

The project demonstrates how a Spring Boot application can publish and consume messages through RabbitMQ and persist orders in both NoSQL and relational databases.

## 🛠️ Technologies

- Java
- Spring Boot
- RabbitMQ
- MongoDB
- SQL Server
- Docker

---

## 🐳 Docker

### RabbitMQ

Run the RabbitMQ community Docker image with the management interface enabled:

```bash
docker run -it --rm --name rabbitmq \
  -p 5672:5672 \
  -p 15672:15672 \
  rabbitmq:3-management
```

RabbitMQ Management Interface:

`http://localhost:15672`

### MongoDB

Run MongoDB:

```bash
docker run --name mongodb-container \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=admin \
  mongo
```

### SQL Server

Run SQL Server:

```bash
docker run --name sqlserver-container \
  -e "ACCEPT_EULA=Y" \
  -e "SA_PASSWORD=@Password123" \
  -p 1433:1433 \
  -d mcr.microsoft.com/mssql/server:2017-latest
```

---

# 🐇 RabbitMQ

The application exposes endpoints for producing and consuming messages through RabbitMQ.

## Running the Spring Boot application

<p align="center">
  <img src="https://imgur.com/4xeVTJb.gif" width="800" title="Running the Spring Boot application">
</p>

## Producing a message

Send an order to the RabbitMQ queue:

**POST**

`http://localhost:8080/servico-rabbitmq/v1/pedidos`

The queue used by this application is also shared with the Node.js version of the project. The queue is named `pedidos_node`.

<p align="center">
  <img src="https://imgur.com/pxDI2Tq.gif" width="800" title="Producing a RabbitMQ message">
</p>

## Consuming messages

Retrieve messages consumed from the RabbitMQ queue:

**GET**

`http://localhost:8080/servico-rabbitmq/v1/pedidos`

The queue used by this application is also shared with the Node.js version of the project and is named `pedidos_node`.

<p align="center">
  <img src="https://imgur.com/kOmv851.gif" width="800" title="Consuming a RabbitMQ message">
</p>

---

# 🍃 MongoDB

The project also demonstrates persistence of orders using MongoDB.

## Get all orders

**GET**

`http://localhost:8080/servico-mongo/v1/pedidos`

## Get order by ID

**GET**

`http://localhost:8080/servico-mongo/v1/pedidos/1`

## Create an order

**POST**

`http://localhost:8080/servico-mongo/v1/pedidos`

Request body:

```json
{
  "id": "1",
  "codigoPedido": "1",
  "dadosPessoa": "[{nome: Gian Eric}, {dataNascimento: 2000-01-01}]",
  "dataPedido": "2021-01-01",
  "nomePedido": "Ordem de Serviço 1",
  "tipoPedido": "Ordem",
  "itensPedido": "[{descricao: Instalação do motor de arranque}, {descricao: Instalação do amortecedor}, {descricao: Troca da bomba de gasolina}]"
}
```

## Delete an order

**DELETE**

`http://localhost:8080/servico-mongo/v1/pedidos/1`

---

# 🗄️ SQL Server

The project also provides endpoints for working with orders stored in SQL Server.

## Get all orders

**GET**

`http://localhost:8080/servico-sql/v1/pedidos`

## Create an order

**POST**

`http://localhost:8080/servico-sql/v1/pedidos`

Request body:

```json
{
  "codigoPedido": "",
  "pessoaPedido": {
    "nomePessoa": "Gian Eric",
    "dataNascimentoPessoa": "1993-10-21"
  },
  "numeroPedido": "3",
  "dataPedido": "2021-01-01",
  "nomePedido": "Pedido de Manutenção",
  "tipoPedido": "Ordem",
  "pedidoItens": {
    "codigoPedidoItem": "",
    "descricao": "Instalação da manopla",
    "valor": "41.78"
  }
}
```

---

## 📚 Purpose

This project was created as a hands-on study of:

- REST APIs with Spring Boot
- RabbitMQ producers and consumers
- Asynchronous message processing
- NoSQL persistence with MongoDB
- Relational persistence with SQL Server
- Running infrastructure dependencies with Docker
- Integrating different backend technologies
