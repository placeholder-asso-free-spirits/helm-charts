# RSS Feed Source

Simple message-driven Java application to fetch & output RSS feeds.

Currently only supports RabbitMQ.

Uses `If-Modified-Since` HTTP header using REDIS storage.

## TL;DR;

```console
$ helm install ??
```
## Configuration

The following table lists the configurable parameters of the Prometheus chart and their default values.

This application uses Spring Cloud stream, configuration can be found [there](https://docs.spring.io/spring-cloud-stream/docs/current/reference/htmlsingle/#_configuration_options).

Logging override etc...

For example, to have this application DEBUG output add

```yml
applicationConfig:
    logging:
        level:
            fr:
                asso:
                    placeholder: DEBUG
```

The key `applicationConfig` can hold all the `application.yml` config for Spring. Below are the common / required ones.

Parameter | Description | Default
--------- | ----------- | -------
`image.repository` | Image to use | `127.0.0.1:34309/data-source-rss`
`image.pullPolicy`| Container image pull policy | `IfNotPresent`
`applicationConfig.*`| Everything there will be created as a ConfigMap | `acquisition-in`
`applicationConfig.spring.cloud.stream.bindings.input.destination`| Queue to listen to | `acquisition-in`
`applicationConfig.spring.cloud.stream.bindings.input.group`| Consumer group to use | `data-source-rss`
`applicationConfig.spring.cloud.stream.bindings.input.binder`| Binder to use | `rabbit` is the only one supported
`applicationConfig.spring.cloud.stream.bindings.output.destination`| Queue to output data to | `acquisition-out`
`applicationConfig.spring.cloud.stream.rabbit.bindings.input.consumer.bindingRoutingKey`| *RabbitMQ* Consumer routing key | `acquisition-out`
`applicationConfig.spring.cloud.stream.rabbit.bindings.output.producer.bindingRoutingKey`| *RabbitMQ* Producer routing key | `rss`
`applicationConfig.spring.cloud.stream.rabbit.bindings.output.producer.routing-key-expression`| *RabbitMQ* Producer routing key | `rss`
`applicationConfig.spring.cloud.stream.binders.rabbit.environment.spring.rabbitmq.host`| *RabbitMQ* host | `localhost`
`applicationConfig.spring.cloud.stream.binders.rabbit.environment.spring.rabbitmq.port`| *RabbitMQ* port | `5672`
`applicationConfig.spring.cloud.stream.binders.rabbit.environment.spring.rabbitmq.username`| *RabbitMQ* username | `admin`
`applicationConfig.spring.cloud.stream.binders.rabbit.environment.spring.rabbitmq.password`| *RabbitMQ* password | `admin`
`applicationConfig.spring.cloud.stream.binders.rabbit.environment.spring.rabbitmq.virtual-host`| *RabbitMQ* virtual-host | `/`
`applicationConfig.spring.redis.host`| Redis host | `localhost`
`applicationConfig.spring.redis.port`| Redis port | `localhost`
