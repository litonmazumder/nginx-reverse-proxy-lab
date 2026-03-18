# ginx Reverse Proxy Lab

This project demonstrates a simple reverse proxy and load balancing setup using Nginx and Docker.

The reverse proxy routes incoming client requests to multiple backend services running in containers. This setup represents a common architecture used in modern DevOps environments.

Architecture

Client requests are received by the Nginx reverse proxy, which forwards traffic to backend services using load balancing.
```
Client
   ↓
Nginx Reverse Proxy
   ↓
App1      App2
```
## Technologies Used

- Nginx

- Docker

- Docker Compose

- Linux

## Nginx Configuration

The Nginx reverse proxy forwards requests to backend containers using an upstream load balancing configuration.

## Example configuration:
```
events {}

http {

    upstream backend {
        server app1:80;
        server app2:80;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://backend;
        }
    }

}
```
This configuration distributes incoming traffic between multiple backend services.

## Docker Compose Setup

Backend services and the reverse proxy are deployed using Docker Compose.

## Example:
```
version: "3"

services:

  nginx:
    image: nginx:latest
    container_name: reverse-proxy
    ports:
      - "80:80"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - app1
      - app2

  app1:
    image: nginx

  app2:
    image: nginx
```
This creates a reverse proxy container and two backend service containers.

## Example Output

### Example Docker containers running in the environment.

![Running Containers](screenshots/running-containers.png)

## Reverse Proxy Routing

### Example browser request routed through the Nginx reverse proxy.

![reverse-proxy-routing](screenshots/reverse-proxy-routing.png)

## Repository Structure
```
nginx-reverse-proxy-lab
│
├── docker-compose.yml
│
├── nginx
│   └── nginx.conf
│
├── architecture
│   └── reverse-proxy-architecture.png
│
├── screenshots
│   ├── docker-containers.png
│   └── nginx-routing.png
│
└── README.md
```
## Purpose

This project demonstrates how to implement a reverse proxy and load balancing architecture using containerized services.

### It highlights key DevOps concepts such as:

- reverse proxy configuration

- containerized infrastructure

- service routing

- load balancing with Nginx

## License

This project is licensed under the MIT License.