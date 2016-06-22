# TradSim

## TradSim Architectural Documentation

The following systems have been created for the following purpose

- Learning new languages
- Learning new technologies
- Learning new architectural patterns

### Languages

- Go
- C#
- F#

### Technologies

- AMQP ([RabbitMQ](http://www.rabbitmq.com/))
- RDBMS ([PostgreSQL](https://www.postgresql.org/))
- MVC 6
- SPA ([aurelia.io](http://aurelia.io/))
- [Docker](https://www.docker.com/)
- [Kubertnetes](http://kubernetes.io/)

### Architectural Patterns

- [Event Sourcing](https://msdn.microsoft.com/en-us/library/dn589792.aspx)
- [CQRS](https://msdn.microsoft.com/en-us/library/dn568103.aspx)
- Event Based Messaging
- Microservices (REST and Event Based)
- Distributed Systems


## Architecture

![Architecture](https://raw.githubusercontent.com/tradsim/tradsim-arch/master/docs/arch/tradsim%20systems.png)

## Systems

### Query Service - Client

This is the client that sends command to the command service and queries the database for the data.

- ASP.NET Core
- C#
- MVC or Aurelia (Preferable)

### Command Service

The system is responsible for sending each command to the message broker (in form of events) and to the exchange.

- Go
- Rest/HTTP service
- Event publishing

The following events are published

- OrderCreatePending
- OrderAmendPending
- OrderCancelPending

### Exchange Service

The systems tries to emulate a stock exchange. When orders are created, amended, canceled or traded events are published to the message broker.

- Go
- Rest/HTTP service
- Event publishing

The following events are published

- OrderCreated
- OrderAmended
- OrderCanceled
- OrderTraded

### Event Writer Service

The system subscribes to the message broker and writes every event to the event store. Finally it publishes a stored event to the message broker.

- Go
- Event Sourcing (writing to storage)
- Event publishing

The following events are received

- OrderCreatePending
- OrderAmendPending
- OrderCancelPending
- OrderCreated
- OrderAmended
- OrderCanceled
- OrderTraded

The following events are published

- OrderEventStored

### Event Aggregator Service

The service is responsible for getting the order events out of the event store and recalculate the order. Finally it saves the order to the orders database.

- F#
- Event Sourcing (aggregation)
- Write to Order Storage

The following events are received

- OrderEventStored

### Messaging Broker

The system brokers messages (events) between the other systems.

- RabbitMQ

### Event Storage

The events are stored to a table in the RDMBS.

- PostgreSQL
- Events

### Order storage

The database holds a relational schema describing users, orders, position etc.

- PostgreSQL
- Relational Data