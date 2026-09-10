# Java Event-Driven API
Study of producers and consumers using queues in RabbitMQ
Study of insert orders in mongodb local

#
## Docker
Use the community image Docker from Rabbit MQ with port 15672:
> docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management

Use the community image Docker from Mongo Express with port 27017:
>docker run --name mongodb-container -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=admin mongo

Use the community image Docker from SQL Server with port 1433:
>docker run --name sqlserver-container -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=@Password123" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest


#
## RabbitMQ 
Open RabbitMQ
> <link>localhost:15672</link>

Running the Spring Boot application
<p align="center">
  <img src="https://imgur.com/4xeVTJb.gif" width="800" title="Screenshot">
</p>

Producing a message in the queue:
>POST
> <link>localhost:8080/servico-rabbitmq/v1/pedidos</link>

Note: The queue consumed is the same as for the <a href="https://github.com/gianeric/API-ServiceRabbit-nodejs">API-ServiceRabbit-nodejs</a>, we named this queue with the name "pedidos_node"
<p align="center">
  <img src="https://imgur.com/pxDI2Tq.gif" width="800" title="Screenshot">
</p>

Consuming messages from the queue:
>GET
> <link>localhost:8080/servico-rabbitmq/v1/pedidos</link>

Note: The queue consumed is the same as for the <a href="https://github.com/gianeric/API-ServiceRabbit-nodejs">API-ServiceRabbit-nodejs</a>, we named this queue with the name "pedidos_node"
<p align="center">
  <img src="https://imgur.com/kOmv851.gif" width="800" title="Screenshot">
</p>

#
## MongoDB (Orders)
Searching for orders in the NoSQL MongoDB database

GET
> <link>http://localhost:8080/servico-mongo/v1/pedidos</link>

GET ID
> <link>http://localhost:8080/servico-mongo/v1/pedidos/1</link>

#
Inserting an order in the NoSQL MongoDB database    

POST
> <link>http://localhost:8080/servico-mongo/v1/pedidos</link>
JSON
```
{
    "id":"1",
    "codigoPedido":"1",
    "dadosPessoa":"[{nome: Gian Eric}, {dataNascimento: 2000-01-01}]",
    "dataPedido":"2021-01-01",
    "nomePedido":"Ordem de Serviço 1",
    "tipoPedido":"Ordem",
    "itensPedido":"[{descricao: Instalação do motor de arranque}, {descricao: Instalação do amortecedor}, {descricao: Troca da bomba de gasolina}]"
}
```

#
DELETE ID
> <link>http://localhost:8080/servico-mongo/v1/pedidos/1</link>


#
## SQL Server (Orders)
Searching for orders in the SQL Server database

GET
> <link>http://localhost:8080/servico-sql/v1/pedidos</link>


Inserting an order in the NoSQL MongoDB database

POST
> <link>http://localhost:8080/servico-sql/v1/pedidos</link>
JSON
```
{
    "codigoPedido": "",
    "pessoaPedido": {"nomePessoa": "Gian Eric", "dataNascimentoPessoa": "1993-10-21"},
    "numeroPedido": "3",
    "dataPedido": "2021-01-01",
    "nomePedido": "Pedido de Manutenção",
    "tipoPedido": "Ordem",
    "pedidoItens": {"codigoPedidoItem": "", "descricao": "Instalação da manopla", "valor": "41.78"}
```
