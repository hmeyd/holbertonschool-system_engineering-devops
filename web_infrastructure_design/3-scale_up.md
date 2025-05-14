# Web Infrastructure: Application Server vs Web Server

This document explains the difference between an application server and a web server within a scalable and fault-tolerant infrastructure. It also outlines the components and their roles in a distributed server environment with load balancing and separate concerns.

## Infrastructure Overview

### Components:

* **1 Load Balancer (HAProxy) in Cluster Mode**
* **1 Web Server**
* **1 Application Server**
* **1 Database Server**

### Description:

* The **load balancer (HAProxy)** distributes incoming HTTP(S) requests to multiple backend servers to balance load and increase fault tolerance. It is configured in cluster mode to avoid a single point of failure (SPOF).
* The **web server (e.g., Nginx)** handles static content like HTML, CSS, JS, and images. It forwards dynamic requests to the application server.
* The **application server (e.g., Gunicorn, uWSGI, Node.js)** processes dynamic content, handles business logic, API requests, etc. It interacts with the database to retrieve or store data.
* The **database server (e.g., MySQL, PostgreSQL)** is used for persistent data storage.

## Why These Components are Split

### Load Balancer

* **Why:** Prevents any one server from becoming a bottleneck or SPOF.
* **Benefit:** Improves availability, scalability, and fault tolerance.

### Web Server

* **Why:** Optimized for serving static files and routing requests.
* **Benefit:** Reduces load on the application server and speeds up request processing.

### Application Server

* **Why:** Dedicated to handling application logic and processing dynamic requests.
* **Benefit:** Clear separation of responsibilities; allows each component to scale independently.

### Database Server

* **Why:** Dedicated data storage and query processing.
* **Benefit:** Allows for better data integrity, backups, and potential scaling via replication.

## Application Server vs Web Server

| Feature          | Web Server                                  | Application Server                                    |
| ---------------- | ------------------------------------------- | ----------------------------------------------------- |
| Purpose          | Serve static files and handle HTTP requests | Execute application logic and handle dynamic requests |
| Example Software | Nginx, Apache                               | Gunicorn, uWSGI, Node.js                              |
| Handles          | Images, HTML, CSS, JS                       | Python, PHP, JavaScript logic, database queries       |
| Protocol         | HTTP/HTTPS                                  | HTTP/HTTPS or FastCGI, WSGI                           |

## Conclusion

This architecture ensures modular design, scalability, and maintainability. Each server performs a specific role, which allows easier debugging, scaling, and security management. The use of a load balancer in cluster mode also increases the availability of the entire infrastructure.
