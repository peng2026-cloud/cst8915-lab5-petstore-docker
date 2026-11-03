# CST8915 Lab 5: Containerizing the Algonquin Pet Store with Docker

| Student Name | Student ID | Course | Semester |
|---|---|---|---|
| Peng Wang | 041107730 | CST8915 Full-stack Cloud-native Development | Fall 2026 |

🎥 [Watch Demo Video](https://www.youtube.com/watch?v=bbWL9oNa3Bw)

---

## 1. Show the stack running from your Docker Hub images.

The final `docker-compose.yaml` in this repository names the Docker Hub images, so Compose downloads them from Docker Hub.

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

This command shows the durable queue and its message count before the order:

```bash
docker compose exec rabbitmq rabbitmqctl list_queues name durable messages
```

Open http://localhost:8080 in the browser. The products load.

Select Cat Food and quantity 2. The total is $69.98. Then place the order.

Run the same queue command again:

```bash
docker compose exec rabbitmq rabbitmqctl list_queues name durable messages
```

The message count increased by one.

## 3. Briefly show the running containers and Docker Hub repositories. Hide passwords and full broker connection strings.

The Docker Hub repositories are public:

| Service | Docker Hub repository |
|---|---|
| Order Service | https://hub.docker.com/r/zhizunbao2019/order-service |
| Product Service | https://hub.docker.com/r/zhizunbao2019/product-service |
| Store Front | https://hub.docker.com/r/zhizunbao2019/store-front |

---

## Submission Details

| Item | Value |
|---|---|
| Order Service fork | https://github.com/peng2026-cloud/order-service-L4 |
| Product Service fork | https://github.com/peng2026-cloud/product-service-python-L4 |
| Store Front fork | https://github.com/peng2026-cloud/store-front-L4 |
| Product Service language | Python |
| API host in the Store Front image | `localhost` |
