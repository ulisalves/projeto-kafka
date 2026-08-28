# Projeto Kafka com Spring Boot

Este projeto demonstra uma arquitetura simples de mensageria orientada a eventos utilizando **Apache Kafka** e **Spring Boot (Java 17)**, totalmente conteinerizada com **Docker**, que pode ser conferido nessa página [Aqui](https://www.youtube.com/watch?v=twDixr_XefI).

## 🚀 Arquitetura do Sistema

O ecossistema é composto por três componentes principais rodando em microsserviços:

1. **Producer (`sb-kafka-producer`)**: Expõe uma API REST na porta `8080`. Recebe uma requisição HTTP POST com os dados de um pagamento e envia para o tópico do Kafka.
2. **Apache Kafka (`localhost:9092`)**: O broker de mensageria central que gerencia o recebimento, o armazenamento temporário e a distribuição das mensagens.
3. **Consumer (`sb-kafka-consumer`)**: Escuta ativamente o broker na porta `8081` e processa as mensagens do tópico de pagamentos em tempo real.

---

## 🛠️ Como Executar o Projeto

### 1. Iniciar a Infraestrutura (Docker)
Na raiz do projeto (onde está o arquivo `docker-compose.yml`), execute o comando para subir o Kafka, Zookeeper e Kafdrop:
```bash
docker compose up -d
```

### 2. Verificar os Contêineres
Certifique-se de que os três serviços estão ativos (`Up`):
```bash
docker ps
```

### 3. Listar Tópicos no Terminal
Para checar se o tópico de pagamentos foi criado com sucesso dentro do contêiner:
```bash
docker exec -it kafka-local kafka-topics --bootstrap-server localhost:9092 --list
```

### 4. Executar as Aplicações Java
* Inicie a classe principal do projeto **Producer**.
* Inicie a classe principal do projeto **Consumer**.

---

## 🧪 Como Testar (Exemplo de Requisição)

Utilize o **Bruno** (ou Postman/Insomnia) para disparar uma requisição HTTP POST:

* **URL:** `http://localhost:8080/pagamentos`
* **Método:** `POST`
* **Body (JSON):**
```json
{
  "numero": 3,
  "valor": 300,
  "descricao": "Debito de compra"
}
