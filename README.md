# CST8915 Lab 5: Containerizing the Algonquin Pet Store with Docker

| Student Name | Student ID | Course | Semester |
|---|---|---|---|
| Peng Wang | 041107730 | CST8915 Full-stack Cloud-native Development | Fall 2026 |

---

## Demo Video

🎥 [Watch Demo Video](VIDEO_LINK)

---

## Service Forks

| Service | Fork |
|---|---|
| Order Service | https://github.com/peng2026-cloud/order-service-L4 |
| Product Service (Python) | https://github.com/peng2026-cloud/product-service-python-L4 |
| Store Front | https://github.com/peng2026-cloud/store-front-L4 |

---

## Docker Hub Images

| Service | Image |
|---|---|
| Order Service | https://hub.docker.com/r/zhizunbao2019/order-service |
| Product Service | https://hub.docker.com/r/zhizunbao2019/product-service |
| Store Front | https://hub.docker.com/r/zhizunbao2019/store-front |

---

## Deployment Details

| Item | Value |
|---|---|
| Product Service implementation | Python |
| API host embedded in the Store Front image | `localhost` (`http://localhost:3000` and `http://localhost:3030`) |
| Docker host | Local machine, Docker Desktop on Windows |

---

## Files

| File | Purpose |
|---|---|
| `docker-compose.yaml` | The final image-only Compose file, which runs the stack from the Docker Hub images. |
| `.env.example` | Public deployment values and placeholder credentials. Copy it to `.env` and set your own password. |
