
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