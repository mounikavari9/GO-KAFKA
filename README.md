# Go Kafka Producer-Consumer

This project demonstrates a simple **event-driven architecture** using **Go (Golang)** and **Apache Kafka**.

A REST API acts as a **producer** that accepts comment data and publishes it to a Kafka topic.  
A worker service acts as a **consumer** that reads messages from Kafka and processes them asynchronously.

---

## Tech Stack

- Go (Golang)
- Apache Kafka
- Sarama (Kafka client for Go)
- Fiber (REST API framework)
- Docker & Docker Compose

---

## Architecture

Client → Producer API → Kafka Topic → Worker (Consumer)

- Producer exposes a REST endpoint to publish messages  
- Kafka stores messages in a topic  
- Worker consumes messages from Kafka and processes them  

---

## Project Structure
GO-KAFKA/
├── producer/
│ └── producer.go
├── worker/
│ └── worker.go
├── docker-compose.yml
├── go.mod
├── go.sum
└── README.md

## Setup & Run
1. Start Kafka using Docker

From the project root:
docker compose up -d

Verify containers are running:
docker ps

You should see:
kafka container
zookeeper container

2. Run the worker (consumer)
go run worker/worker.go

You should see:
consumer started

3. Run the producer (REST API)
go run producer/producer.go

The server will start on:
http://localhost:3000

## API Usage
Publish a comment

Endpoint:
POST /api/v1/comment

Example:
curl --location --request POST 'http://localhost:3000/api/v1/comment' \
--header 'Content-Type: application/json' \
--data-raw '{ "text":"message 1" }'

Sample Output
Producer:
Message is stored in topic(comment)/partition(0)/offset(0)

Worker:
Received message count: 1 | Topic(comment) | Message({"text":"message 1"})

---
## Learning Outcomes

Implement Kafka producer and consumer in Go
Build REST APIs using Fiber
Use Sarama to interact with Kafka
Run Kafka using Docker
Understand event-driven microservice architecture

---
## Future Enhancements

Add database storage in worker
Implement consumer groups
Add retry and error handling
Add structured logging
Support multiple partitions
