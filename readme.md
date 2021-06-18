
## Comandos para configuração
### 1. Venv
```sh
python -m venv .venv
```
### 2. Install pacote
```sh
python -m pip install -r requirements.txt
```

## Comandos Utilizados
### Python
```sh
python -m venv .venv

python -m pip install -U pika
```

### Docker
```sh
docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management
```

### Scripts
#### RabbitAdmin
1. Queue
```sh
python rabbitmqadmin declare queue --vhost=/ name=some_outgoing_queue durable=true
```
2. Exchange
```sh
python rabbitmqadmin declare exchange --vhost=/ name=some_exchange type=direct
```
3. Binding
```sh
python rabbitmqadmin --vhost=/ declare binding source="some_exchange" destination_type="queue" destination="some_outgoing_queue" routing_key="some_routing_key"
```

#### Clusters
- 1. Primeiro servidor
```sh
set RABBITMQ_NODENAME=rabbit1
set RABBITMQ_NODE_PORT=5672
set RABBITMQ_SERVER_START_ARGS=-rabbitmq_management listener [{port,15672}]
rabbitmq-server start
```
- 2. Segundo Servidor
```sh
set RABBITMQ_NODENAME=rabbit2
set RABBITMQ_NODE_PORT=5673
set RABBITMQ_SERVER_START_ARGS=-rabbitmq_management listener [{port,15673}]
rabbitmq-server start
```

- 3. Juntar segundo servidor ao cluster do primeiro
```sh
rabbitmqctl -n rabbit2 stop_app
rabbitmqctl -n rabbit2 join_cluster rabbit1
rabbitmqctl -n rabbit2 start_app
```