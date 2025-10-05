---
title: "API - Application Programming Interface"
datePublished: Sun Oct 05 2025 06:32:43 GMT+0000 (Coordinated Universal Time)
cuid: cmgdbrvf1000002jpcm15044r
slug: api-application-programming-interface
tags: codewithnini

---

# **1\. What is an API?**

**API (Application Programming Interface)** is a **set of rules & protocol that allows two applications or systems to communicate**.

* Acts as a **bridge** between different software components.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1759658423393/e69e84d4-d453-472b-ad20-df54d4410acc.png align="center")

* Can be **local (within app)** or **web-based (over HTTP/HTTPS)**.
    

**Example:**

* When you check weather on your app, it calls a **weather API** to fetch data from a server.
    

---

### **Networking Protocols**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1759661793100/fad45bf6-b25b-4916-ae99-9bad1fb7e7fc.png align="center")

A **network protocol** is basically a set of **rules and standards** that computers and devices follow to **communicate over a network**.

In simpler terms:

* It tells devices **how to send, receive, and interpret data**.
    
* Think of it as a **common language** for computers to talk to each other.
    
* Without protocols, devices wouldn’t understand each other and communication would fail.
    

1. **HTTP (HyperText Transfer Protocol)**
    
    * How the web works.
        
    * Lets your browser fetch web pages (HTML, images, etc.) from servers.
        
    * Works on a client-server model.
        
2. **HTTP/3**
    
    * New version of HTTP.
        
    * Uses **QUIC** protocol over **UDP** instead of TCP → faster for mobile & heavy web apps.
        
    * Great for apps needing speed & high bandwidth (VR, interactive websites).
        
3. **HTTPS (HyperText Transfer Protocol Secure)**
    
    * Secure version of HTTP.
        
    * Encrypts data so no one can eavesdrop.
        
    * Used for banking, login pages, and private communication.
        
4. **WebSocket**
    
    * Enables **real-time communication**.
        
    * Works over TCP.
        
    * Instead of always asking for updates (pull), server can **push data** instantly.
        
    * Used in: online games, stock trading, chat apps.
        
5. **TCP (Transmission Control Protocol)**
    
    * Sends data reliably.
        
    * Ensures packets arrive in order and without loss.
        
    * Many web protocols (HTTP, FTP, SMTP) run on TCP.
        
6. **UDP (User Datagram Protocol)**
    
    * Sends data **without waiting for confirmation**.
        
    * Faster but may lose some packets.
        
    * Ideal for: video calls, streaming, online gaming.
        
7. **SMTP (Simple Mail Transfer Protocol)**
    
    * Standard way to send emails.
        
    * Transfers email from one server/user to another.
        
8. **FTP (File Transfer Protocol)**
    
    * Moves files between computers (client ↔ server).
        
    * Uses separate channels:
        
        * **Control channel** → commands
            
        * **Data channel** → file transfer
            

## **API PROTOCOLS**

### **1️⃣ REST (Representational State Transfer)**

* **Type:** Architectural style
    
* **Uses:** HTTP methods (`GET`, `POST`, `PUT`, `DELETE`)
    
* **Format:** JSON / XML
    
* **Best for:** Web & mobile APIs
    
* **Example:**
    
    ```java
    GET https://api.example.com/users
    ```
    
    ![](https://blog.postman.com/wp-content/uploads/2023/11/02_API_protocols-1024x390.jpg align="left")
    

---

### **2️⃣ Webhooks**

* **Type:** Event-driven callback mechanism
    
* **How it works:** Server **notifies client** via HTTP POST when an event occurs
    
* **Example:** Payment success → triggers webhook to client app
    
* **Use Case:** Real-time updates (payments, GitHub push, Slack message)
    

![](https://blog.postman.com/wp-content/uploads/2023/11/03_API_protocols-1024x977.jpg align="left")

---

### **3️⃣ GraphQL**

* **Type:** Query language for APIs
    
* **How it works:** Client requests **exact fields needed**
    
* **Advantage:** Reduces over-fetching and under-fetching
    
* **Example:**
    
    ```java
    { user { id name email } }
    ```
    

![](https://blog.postman.com/wp-content/uploads/2023/11/04_API_protocols-1024x695.jpg align="left")

---

### **4️⃣ SOAP (Simple Object Access Protocol)**

* **Type:** XML-based messaging protocol
    
* **Transport:** HTTP / SMTP
    
* **Structure:** Envelope + Header + Body
    
* **Use Case:** Enterprise-level, strict contracts
    
* **Example:** Banking, payment, legacy systems
    

![](https://blog.postman.com/wp-content/uploads/2023/11/05_API_protocols-1024x779.jpg align="left")

---

### **5️⃣ WebSocket**

* **Type:** Full-duplex communication channel
    
* **How it works:** Keeps a single connection open for both send & receive
    
* **Use Case:** Real-time apps (chat, games, stock updates)
    

![](https://blog.postman.com/wp-content/uploads/2023/11/06_API_protocols-1024x279.jpg align="left")

---

### **6️⃣ gRPC (Google Remote Procedure Call)**

* **Type:** High-performance binary protocol
    
* **Format:** Protocol Buffers (`.proto` files)
    
* **Languages:** Cross-language (Java, Python, Go, etc.)
    
* **Use Case:** Microservices communication
    

![](https://blog.postman.com/wp-content/uploads/2023/11/07_API_protocols-1024x775.jpg align="left")

---

### **7️⃣ MQTT (Message Queuing Telemetry Transport)**

* **Type:** Lightweight publish/subscribe protocol
    
* **Transport:** TCP/IP
    
* **Use Case:** IoT devices, low-bandwidth environments
    
* **Example:** Sensors → Broker → Subscribers
    

---

### **8️⃣ AMQP (Advanced Message Queuing Protocol)**

* **Type:** Open standard for messaging
    
* **Components:** Producer → Exchange → Queue → Consumer
    
* **Use Case:** Enterprise message brokers (RabbitMQ)
    

---

### **9️⃣ SSE (Server-Sent Events)**

* **Type:** One-way push from server to client via HTTP
    
* **Use Case:** Live feeds, notifications, dashboards
    
* **Difference from WebSocket:** One-direction (server → client only)
    

---

### **🔟 EDA (Event-Driven Architecture)**

* **Type:** Software design pattern
    
* **Flow:** Producer → Event Channel → Consumer
    
* **Use Case:** Scalable, async microservices (Kafka, RabbitMQ)
    

---

### **1️⃣1️⃣ EDI (Electronic Data Interchange)**

* **Type:** Standardized B2B data exchange format
    
* **Use Case:** Supply chain, invoicing, healthcare data
    
* **Format:** Plain text with specific structure (not JSON/XML)
    

---

## 🧩 **Summary Table**

| Protocol | Type | Format | Direction | Common Use |
| --- | --- | --- | --- | --- |
| **REST** | Architectural | JSON/XML | Request/Response | Web & Mobile APIs |
| **Webhooks** | Event callback | JSON | Server → Client | Notifications |
| **GraphQL** | Query language | JSON | Client ↔ Server | Custom data queries |
| **SOAP** | Protocol | XML | Request/Response | Enterprise systems |
| **WebSocket** | Communication | Binary/Text | Duplex | Real-time chat |
| **gRPC** | RPC Protocol | ProtoBuf | Duplex | Microservices |
| **MQTT** | Messaging | Binary | Pub/Sub | IoT |
| **AMQP** | Messaging | Binary | Pub/Sub | Enterprise queues |
| **SSE** | Stream | Text | Server → Client | Live data |
| **EDA** | Architecture | Event | Async | Microservices |
| **EDI** | Data format | Plain text | B2B | Business data exchange |

# 🧩 Understanding Different Types of APIs

You might have heard about different types of APIs like **GraphQL**, **SOAP**, **REST**, **gRPC**, and others.  
But what do these really mean?

---

### 🏛️ APIs as Architectural Styles

Think of APIs like **architectural styles for houses**:

* When you build a house, you choose a **design style** — maybe **Ionic columns** or **Doric columns**.
    
* Both support your house, but they look and function slightly differently.
    
* Similarly, different API styles define **different rule sets and structures** for how systems communicate.
    

Each API type has its own “style” of building and interacting with software systems.

---

### 💡 The Purpose of API Styles

Each API architectural style defines:

* How data is **requested** and **sent**.
    
* How the **client** (like a browser or app) and **server** (backend) communicate.
    
* The **rules and format** for exchanging data.
    

---

### 🧠 Do You Need to Learn All API Types?

Not really.  
You don’t have to learn every type of API under the sun.  
Instead, use the principle of **“Just-In-Time Learning”** — learn what you need **when** you need it.

That approach gives you:

* Stronger motivation.
    
* Better understanding (since you apply it immediately).
    
* Less wasted time on unused concepts.
    

---

### 🌍 The King of Web APIs: REST

When it comes to **web development**, one API style dominates — **REST (Representational State Transfer)**.

✅ REST is:

* The **most popular**,
    
* **Most widely used**, and
    
* **Most important** API style to know for web-based projects.
    

---

### ⚙️ What Makes an API RESTful?

A **RESTful API** is not one that puts you to sleep 😄 —  
It’s an API that **follows a specific set of architectural rules**.

The most important rule:

> **RESTful APIs use the HTTP Protocol** to communicate between client and server.

So whenever you send a request or receive a response over the web using **HTTP methods** (`GET`, `POST`, `PUT`, `DELETE`), you’re interacting with a RESTful API.

---

### 🗺️ Summary

| Concept | Description |
| --- | --- |
| **API** | Set of rules for communication between two systems |
| **Architectural Style** | The design pattern or rule set defining how the API works |
| **Popular Styles** | REST, SOAP, GraphQL, gRPC, WebSockets, etc. |
| **Most Used** | REST (uses HTTP methods for client-server communication) |
| **Learning Tip** | Learn as needed — focus on REST first |

# **As we know many types of APIs**

1. **Web APIs (REST, SOAP)** – over the internet
    
2. **Library/Framework APIs** – like `java.util`, `Selenium WebDriver API`
    
3. **Operating System APIs** – for file access, memory management
    

**Focus for Automation:** Web APIs (REST and SOAP)

---

# **REST API vs SOAP API**

| Feature | REST | SOAP |
| --- | --- | --- |
| Protocol | HTTP | XML over HTTP/SOAP |
| Format | JSON / XML | XML only |
| Speed | Faster | Slower |
| State | Stateless | Stateful or Stateless |
| Use Case | Modern web services | Legacy systems |

**REST API** is more common in automation and modern apps.

---

# **HTTP Methods in REST API**

| Method | Description |
| --- | --- |
| GET | Retrieve data from server |
| POST | Send data to server (create resource) |
| PUT | Update existing data |
| PATCH | Update part of resource |
| DELETE | Remove resource |

---

# **REST API Request & Response**

* **Request** → sent by client
    
    * URL, HTTP method, headers, body (for POST/PUT)
        
* **Response** → received from server
    
    * Status code, headers, body
        

**Example: GET request**

```java
GET https://api.example.com/products/1
Response:
{
    "id": 1,
    "name": "Laptop",
    "price": 50000
}
```

**Status Codes:**

* 200 → Success
    
* 201 → Created
    
* 400 → Bad Request
    
* 401 → Unauthorized
    
* 404 → Not Found
    
* 500 → Server Error
    

---

# **Tools to Test API**

1. **Postman** – GUI tool to send API requests
    
2. **Swagger** – API documentation & testing
    
3. **cURL** – command line tool
    
4. **RestAssured (Java)** – automation of API testing
    

---

# Things Need to know

### What is FrontEnd?

Frontend is something that is visible to the user.

**ex**: In a web application, you can see the web elements like inputArea, radioButton, All elements are visible to the user.

### What is BackEnding?

The backend is the code that is written by developers ,it could be data or database every thing is backend of an application and it is not visiable to user.

Ex:

### When coming to the testing

* In frontend manual testing is performed, with the help of frontend.
    
* In Backend API testing fall in to Action .
    
    **NOTE**: API is complete about backend.
    

### What is WebApplication?

Any application which is accessable through browser is called as web application.

In client-server applications if we go for web application a browser act as a client.

**server**: process the request and give back the response to client.

### What is Browser?

* A browser is a stand-alone application that is used to access any webapplication over the network via **URI**.
    
* The browser understand only HTML, CSS, JAVASCRIPT and hence it always create **HTTP-request** and interpret **HTTP-response** the given by the webserver.
    
* The browser is the only way to access the web application.
    
* The browser always sends and receive the request via **HTTP** (Hyper Text Transfer Protocol).
    
    **EX**: Chrome, Brave , Firefox, Opera, Edge, etc.
    

### What is WebServer?

Web- server as name implies it “server the Request to to browser” , it help both web-server and web-application to intract with each other.

## 🔹 **Web Server**

A **Web Server** is software (and sometimes hardware) that:

1. **Stores, processes, and delivers web content** (HTML, CSS, JavaScript, images, etc.) to clients (browsers).
    
2. Handles **HTTP/HTTPS requests and responses**.
    
3. Serves **static content** and can forward **dynamic requests** to an Application Server.
    

---

### 🔹 Functions of a Web Server

* Accepts HTTP requests from browsers (clients).
    
* Serves static files (HTML, CSS, JS, images, videos).
    
* Can use plugins/CGI scripts to generate dynamic content.
    
* Routes API or servlet requests to **Application Server** if needed.
    

---

### 🔹 Examples

* **Apache HTTP Server**
    
* **Nginx**
    
* **IIS (Internet Information Services)**
    
* **LiteSpeed**
    
* **Tomcat (acts as both Web + App server)**
    

---

### 🔹 Web Server vs App Server (Quick Difference)

| Feature | **Web Server** | **Application Server** |
| --- | --- | --- |
| **Purpose** | Serves static content, handles HTTP requests | Runs business logic, processes dynamic content |
| **Content** | HTML, CSS, JS, images | Servlets, EJBs, APIs |
| **Examples** | Apache, Nginx, IIS | WebLogic, JBoss, Tomcat |

---

✅ **In short:**  
A **Web Server** is software that **accepts client (browser) requests and serves static content** or forwards dynamic requests to an **Application Server** for processing.

### What is AppServer or WebApplication?

## 🔹 **App Server (Application Server)**

* An **Application Server** is a software framework that provides an environment to run **business logic (server-side code)**.
    
* It handles **complex operations** like transactions, messaging, security, and database connectivity.
    
* Examples: **JBoss, WebSphere, WebLogic, GlassFish, Tomcat (partially)**.
    

👉 Think of it as:  
“**Where your core business logic lives and runs.**”

---

## 🔹 **Web Application**

* A **Web Application** is a **software program** that runs on a web server and can be accessed through a browser via the internet or intranet.
    
* It usually contains **frontend (UI)** + **backend logic** + **database**.
    
* Examples: **Facebook, Gmail, Online Banking, Amazon**.
    

👉 Think of it as:  
“**An actual application users interact with via a browser.**”

---

## 🔹 Key Difference

| Feature | **App Server** | **Web Application** |
| --- | --- | --- |
| **Definition** | Platform to run business logic | Actual software used by end-users |
| **Purpose** | Provides environment for backend code | Provides functionality to users |
| **Examples** | JBoss, WebLogic, Tomcat | Gmail, Amazon, Netflix |
| **User Access** | Developers/Programs interact | End-users interact via browser |

---

✅ **In short:**

* **App Server** = The engine/environment that runs your backend code.
    
* **Web Application** = The actual app (with UI + backend) users access via a browser.
    

### Types of Web Resources?

## 🔹 **Types of Web Resources**

In web technology, a **web resource** is anything that can be identified and accessed on the web through a **URL**.

### Common Types:

1. **Static Resources** → Fixed content that does not change.
    
    * Examples: HTML files, CSS, JavaScript, images, videos, PDFs.
        
2. **Dynamic Resources** → Content generated at runtime by server-side code.
    
    * Examples: JSP, Servlets, PHP scripts, [ASP.NET](http://ASP.NET) pages, REST API responses.
        
3. **Services (APIs / Endpoints)** → Web services or APIs that expose data and operations.
    
    * Examples: [`https://api.github.com/users`](https://api.github.com/users), SOAP services.
        
4. **Other Media Resources** → Audio, video, documents, fonts delivered via the web.
    

👉 In short:  
**Web resources = Any file, document, or service that can be accessed over the web using a URL.**

### What is URL explain with syntax ?

## 🔹 **What is URL?**

**URL (Uniform Resource Locator)** is the address used to identify and access a resource on the internet.  
It tells the browser **where the resource is located** and **how to fetch it**.

---

### 🔹 **Syntax of a URL**

```java
protocol://hostname:port/path?query#fragment
```

### 🔹 Explanation of Parts

1. **protocol** → Communication method (e.g., `http`, `https`, `ftp`).
    
    * Example: `https`
        
2. **hostname (domain name / IP)** → The server hosting the resource.
    
    * Example: [`www.google.com`](http://www.google.com)
        
3. **port** → The communication endpoint (optional, defaults: 80 for HTTP, 443 for HTTPS).
    
    * Example: `:8080`
        
4. **path** → Location of the resource on the server.
    
    * Example: `/products/list`
        
5. **query string** → Extra parameters in key=value pairs (after `?`).
    
    * Example: `?id=10&sort=asc`
        
6. **fragment** → A section inside the page (after `#`).
    
    * Example: `#section2`
        

---

### 🔹 Example URL

```java
https://www.amazon.in:443/laptops?brand=hp&sort=price#reviews
```

* **protocol** → `https`
    
* **hostname** → [`www.amazon.in`](http://www.amazon.in)
    
* **port** → `443`
    
* **path** → `/laptops`
    
* **query** → `brand=hp&sort=price`
    
* **fragment** → `reviews`
    

---

✅ **In short:**

* **Web Resources** = Any static/dynamic file or service accessible on the web.
    
* **URL** = The complete web address used to locate and access those resources.
    
* URL or WebURL is used to uniquely identify the specific web resources within the web application.
    
* Every web application should have its unique adress in the form of url.
    

URL is the only way to access web applications vai browser.

### Syntax of URL

### protocol :// domainName:portNumber/resourcePath?queyString#fragmentId

### What is protocol ?

* When one application wants to communicate with other application, there need to be a common language that both applications understand each other ,Hence we use protocol.
    
* The protocol is a common language where two applications exchange information with each other.
    
* It is a set of rule and instructions.
    
* The browser always sends a request and receives a response vai HHTP protocol hence it is called HHTP-request / HTTP-response,
    

Its optional information and case insensitive

### Some other types of protocol are

* HTTP
    
* HTTPS
    
* FTP
    
* SMTP
    

### What is domain name?

* Used to uniquely identify the the specific computer / service within the network in which web application present.
    
* A domain name might be a computer name ot IP-adress
    
* It is mandotory information
    
    Ex: www.amazon.com
    

### What is port number ?

* Used to uniquely identify the specific software/applicatiuon within the computer/system.
    
* It is optional information in the webURL.
    
* The below table specify the defect port number.
    

### What is Resources path?

* Used to uniqly identify the specific Web resources within the application server(webapplication).
    
* EX:
    

### What is Query String ?

* It is one of the parameter passed in the URL which i used to specify / filter a condition.
    
* Query String always begins with ” **? “.**
    
* Query String is always written in **name = value** pairs\*\*.\*\*
    
* We can have any numbers of **name = value** pairs separated by “ **&** “ .
    

### What is fragmentID?

* Used to uniquely identify the specific fragment/ section within the webpage.
    
* FragmentID should always begain with “ **#** “.
    
* **EX**: #inbox, #Draft etc in gmail.
    

## **API PROTOCOLS**

### **1️⃣ REST (Representational State Transfer)**

* **Type:** Architectural style
    
* **Uses:** HTTP methods (`GET`, `POST`, `PUT`, `DELETE`)
    
* **Format:** JSON / XML
    
* **Best for:** Web & mobile APIs
    
* **Example:**
    
    ```java
    GET https://api.example.com/users
    ```
    
    ![](https://blog.postman.com/wp-content/uploads/2023/11/02_API_protocols-1024x390.jpg align="left")
    

---

### **2️⃣ Webhooks**

* **Type:** Event-driven callback mechanism
    
* **How it works:** Server **notifies client** via HTTP POST when an event occurs
    
* **Example:** Payment success → triggers webhook to client app
    
* **Use Case:** Real-time updates (payments, GitHub push, Slack message)
    

![](https://blog.postman.com/wp-content/uploads/2023/11/03_API_protocols-1024x977.jpg align="left")

---

### **3️⃣ GraphQL**

* **Type:** Query language for APIs
    
* **How it works:** Client requests **exact fields needed**
    
* **Advantage:** Reduces over-fetching and under-fetching
    
* **Example:**
    
    ```java
    { user { id name email } }
    ```
    

![](https://blog.postman.com/wp-content/uploads/2023/11/04_API_protocols-1024x695.jpg align="left")

---

### **4️⃣ SOAP (Simple Object Access Protocol)**

* **Type:** XML-based messaging protocol
    
* **Transport:** HTTP / SMTP
    
* **Structure:** Envelope + Header + Body
    
* **Use Case:** Enterprise-level, strict contracts
    
* **Example:** Banking, payment, legacy systems
    

![](https://blog.postman.com/wp-content/uploads/2023/11/05_API_protocols-1024x779.jpg align="left")

---

### **5️⃣ WebSocket**

* **Type:** Full-duplex communication channel
    
* **How it works:** Keeps a single connection open for both send & receive
    
* **Use Case:** Real-time apps (chat, games, stock updates)
    

![](https://blog.postman.com/wp-content/uploads/2023/11/06_API_protocols-1024x279.jpg align="left")

---

### **6️⃣ gRPC (Google Remote Procedure Call)**

* **Type:** High-performance binary protocol
    
* **Format:** Protocol Buffers (`.proto` files)
    
* **Languages:** Cross-language (Java, Python, Go, etc.)
    
* **Use Case:** Microservices communication
    

![](https://blog.postman.com/wp-content/uploads/2023/11/07_API_protocols-1024x775.jpg align="left")

---

### **7️⃣ MQTT (Message Queuing Telemetry Transport)**

* **Type:** Lightweight publish/subscribe protocol
    
* **Transport:** TCP/IP
    
* **Use Case:** IoT devices, low-bandwidth environments
    
* **Example:** Sensors → Broker → Subscribers
    

---

### **8️⃣ AMQP (Advanced Message Queuing Protocol)**

* **Type:** Open standard for messaging
    
* **Components:** Producer → Exchange → Queue → Consumer
    
* **Use Case:** Enterprise message brokers (RabbitMQ)
    

---

### **9️⃣ SSE (Server-Sent Events)**

* **Type:** One-way push from server to client via HTTP
    
* **Use Case:** Live feeds, notifications, dashboards
    
* **Difference from WebSocket:** One-direction (server → client only)
    

---

### **🔟 EDA (Event-Driven Architecture)**

* **Type:** Software design pattern
    
* **Flow:** Producer → Event Channel → Consumer
    
* **Use Case:** Scalable, async microservices (Kafka, RabbitMQ)
    

---

### **1️⃣1️⃣ EDI (Electronic Data Interchange)**

* **Type:** Standardized B2B data exchange format
    
* **Use Case:** Supply chain, invoicing, healthcare data
    
* **Format:** Plain text with specific structure (not JSON/XML)
    

---

## 🧩 **Summary Table**

| Protocol | Type | Format | Direction | Common Use |
| --- | --- | --- | --- | --- |
| **REST** | Architectural | JSON/XML | Request/Response | Web & Mobile APIs |
| **Webhooks** | Event callback | JSON | Server → Client | Notifications |
| **GraphQL** | Query language | JSON | Client ↔ Server | Custom data queries |
| **SOAP** | Protocol | XML | Request/Response | Enterprise systems |
| **WebSocket** | Communication | Binary/Text | Duplex | Real-time chat |
| **gRPC** | RPC Protocol | ProtoBuf | Duplex | Microservices |
| **MQTT** | Messaging | Binary | Pub/Sub | IoT |
| **AMQP** | Messaging | Binary | Pub/Sub | Enterprise queues |
| **SSE** | Stream | Text | Server → Client | Live data |
| **EDA** | Architecture | Event | Async | Microservices |
| **EDI** | Data format | Plain text | B2B | Business data exchange |

fsfsfsf