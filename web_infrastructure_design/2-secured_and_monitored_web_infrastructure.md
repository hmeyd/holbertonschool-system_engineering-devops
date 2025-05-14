# Secure Three-Server Web Infrastructure for [www.foobar.com](http://www.foobar.com)
![Simple Web Stack](images/2-secured_and_monitored_web_infrastructure.jpeg)

## Infrastructure Components

### Load Balancer (HAProxy)

* Distributes incoming traffic to web servers.
* Terminates SSL (HTTPS) connections.
* Configured with round-robin algorithm for even traffic distribution.

### Web Servers (2 Servers)

* Each contains:

  * Nginx web server (serves static files, handles HTTPS requests)
  * Application server (executes backend logic)
  * Application files (website codebase)
  * MySQL database (configured in a Primary-Replica setup)
  * Monitoring client (e.g., for Sumologic)

### Firewalls (3 Total)

* One for the load balancer
* One for each web server
* Restrict unauthorized access to ports/services (e.g., only allow HTTP/HTTPS traffic and internal DB communication)

### SSL Certificate

* Ensures encrypted traffic using HTTPS (secure communication)
* Installed on the load balancer (SSL termination point)

### Monitoring Clients

* Installed on each server
* Collects system metrics, logs, application performance data
* Sends data to external monitoring service (e.g., Sumologic)

---

## Purpose of Each Component

### Firewalls

* Protect servers from unauthorized access
* Control inbound and outbound traffic

### HTTPS Traffic (SSL Certificate)

* Ensures encrypted and secure communication
* Protects sensitive data from interception

### Monitoring

* Observes server health, traffic, uptime, errors
* Enables proactive alerts and diagnostics

### Monitoring Data Collection

* Monitoring agent installed on each server
* Collects logs, metrics, application QPS (queries per second), CPU/memory usage
* Sends data to external dashboard/service

### Monitoring Web Server QPS

* Enable Nginx access logs
* Configure log parser or use exporter/agent
* Monitor HTTP request rate with alerts if thresholds exceeded

---

## Issues With This Infrastructure

### SSL Termination at Load Balancer

* Traffic between load balancer and web servers is not encrypted
* Sensitive if internal network is compromised

### Single MySQL Write Node

* All writes go to Primary database
* Risk of data loss if Primary fails
* Failover requires manual or complex setup

### Identical Servers (Web, App, DB on same node)

* Poor separation of concerns
* Difficult to scale individual services
* If one service crashes, it may affect others

---

## Summary

This infrastructure enhances a simple LAMP stack by adding encryption (HTTPS), monitoring, and firewall security. However, it still contains challenges around SSL termination, MySQL write bottlenecks, and the need for service separation.
