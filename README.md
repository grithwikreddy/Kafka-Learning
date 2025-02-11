# Kafka Producer-Consumer Application in Spring Boot

## Overview
This project demonstrates how to configure and implement a Kafka Producer-Consumer system using **Spring Boot**. The application runs on a single instance where both the **producer** sends messages and the **consumer** receives them using **Apache Kafka**. Kafka is configured to run on **port 9092**.

## Features
- Kafka **Producer** sends event messages to a Kafka topic.
- Kafka **Consumer** listens to the topic and processes the incoming messages.
- Single Spring Boot application containing both producer and consumer logic.
- Uses **Spring Kafka** for seamless integration with Apache Kafka.

## Technologies Used
- **Spring Boot**
- **Spring Kafka**
- **Apache Kafka (port 9092)**
- **Maven**
- **Java 17+**

## Installation and Setup
### Prerequisites
Ensure you have the following installed and running:
- **Apache Kafka** (Port: **9092**)
- **Zookeeper** (Port: **2181**)
- **Java 17+**
- **Maven**


## Kafka Configuration
The application is configured to connect to Kafka running on **localhost:9092**.

### Kafka Producer Configuration (`application.properties`)
```properties
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.producer.key-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.producer.value-serializer=org.apache.kafka.common.serialization.StringSerializer
```

### Kafka Consumer Configuration (`application.properties`)
```properties
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.consumer.group-id=my-group
spring.kafka.consumer.auto-offset-reset=earliest
spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.value-deserializer=org.apache.kafka.common.serialization.StringDeserializer
```

## Example Usage
### Sending a Kafka Message (Producer)
```java
@Autowired
private KafkaTemplate<String, String> kafkaTemplate;

public void sendMessage(String message) {
    kafkaTemplate.send("my-topic", message);
}
```

### Receiving a Kafka Message (Consumer)
```java
@KafkaListener(topics = "my-topic", groupId = "my-group")
public void listen(String message) {
    System.out.println("Received Message: " + message);
}
```

## Testing the Application
1. **Send a message using Postman or API call**
   ```http
   POST /send-message
   Content-Type: application/json
   Body: {"message": "Hello, Kafka!"}
   ```

2. **Check consumer logs for received messages.**
   ```sh
   Received Message: Hello, Kafka!
   ```
