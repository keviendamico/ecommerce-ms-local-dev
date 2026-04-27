# ecommerce-ms-local-dev

Local development infrastructure for the ecommerce microservices pipeline. Runs a Kafka cluster and supporting services via Docker Compose.

## What's included

| Service | URL |
|---------|-----|
| Kafka brokers | `localhost:9092`, `localhost:9093`, `localhost:9094` |
| Schema Registry | `http://localhost:8082` |
| Kafka UI | `http://localhost:8081` |
| Mailpit (SMTP) | `localhost:1025` |
| Mailpit (Web UI) | `http://localhost:8025` |

The Kafka cluster runs 3 brokers in KRaft mode (no ZooKeeper). Each node acts as both broker and controller.

## Setup

**1. Generate a cluster ID**

```sh
docker run --rm confluentinc/cp-kafka:7.7.8 kafka-storage random-uuid
```

**2. Create a `.env` file**

```sh
cp .env.example .env
# paste the generated value into CLUSTER_ID
```

**3. Start**

```sh
docker compose up -d
```

**4. Stop**

```sh
docker compose down
```

To also remove volumes (wipes all Kafka data):

```sh
docker compose down -v
```

## Notes

- This repo is infrastructure only. No application services are defined here.
- Spring Cloud Config Server (`ecommerce-ms-config-server`) is part of this stack and must be running before starting the application services.
- Do not add `docker-compose.yml` files to individual service repos — all local infrastructure lives here.