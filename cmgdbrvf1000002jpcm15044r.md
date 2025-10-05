---
title: "API - Application Programming Interface"
datePublished: Sun Oct 05 2025 06:32:43 GMT+0000 (Coordinated Universal Time)
cuid: cmgdbrvf1000002jpcm15044r
slug: api-application-programming-interface
tags: codewithnini

---

# **1\. What is an API?**

**API (Application Programming Interface)** is a **set of rules that allows two applications or systems to communicate**.

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