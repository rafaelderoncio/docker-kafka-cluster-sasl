# 🚀 Kafka CLI Cheat Sheet

Comandos úteis para gerenciamento de tópicos, produção e consumo de mensagens em um cluster Kafka com autenticação SASL.

## 📌 Comandos Básicos de Tópicos

### Criar Tópico
```bash
kafka-topics \
  --create \
  --bootstrap-server kafka:29093 \
  --topic meutopico \
  --partitions 3 \
  --replication-factor 1 \
  --command-config /etc/kafka/client.properties
```

### Listar Tópicos
```bash
kafka-topics \
  --list \
  --bootstrap-server kafka:29093 \
  --command-config /etc/kafka/client.properties
```

### Descrever Tópico
```bash
kafka-topics \
  --describe \
  --topic meutopico \
  --bootstrap-server kafka:29093 \
  --command-config /etc/kafka/client.properties
```

### Apagar Tópico
```bash
kafka-topics \
  --delete \
  --topic meutopico \
  --bootstrap-server kafka:29093 \
  --command-config /etc/kafka/client.properties
```

## 📨 Produção e Consumo

### Publicar Mensagens
```bash
kafka-console-producer \
  --broker-list kafka:29093 \
  --topic meutopico \
  --producer.config /etc/kafka/client.properties
```

### Consumir Mensagens (do início)
```bash
kafka-console-consumer \
  --bootstrap-server kafka:29093 \
  --topic meutopico \
  --from-beginning \
  --group meu-grupo \
  --consumer.config /etc/kafka/client.properties
```

## 👥 Gerenciamento de Grupos

### Descrever Grupo de Consumidores
```bash
kafka-consumer-groups \
  --group meu-grupo \
  --describe \
  --bootstrap-server kafka:29093 \
  --command-config /etc/kafka/client.properties
```

## 🔍 Inspeção do Cluster

### Verificar Brokers
```bash
kafka-broker-api-versions \
  --bootstrap-server kafka:29093 \
  --command-config /etc/kafka/client.properties
```

## 🔐 Observações de Segurança

- Todos os comandos usam autenticação SASL configurada em `/etc/kafka/client.properties`
- O listener `kafka:29093` está configurado com SASL_PLAINTEXT
- Certifique-se de que o arquivo `client.properties` contém as credenciais corretas

## 💡 Dicas

1. Para consumir em tempo real (sem `--from-beginning`), remova a flag
2. Use `--property print.key=true` no consumer para ver chaves das mensagens
3. Adicione `--property print.partition=true` para ver informações de partição

```bash
kafka-console-consumer \
  --bootstrap-server kafka:29093 \
  --topic meutopico \
  --property print.key=true \
  --property print.partition=true \
  --group meu-grupo \
  --consumer.config /etc/kafka/client.properties
```

Este cheat sheet assume que você está executando os comandos de dentro de um container Kafka ou com as ferramentas Kafka instaladas localmente.