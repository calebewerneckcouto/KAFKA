# API Boleto

Este projeto consiste em uma API para gerenciamento de boletos bancários, utilizando Spring Boot, Kafka e Avro para comunicação com outro serviço.

## Tecnologias Utilizadas
- **Spring Boot**: Framework Java para construção da API.
- **H2 Database**: Banco de dados em memória para armazenamento dos boletos.
- **Kafka**: Sistema de mensageria para comunicação assíncrona.
- **Avro**: Serialização de mensagens enviadas para o Kafka.
- **Swagger/OpenAPI**: Documentação interativa da API.

## Estrutura do Projeto

### 1. **Configuração do OpenAPI**
Arquivo: `OpenAPIConfig.java`
- Define as configurações da documentação da API.

### 2. **Controller**
Arquivo: `BoletoController.java`
- Endpoints para criação e consulta de boletos:
  - `GET /api/boleto/{codigoBarras}`: Busca um boleto pelo código de barras.
  - `POST /api/boleto`: Cria um novo boleto.

### 3. **Mapper**
Arquivo: `BoletoMapper.java`
- Converte entre `BoletoEntity`, `BoletoDTO` e `Avro Boleto`.

### 4. **Serviço**
Arquivo: `BoletoService.java`
- Lógica de negócio da API:
  - Criação de boletos
  - Consulta de boletos
  - Atualização de boletos
  - Envio de mensagens Kafka

### 5. **Configuração Kafka**
- `spring.kafka.bootstrapServers=localhost:19092`
- `spring.kafka.topico-boleto=solicitacao-boleto`
- `spring.kafka.topico-notificacao=notificacao-boleto`
- `spring.kafka.producer.value-serializer=io.confluent.kafka.serializers.KafkaAvroSerializer`
- `spring.kafka.consumer.value-deserializer=io.confluent.kafka.serializers.KafkaAvroDeserializer`

## Como Rodar o Projeto

1. **Clonar o repositório**
```sh
 git clone <url_do_repositorio>
 cd api-boleto
```
2. **Subir o ambiente**
```sh
 docker-compose up -d
```
3. **Executar a aplicação**
```sh
 mvn spring-boot:run
```
4. **Acessar a documentação**
Abrir no navegador: [http://localhost:8282/swagger-ui.html](http://localhost:8282/swagger-ui.html)

## Comunicação com Outro Projeto

A API `api-boleto` se comunica com outro serviço através do Kafka, enviando mensagens Avro para o tópico `solicitacao-boleto`. O outro serviço consome essas mensagens para processar os pagamentos.

## Autor
- **Calebe Werneck Couto**
- Email: calebewerneck@hotmail.com

