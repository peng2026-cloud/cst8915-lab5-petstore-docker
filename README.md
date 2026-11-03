# CST8915 Lab 5: Containerizing the Algonquin Pet Store with Docker

| Student Name | Student ID | Course | Semester |
|---|---|---|---|
| Peng Wang | 041107730 | CST8915 Full-stack Cloud-native Development | Fall 2026 |

🎥 [Watch Demo Video](VIDEO_LINK)

---

## 1. Show the stack running from your Docker Hub images.

The final `docker-compose.yaml` in this repository has no `build` keys. It only names images, so Compose downloads them from Docker Hub and does not need the source code.

| Service | Image | Port on the host |
|---|---|---|
| RabbitMQ | `rabbitmq:4.3.6-management` | 15672 (management UI) |
| Order Service | `zhizunbao2019/order-service:latest` | 3000 |
| Product Service (Python) | `zhizunbao2019/product-service:latest` | 3030 |
| Store Front | `zhizunbao2019/store-front:latest` | 8080 |

This command lists the running containers, and the IMAGE column shows the Docker Hub images:

```bash
docker compose ps
```

## 2. Show products loading, place an order, and verify the increased message count in the durable queue.

This command shows the queue before the order. `order_queue` has `durable` set to `true`, so the queue survives a broker restart. The last column is the message count:

```bash
docker compose exec rabbitmq rabbitmqctl list_queues name durable messages
```

Open http://localhost:8080 in the browser. The products load from the Product Service.

Select Dog Food and quantity 2. The total is $39.98. Then place the order.

Run the same queue command again:

```bash
docker compose exec rabbitmq rabbitmqctl list_queues name durable messages
```

The message count increased by one. This lab has no consumer, so accepted orders stay in RabbitMQ.

## 3. Briefly show the running containers and Docker Hub repositories. Hide passwords and full broker connection strings.

The running containers are the four in the `docker compose ps` output from item 1. RabbitMQ is healthy because Compose waits for its health check before it starts the Order Service.

The Docker Hub repositories are public:

| Service | Docker Hub repository |
|---|---|
| Order Service | https://hub.docker.com/r/zhizunbao2019/order-service |
| Product Service | https://hub.docker.com/r/zhizunbao2019/product-service |
| Store Front | https://hub.docker.com/r/zhizunbao2019/store-front |

Passwords stay in `.env`, which is not in this repository. The Compose file only holds variable names, so it shows no password and no full broker connection string.

---

## Submission Details

**Links to your three chosen service forks:**

| Service | Fork |
|---|---|
| Order Service | https://github.com/peng2026-cloud/order-service-L4 |
| Product Service | https://github.com/peng2026-cloud/product-service-python-L4 |
| Store Front | https://github.com/peng2026-cloud/store-front-L4 |

**Identify whether your Product Service uses Python or Rust:** Python.

**Document the API host embedded in your Store Front image:** `localhost`. The browser makes the API requests, and Vue embeds these addresses when the image is built:

- `http://localhost:3000`
- `http://localhost:3030`
