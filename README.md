# CST8915 Lab 5: Containerizing the Algonquin Pet Store with Docker

| Student Name | Student ID | Course | Semester |
|---|---|---|---|
| Peng Wang | 041107730 | CST8915 Full-stack Cloud-native Development | Fall 2026 |

🎥 [Watch Demo Video](VIDEO_LINK)

---

## 1. The stack runs from my Docker Hub images

I containerized the Order Service, the Product Service and the Store Front, and I pushed their images to Docker Hub. The final `docker-compose.yaml` in this repository has no `build` keys. It only names images, so Compose downloads them from Docker Hub and does not need the source code.

| Service | Image | Port on the host |
|---|---|---|
| RabbitMQ | `rabbitmq:4.3.6-management` | 15672 (management UI) |
| Order Service | `zhizunbao2019/order-service:latest` | 3000 |
| Product Service (Python) | `zhizunbao2019/product-service:latest` | 3030 |
| Store Front | `zhizunbao2019/store-front:latest` | 8080 |

This command lists the running containers, and the IMAGE column shows my Docker Hub images:

```bash
docker compose ps
```

RabbitMQ is healthy because Compose waits for its health check before it starts the Order Service.

## 2. Products load, and an order reaches the durable queue

This command shows the queue before the order. `order_queue` has `durable` set to `true`, so the queue survives a broker restart. The last column is the message count:

```bash
docker compose exec rabbitmq rabbitmqctl list_queues name durable messages
```

I open http://localhost:8080 in the browser. The products load from the Product Service.

I select Dog Food and quantity 2. The total is $39.98. Then I place the order.

I run the same queue command again:

```bash
docker compose exec rabbitmq rabbitmqctl list_queues name durable messages
```

The message count increased by one. This lab has no consumer, so accepted orders stay in RabbitMQ.

The browser makes the API requests, so the Store Front uses addresses that the browser can reach. Vue embeds these addresses when the image is built, and the API host in my Store Front image is `localhost`:

- `http://localhost:3000`
- `http://localhost:3030`

## 3. The Docker Hub repositories are public

| Service | Docker Hub repository |
|---|---|
| Order Service | https://hub.docker.com/r/zhizunbao2019/order-service |
| Product Service | https://hub.docker.com/r/zhizunbao2019/product-service |
| Store Front | https://hub.docker.com/r/zhizunbao2019/store-front |

---

## Service Forks

Each fork holds the Dockerfile for its service. My Product Service uses the Python implementation.

| Service | Fork |
|---|---|
| Order Service | https://github.com/peng2026-cloud/order-service-L4 |
| Product Service (Python) | https://github.com/peng2026-cloud/product-service-python-L4 |
| Store Front | https://github.com/peng2026-cloud/store-front-L4 |

## Files

| File | Purpose |
|---|---|
| `docker-compose.yaml` | The final image-only Compose file. |
| `.env.example` | Public deployment values and placeholder credentials. My actual `.env` is ignored. |
