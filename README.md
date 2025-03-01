# Transactional Outbox Pattern with Elasticsearch and RabbitMQ in Python

This example demonstrates how to implement the Transactional Outbox Pattern using Elasticsearch and RabbitMQ in Python.

![](transactional-outbox-pattern.png)


## Running the example
```bash
docker compose build
docker compose up
```

## Info endpoints
- Producer: http://localhost:8091/info
- Relay: http://localhost:8092/info
- Consumer: http://localhost:8093/info

Use `sh monitor.sh` to monitor the status of each service and Elasticsearch/RabbitMQ availability.

## Interaction endpoints
- Add items (via producer): http://localhost:8091/add-items/10

## Scenarios

Base scenario:
1. Check the items in Elasticsearch: http://localhost:9200/auction_items/_search
2. Show queues in RabbitMQ: http://localhost:15672/#/queues (`guest`/`guest`)
3. Show results of the monitoring script.
4. Publish some items: http://localhost:8091/add-items/10
5. Observe the changes and how producer, relay, and consumer interact.

### Scenario 1: Producer is down
```bash
docker compose stop producer
docker compose start producer
```

### Scenario 2: Outbox relay is down
```bash
docker compose stop relay
docker compose start relay
```

### Scenario 3: Consumer is down
```bash
docker compose stop consumer
docker compose start consumer
```

### Scenario 4: RabbitMQ is down
```bash
docker compose stop rabbitmq
docker compose start rabbitmq
```

### Scenario 5: Elasticsearch is down
```bash
docker compose stop elasticsearch
docker compose start elasticsearch
```