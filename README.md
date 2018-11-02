# Spring Boot application with AMQP using Cloud Foudnry Service Key

### List services

```bash
cf services
Getting services in org pcfdev-org / space pcfdev-space as admin...

name      service      plan       bound apps           last operation
my-amqp   p-rabbitmq   standard   rabbitmq-perf-test   create succeeded
```

### Create a new service key for RabbitMQ service

```bash
cf create-service-key MY-SERVICE MY-KEY -c '{"permissions":"read-only"}'
Creating service key MY-KEY for service instance MY-SERVICE as me@example.com...
OK
```


### List service keys for the service

```bash
cf service-keys my-amqp
Getting keys for service instance my-amqp as admin...

name
my-amqp-service-key
```

### Obtain credentials for service key

```bash
cf service-key my-amqp my-amqp-service-key

...
   "uri": "amqp://7950db4e-0efc-4147-9455-ccb3ac514349:pa72i27dh5o72chemb7f444h4g@rabbitmq.local.pcfdev.io:5672/d2cd1f31-3855-4301-a88c-ad02b3e92817",
...
```

### Use credentials in application.properties, or serve via CredHub

```properties
spring.rabbitmq.host=rabbitmq.local.pcfdev.io
spring.rabbitmq.port=5672
spring.rabbitmq.password=pa72i27dh5o72chemb7f444h4g
spring.rabbitmq.username=7950db4e-0efc-4147-9455-ccb3ac514349
spring.rabbitmq.virtual-host=/d2cd1f31-3855-4301-a88c-ad02b3
```