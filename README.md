# TradSim

## TradSim Architectural Documentation

### Architectural Patterns

- [Event Sourcing](https://msdn.microsoft.com/en-us/library/dn589792.aspx)
- [CQRS](https://msdn.microsoft.com/en-us/library/dn568103.aspx)
- Event Based Messaging
- Microservices (REST and Event Based)

### Technologies

- golang
- C#
- F#
- AMQP ([RabbitMQ](http://www.rabbitmq.com/))
- RDBMS ([PostgreSQL](https://www.postgresql.org/))
- MVC 6
- SPA ([aurelia.io](http://aurelia.io/))

## Architecture

![Architecture](https://raw.githubusercontent.com/tradsim/tradsim-arch/master/docs/arch/tradsim%20systems.png)

## Systems

### Query Service - Client

- ASP.NET core 1.0
- C#
- MVC or Aurelia

### Command Service

- golang
- Rest/HTTP service
- Event publishing

### Exchange Service

- golang
- Rest/HTTP service
- Event publishing

### Event Writer Service

- golang
- Event Sourcing (writing to storage)
- Event publishing

### Event Aggregator Service

- F#
- Event Sourcing (aggregation)
- Write to Order Storage

### Messaging Broker

- RabbitMQ
- AMQP

### Event Storage

- PostgreSQL
- Events

### Order storage

- PostgreSQL
- Relational Data