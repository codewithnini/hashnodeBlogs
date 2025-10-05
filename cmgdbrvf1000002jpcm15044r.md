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

# **2\. Types of APIs**

1. **Web APIs (REST, SOAP)** – over the internet
    
2. **Library/Framework APIs** – like `java.util`, `Selenium WebDriver API`
    
3. **Operating System APIs** – for file access, memory management
    

**Focus for Automation:** Web APIs (REST and SOAP)

---

# **3\. REST API vs SOAP API**

| Feature | REST | SOAP |
| --- | --- | --- |
| Protocol | HTTP | XML over HTTP/SOAP |
| Format | JSON / XML | XML only |
| Speed | Faster | Slower |
| State | Stateless | Stateful or Stateless |
| Use Case | Modern web services | Legacy systems |

**REST API** is more common in automation and modern apps.

---

# **4\. HTTP Methods in REST API**

| Method | Description |
| --- | --- |
| GET | Retrieve data from server |
| POST | Send data to server (create resource) |
| PUT | Update existing data |
| PATCH | Update part of resource |
| DELETE | Remove resource |

---

# **5\. REST API Request & Response**

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

# **6\. Tools to Test API**

1. **Postman** – GUI tool to send API requests
    
2. **Swagger** – API documentation & testing
    
3. **cURL** – command line tool
    
4. **RestAssured (Java)** – automation of API testing
    

---

# **7\. Java Example: Calling REST API**

**Using** `HttpURLConnection`:

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class TestAPI {
    public static void main(String[] args) {
        try {
            URL url = new URL("https://jsonplaceholder.typicode.com/posts/1");
            HttpURLConnection con = (HttpURLConnection) url.openConnection();
            con.setRequestMethod("GET");

            int status = con.getResponseCode();
            System.out.println("Status Code: " + status);

            BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
            String inputLine;
            StringBuilder content = new StringBuilder();
            while ((inputLine = in.readLine()) != null) {
                content.append(inputLine);
            }

            in.close();
            con.disconnect();

            System.out.println("Response Body: " + content);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Output:**

```java
Status Code: 200
Response Body: {"userId":1,"id":1,"title":"...","body":"..."}
```

---

# **8\. Using RestAssured for API Testing (Automation)**

**Add Maven Dependency:**

```java
<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>rest-assured</artifactId>
    <version>5.3.0</version>
    <scope>test</scope>
</dependency>
```

**Java Example:**

```java
import io.restassured.RestAssured;
import io.restassured.response.Response;

public class RestAssuredTest {
    public static void main(String[] args) {
        Response response = RestAssured.get("https://jsonplaceholder.typicode.com/posts/1");
        System.out.println("Status Code: " + response.getStatusCode());
        System.out.println("Response Body: " + response.getBody().asString());
    }
}
```

---

# **9\. API Automation Best Practices**

1. Validate **status codes**
    
2. Validate **response body** (data correctness)
    
3. Validate **headers and content-type**
    
4. Parameterize **URL and payload**
    
5. Use **JSON or XML schema validation**
    
6. Chain API calls if needed (create → get → update → delete)
    

---

# **10\. Real-World Example (Sales & Inventory Project)**

**Scenario:** Create a new product via API

* **POST** request to `/products`
    
* **Payload:**
    

```java
{
    "name": "Laptop",
    "price": 50000,
    "quantity": 10
}
```

* **Automation Validation:**
    
    * Check **status code 201**
        
    * Check **response body** contains `"name": "Laptop"`
        
    * Optionally, send **GET request** to confirm creation
        

---

# ✅ **Key Takeaways**

1. API allows **communication between apps**
    
2. **REST APIs** are modern, stateless, and use JSON
    
3. Java can call APIs using **HttpURLConnection** or **RestAssured**
    
4. API automation is **critical in testing modern applications**
    

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

## 🧭 **API PROTOCOLS**

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