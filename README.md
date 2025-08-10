# 🚀 Kafka + Zookeeper + Kafka UI Docker Setup

Este repositório contém uma configuração Docker Compose para executar um ambiente Kafka com Zookeeper e Kafka UI, incluindo autenticação SASL/PLAIN.

## 📋 Estrutura do Projeto

```
.
├── docker-compose.yml
└── secrets
    ├── client.properties
    ├── kafka_jaas.conf
    └── zookeeper_jaas.conf
```

## 🛠 Componentes

- **Zookeeper**: Gerenciamento de coordenação do cluster Kafka
  - Porta: 2181
  - Autenticação SASL habilitada

- **Kafka**: Broker Kafka com três listeners:
  1. `INTERNAL` (PLAINTEXT, 29092) - Comunicação interna entre brokers
  2. `INTERNAL_SASL` (SASL_PLAINTEXT, 29093) - Para Kafka UI e containers internos
  3. `EXTERNAL_SASL` (SASL_PLAINTEXT, 9092) - Para clientes externos

- **Kafka UI**: Interface web para gerenciamento e monitoramento
  - Acessível em: http://localhost:8080

## 🔧 Pré-requisitos

- Docker
- Docker Compose

## 🚀 Como Executar

1. Clone o repositório:
   ```bash
   git clone https://github.com/rafaelderoncio/docker-kafka-cluster-sasl.git
   cd ./docker-kafka-cluster-sasl
   ```

2. Inicie os serviços:
   ```bash
   docker-compose up -d
   ```

3. Acesse o Kafka UI:
   ```
   http://localhost:8080
   ```

## 🔒 Configuração de Segurança

O Kafka está configurado com autenticação SASL/PLAIN usando as credenciais:
- Usuário: `admin`
- Senha: `admin-secret`

## 🌐 Conectividade

- **Clientes externos**: Use `localhost:9092` com SASL/PLAIN
- **Clientes internos**: Use `kafka:29093` com SASL/PLAIN
- **Comunicação entre brokers**: Usa `kafka:29092` (PLAINTEXT)

## ⚙️ Configurações Avançadas

Os arquivos de configuração estão no diretório `secrets`:
- `zookeeper_jaas.conf`: Configuração JAAS para Zookeeper
- `kafka_jaas.conf`: Configuração JAAS para Kafka
- `client.properties`: Propriedades para clientes Kafka

## 🛑 Parando os Serviços

```bash
docker-compose down
```

## 📚 Documentação Adicional

- [Kafka Documentation](https://kafka.apache.org/documentation/)
- [Kafka UI GitHub](https://github.com/provectus/kafka-ui)

## 📝 Notas

- Este setup é para desenvolvimento/local. Para produção, considere:
  - Configurações de segurança adicionais
  - Replicação adequada
  - Monitoramento
  - Backup de dados

## 🤝 Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou pull requests.