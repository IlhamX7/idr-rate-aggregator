# IDR Rate Aggregator

Polymorphic IDR rate aggregator built with Spring Boot.

---

## 🛠 Tech Stack

- Java 21
- Spring Boot 4
- Maven
- WebClient (Reactive)
- JUnit 5
- Mockito

---

## 🏗 Architecture Overview

### ✅ Strategy Pattern
Three different resource types are handled via polymorphism:

- `latest_idr_rates`
- `historical_idr_usd`
- `supported_currencies`

Each resource has its own `IDRDataFetcher` implementation.

The controller does not use `if` or `switch`.  
Strategy resolution is handled via Spring map injection.

---

### ✅ FactoryBean for WebClient

The external API client is created using a custom `FactoryBean<WebClient>` implementation.

This allows:
- Centralized client construction
- Externalized base URL configuration
- Clean separation of configuration responsibility

---

### ✅ Startup Data Initialization

All external data is fetched **once** during application startup using `ApplicationRunner`.

The results are stored in an immutable, thread-safe in-memory store.

No external API call is made during request handling.

---

## 📦 Setup & Run

### 1. Clone repository

```bash
git clone https://github.com/IlhamX7/idr-rate-aggregator.git
cd idr-rate-aggregator
```

### 2.️ Build

```bash
mvn clean install
```

### 3. Run

```bash
mvn spring-boot:run
```
Application runs at: http://localhost:8080

### 4. API Usage

- Supported Currencies
```bash
curl http://localhost:8080/api/finance/data/supported_currencies
```

- Latest IDR Rates
```bash
curl http://localhost:8080/api/finance/data/latest_idr_rates
```

- Historical IDR → USD
```bash
curl http://localhost:8080/api/finance/data/historical_idr_usd
``` 

### 5. Testing

Run tests:
```bash
mvn test
```

📁 Project Structure

```bash
config/
client/
controller/
exception/
model/dto/
service/
strategy/
util/
```

👨‍💻 Author
```bash
Ilham
```
