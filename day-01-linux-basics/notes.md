# Notes - Day 1 Linux Basics for DevOps

## Topics Covered

- How the internet works
- What is a server?
- Difference between web server and application server
- Types of applications
- Standalone applications
- Web applications
- Application support
- Application maintenance
- Linux introduction
- Kernel, shell, and bootloader
- Linux system architecture
- Linux file system
- Linux vs Unix
- Process states in Linux

## 1. How the Internet Works

The internet is a global network of connected computers that communicate using standard protocols. When a user opens a website, the browser sends a request, the request travels through networks, reaches the server, and the server sends a response back to the user.

Important parts of the internet include:

- DNS
- ISP
- IP address
- Packets
- TCP
- Routing
- HTTP/HTTPS

## 2. DNS

DNS stands for Domain Name System. It converts domain names like `google.com` into IP addresses.

DNS works like a phonebook of the internet. Humans remember names easily, but computers communicate using IP addresses.

## 3. ISP

ISP stands for Internet Service Provider. It connects your device to the internet.

Examples:

- PTCL
- Nayatel
- StormFiber
- Local internet providers

## 4. IP Address

An IP address is a unique address used to identify a device on a network.

Every packet of data contains source and destination IP addresses so it can travel correctly across networks.

## 5. Packets

Data on the internet is broken into small pieces called packets.

Each packet travels independently through the network and is reassembled at the destination.

## 6. TCP

TCP stands for Transmission Control Protocol.

It ensures reliable delivery of data. If packets are lost, TCP handles retransmission and makes sure data reaches correctly.

## 7. Routing

Routing decides the best path for data packets to travel across the internet.

Routers move packets between networks until they reach the destination server.

## 8. HTTP and HTTPS

HTTP and HTTPS are protocols used by browsers to communicate with web servers.

HTTPS is more secure because it uses encryption through SSL/TLS.

## 9. What is a Server?

A server is a powerful computer or software system that provides services, data, or resources to other computers over a network.

In simple words, a server waits for requests and sends responses.

Example:

- Browser = client
- Website machine = server

## 10. Types of Servers

Common types of servers include:

- Web server
- Application server
- Database server
- File server
- Cloud server

## 11. Web Server

A web server receives HTTP/HTTPS requests and serves static files like HTML, CSS, JavaScript, and images.

Examples:

- Nginx
- Apache

## 12. Application Server

An application server executes application code and business logic.

Examples:

- Node.js
- Spring Boot
- Tomcat
- .NET

## 13. Database Server

A database server stores and manages structured data.

Examples:

- MySQL
- PostgreSQL
- MongoDB

## 14. File Server

A file server stores and shares files across a network.

It is used for documents, backups, images, videos, and logs.

## 15. Cloud Server

A cloud server is a virtual server hosted by a cloud provider.

Examples:

- AWS EC2
- Azure VM
- Google Cloud VM

## 16. Server vs Cloud vs Container

A server is a machine that runs applications and provides services.

A cloud is a collection of servers managed by cloud providers.

A container is a lightweight package that includes application code, libraries, dependencies, and runtime.

## 17. Web Application

A web application runs on a server and is accessed through a browser over the internet.

Examples:

- Gmail
- Facebook
- Amazon
- Online banking

## 18. Standalone Application

A standalone application runs on a single machine and does not always need an internet connection.

Examples:

- MS Word
- Notepad
- VLC Player
- Photoshop

## 19. Application Support

Application support means keeping an application running smoothly in production.

It includes:

- Fixing bugs
- Handling user issues
- Monitoring logs and alerts
- Restarting services if needed
- Handling downtime or outages
- Providing technical assistance

## 20. Application Maintenance

Application maintenance means updating and improving the application over time.

It includes:

- Corrective maintenance
- Adaptive maintenance
- Perfective maintenance
- Preventive maintenance

## Day 1 Summary

Day 1 helped me understand the basic foundation of the internet, servers, applications, and Linux-related concepts. These concepts are important for DevOps because DevOps engineers work with servers, cloud platforms, containers, automation, deployments, and monitoring.
