# Client-server architecture

## Summary

Client-server architecture is a distributed system framework where tasks and workloads are divided between service providers (servers) and service requesters (clients). Clients initiate requests for resources or services, and servers process and respond to these requests.

## Prerequisites

TODO: link the notes a reader should know first.

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

### Definition

Client-server architecture is a distributed system framework where tasks and workloads are divided between service providers (servers) and service requesters (clients). Clients initiate requests for resources or services, and servers process and respond to these requests.

#### Key characteristics

##### Two-Tier model

The architecture consists of two main components:

- **Client**: A user interface or front-end device (e.g., browser, desktop application) that interacts with the user and sends requests to the server.
- **Server**: A back-end system that provides resources, processes data, and responds to client requests.

##### Centralized control

Servers centralize data storage and processing, making management and updates more efficient.

##### Resource sharing

Multiple clients can access and share resources provided by the server, such as databases, files, and services.

##### Scalability

Clients and servers can be scaled independently based on demand, though scaling servers often requires more effort compared to modern architectures like serverless.

##### Synchronous communication

Typically relies on synchronous request-response communication models (e.g., HTTP, RPC).

#### Use cases

Client-server architecture is widely used across various applications, including:

- **Web Applications**: Websites where browsers (clients) interact with web servers to retrieve and display content.
- **Email Services**: Email clients connect to servers (e.g., SMTP, IMAP) to send and receive messages.
- **Database Systems**: Applications accessing centralized databases for CRUD operations.
- **Enterprise Applications**: Systems like ERP or CRM that rely on a central server for data and logic.

#### Advantages

Client-server architecture offers a range of benefits, particularly for centralized systems with multiple clients accessing shared resources.

##### Centralized management

All data, resources, and logic are stored and managed on the server.

**Benefits**:

- Simplifies updates and maintenance since changes are made centrally on the server.
- Reduces the risk of data inconsistency by ensuring a single source of truth.

**Example**: In a database-driven application, only the server maintains and updates records.

###### Resource sharing

Multiple clients can access the same resources and services provided by the server.

**Benefits**:

- Efficient use of server resources.
- Promotes collaboration, such as in shared document editing or team management systems.

**Example**: A group of employees accessing a centralized CRM system.

###### Scalability

Client-server architecture allows for scaling both the server and client-side independently.

**Benefits**:

- Servers can be upgraded (vertical scaling) or duplicated (horizontal scaling) to handle increased load.
- New clients can be added without significantly impacting server performance, provided resources are sufficient.

**Example**: Adding more application servers behind a load balancer to manage a growing user base.

###### Enhanced security

Sensitive data is stored and managed on the server, reducing security risks on client devices.

**Benefits**:

- Centralized control allows enforcement of security policies and access permissions.
- Data encryption and authentication mechanisms can be implemented effectively.

**Example**: User credentials are verified on a secure server rather than on local client devices.

###### Ease of maintenance

Maintenance tasks like backups, updates, and monitoring can be performed centrally on the server.

**Benefits**:

- Simplifies troubleshooting and reduces downtime.
- Clients do not need to be individually updated or maintained.

**Example**: Patching a vulnerability in a web application’s server ensures all connected clients are secure.

###### Flexibility

Clients can run on various devices and platforms while relying on the server for core functionality.

**Benefits**:

- Supports diverse client types (e.g., web browsers, mobile apps, desktop software).
- Encourages platform independence.

**Example**: A banking application accessible via web, mobile, and ATM clients, all connected to the same backend server.

###### Load distribution

Tasks are distributed between the client (user interface, input handling) and server (data storage, processing).

**Benefits**:

- Optimizes resource utilization by offloading computation-heavy tasks to the server.
- Reduces workload on the client, enabling lightweight devices to participate.

**Example**: A video streaming service where the server handles content delivery, and the client focuses on playback.

###### Standardized communication

Uses well-defined protocols for communication between client and server.

**Benefits**:

- Promotes interoperability between different client and server platforms.
- Simplifies integration with third-party tools and services.

**Example**: A RESTful API using HTTP allows various client applications to interact with the server.

###### Real-Time data access

Clients can retrieve and update data in real-time through server connections.

**Benefits**:

- Enables dynamic applications like live chats, stock trading platforms, or multiplayer games.

**Example**: A stock trading app displays real-time stock prices fetched from the server.

###### Reliable backup and recovery

Centralized data storage on the server allows for systematic backup and disaster recovery strategies.

**Benefits**:

- Minimizes data loss and ensures quick recovery during failures.

**Example**: A cloud storage service maintains daily backups of user files on its servers.

### Core components

Client-server architecture relies on distinct components, each playing a critical role in the system's functionality.

#### Client

**Role**: The client is the interface through which users interact with the system. It sends requests to the server for data or services.

**Characteristics**:

- Runs on user devices like desktops, mobile phones, or browsers.
- Provides a graphical user interface (GUI) or command-line interface (CLI) to interact with users.
- Initiates requests and processes responses from the server.

**Examples**:

- Web browsers (e.g., Chrome, Firefox) acting as clients for web servers.
- Email clients (e.g., Outlook, Thunderbird) interacting with mail servers.

##### Server

**Role**: The server is responsible for processing client requests and providing the requested data or services.

**Characteristics**:

- Centralized system that stores data, runs applications, and performs backend operations.
- Handles multiple simultaneous requests from clients.
- Ensures data integrity, security, and resource availability.

**Examples**:

- Web servers (e.g., Apache, NGINX).
- Database servers (e.g., MySQL, PostgreSQL).
- Application servers (e.g., Tomcat, Node.js).

##### Communication protocols

**Role**: Protocols govern the exchange of data between the client and server, ensuring proper communication.

**Common Protocols**:

- **HTTP/HTTPS**: Used for web applications.
- **FTP**: Used for file transfers.
- **SMTP, IMAP, POP3**: Used for email communication.
- **WebSockets**: Enables real-time, bidirectional communication.

**Examples**:

- A web browser using HTTP to fetch content from a server.
- An email client using SMTP to send emails and IMAP to receive them.

##### Network

**Role**: Provides the physical or virtual infrastructure that connects clients and servers.

**Key Components**:

- **LAN (Local Area Network)**: Used in smaller, localized client-server setups (e.g., office networks).
- **WAN (Wide Area Network)**: Used for global communication (e.g., the internet).

**Importance**:

- Ensures reliable and secure data transfer between clients and servers.

###### Middleware

**Role**: Acts as an intermediary layer facilitating communication and resource management between clients and servers.

**Functions**:

- Manages API calls and message queues.
- Provides data transformation and authentication.

**Examples**:

- API Gateways, Load Balancers.

###### Data storage

**Role**: Servers typically connect to a database or file system to store and retrieve data.

**Examples**:

- Relational Databases (e.g., MySQL, Oracle DB).
- NoSQL Databases (e.g., MongoDB, DynamoDB).
- File Systems (e.g., distributed file systems like HDFS).

###### Authentication and authorization systems

**Role**: Ensures only authenticated and authorized clients can access server resources.

**Components**:

- Authentication mechanisms (e.g., OAuth, JWT).
- Access control policies for resource permissions.

**Importance**:

- Enhances security and ensures proper resource utilization.

###### Error handling

**Role**: Manages failures in client-server communication.

**Examples**:

- HTTP Status Codes: 404 (Not Found), 500 (Server Error).
- Retries or fallbacks in case of temporary server unavailability.

### Workflow

Client-server architecture operates on a request-response model, where the client requests resources or services, and the server processes and responds to those requests.

#### Flow

1. **Client Request**:
    - A client initiates a request for data or services by sending a message to the server.
    - Example: A web browser requests a webpage by sending an HTTP GET request to the server.
2. **Server Processing**:
    - The server receives the request, processes it, and performs necessary operations such as:
        - Querying a database.
        - Executing backend logic.
        - Preparing the requested resource.
    - Example: The server queries a database for user details based on the request parameters.
3. **Response to Client**:
    - After processing, the server sends a response back to the client.
    - This response typically includes:
        - The requested data (e.g., HTML content, JSON response).
        - A status code indicating the success or failure of the request.
    - Example: The server returns an HTML page with a 200 OK status code or an error message with a 404 Not Found code.
4. **Client Rendering**:
    - The client processes the server’s response and displays or utilizes the data.
    - Example: A browser renders a webpage using the HTML content provided by the server.

#### Communication rotocols

The interaction between the client and server is governed by protocols that define how data is exchanged:

- **HTTP/HTTPS**: Used for web applications.
- **TCP/IP**: Ensures reliable data transfer.
- **WebSocket**: Enables real-time, bidirectional communication.
- **SMTP/IMAP**: Used for email systems.

##### Synchronous and asynchronous

**Synchronous**:

- The client waits for the server’s response before proceeding.
- Example: A browser waiting for a webpage to load.

**Asynchronous**:

- The client can continue other tasks while waiting for the server’s response.
- Example: AJAX calls in web applications allow partial page updates without reloading.

#### Scalability and load distribution

Multiple clients can interact with a single server, but when the load increases:

- **Vertical Scaling**: Adding more resources (e.g., CPU, RAM) to the server.
- **Horizontal Scaling**: Distributing requests across multiple servers using load balancers.

#### Fault tolerance

If a server becomes unavailable, client-server systems often rely on:

- Redundant servers.
- Caching mechanisms to serve previously requested data.
- Error responses to inform clients of the issue.

### Challenges

While client-server architecture has many advantages, it also comes with its own set of challenges that need to be addressed for efficient implementation and operation.

#### Single point of failure

**Problem**: If the central server fails, the entire system becomes inaccessible to all clients.

**Impact**:

- Loss of availability for critical applications.

**Mitigation**:

- Implement server redundancy and failover mechanisms.
- Use load balancers and distributed systems to reduce reliance on a single server.

##### Scalability limitations

**Problem**: As the number of clients increases, the server may become a bottleneck due to resource constraints.

**Impact**:

- Performance degradation and slower response times during peak usage.

**Mitigation**:

- Use horizontal scaling (e.g., adding more servers) and load balancers.
- Optimize server-side code and implement caching mechanisms.

###### Network dependency

**Problem**: The architecture relies heavily on stable and fast network connections between clients and servers.

**Impact**:

- Network latency or disruptions can cause delays or complete service outages.

**Mitigation**:

- Deploy servers closer to users (e.g., via CDN or regional servers).
- Optimize data transfer with compression and minimize unnecessary client-server communication.

###### High server costs

**Problem**: Maintaining and scaling central servers can be expensive, especially for large-scale applications.

**Impact**:

- Increased operational costs for hardware, software, and personnel.

**Mitigation**:

- Leverage cloud computing services to reduce infrastructure costs.
- Use server virtualization to maximize resource utilization.

###### Security vulnerabilities

**Problem**: Centralized data storage makes the server a prime target for cyberattacks such as DDoS, data breaches, and unauthorized access.

**Impact**:

- Compromises sensitive data and disrupts service availability.

**Mitigation**:

- Implement strong authentication (e.g., MFA), encryption, and access controls.
- Regularly patch vulnerabilities and conduct security audits.

###### Performance bottlenecks

**Problem**: When too many clients send simultaneous requests, the server may become overloaded.

**Impact**:

- Slower response times or server crashes.

**Mitigation**:

- Use caching systems (e.g., Redis, Memcached) to reduce server load.
- Implement asynchronous processing and rate limiting for client requests.

###### Maintenance complexity

**Problem**: Centralized updates to the server can disrupt service for all connected clients.

**Impact**:

- Downtime during maintenance can affect user experience.

**Mitigation**:

- Schedule maintenance during low-traffic periods.
- Use rolling updates to minimize downtime.

###### Limited offline functionality

**Problem**: Clients often depend on real-time communication with the server, making offline usage difficult.

**Impact**:

- Users cannot access the application without an active internet connection.

**Mitigation**:

- Implement offline-first strategies, such as local caching or Progressive Web Apps (PWAs).
- Synchronize data with the server when connectivity is restored.

###### Complexity of load distribution

**Problem**: Distributing workloads effectively across multiple servers requires careful planning and management.

**Impact**:

- Uneven server utilization can lead to inefficiencies or overloading.

**Mitigation**:

- Use load balancers to distribute traffic evenly.
- Monitor server performance and dynamically allocate resources.

###### Difficulty in debugging

**Problem**: Debugging issues in a distributed system can be challenging due to the separation of client and server components.

**Impact**:

- Identifying the source of errors (client-side, server-side, or network) becomes time-consuming.

**Mitigation**:

- Use comprehensive logging and monitoring tools (e.g., ELK stack, Splunk).
- Implement end-to-end tracing to track requests across the system.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Richards, M., Ford, N. (2020). *Fundamentals of Software Architecture*. O'Reilly Media. Covers the role and expectations of an architect, architecture characteristics and the main architectural styles.

TODO: check the content of this note against the sources above and record what was verified and when.
