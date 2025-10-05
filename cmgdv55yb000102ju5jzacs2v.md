---
title: "RestAssured"
datePublished: Sun Oct 05 2025 15:34:56 GMT+0000 (Coordinated Universal Time)
cuid: cmgdv55yb000102ju5jzacs2v
slug: restassured
tags: codewithnini

---

# **Authentication vs Authorization**

# often confused 👇

---

### 🧩 **1\. Authentication (Who are you?)**

**Definition:**  
Authentication is the process of **verifying a user’s identity** — checking if they really are who they claim to be.

**Example:**

* When you **log in** with your username and password, the system checks if they’re correct.
    
* If correct → you’re *authenticated* (you’ve proven your identity).
    

**Common Methods:**

* Username + Password
    
* OTP (One-Time Password)
    
* Biometrics (Fingerprint, Face ID)
    
* OAuth / SSO (e.g., Login with Google)
    

**Real-world analogy:**  
🔐 Showing your **ID card** to enter a building — it proves who you are.

---

### 🧱 **2\. Authorization (What can you do?)**

**Definition:**  
Authorization decides **what actions or resources you’re allowed to access** *after* you’ve been authenticated.

**Example:**

* A normal user can view data.
    
* An admin can view, edit, and delete data.
    
* Both are authenticated, but their **permissions** differ.
    

**Common Methods:**

* Role-Based Access Control (RBAC) → admin, user, guest
    
* Access tokens or scopes in APIs
    

**Real-world analogy:**  
🎫 Once you’re inside the building, your **access card** decides which rooms you can enter.

---

### 🔁 **3\. In Short:**

| Feature | Authentication | Authorization |
| --- | --- | --- |
| Purpose | Verifies identity | Grants permissions |
| Question | “Who are you?” | “What can you do?” |
| Happens | First | After authentication |
| Example | Login with username & password | Accessing admin panel |
| Real Example | Google sign-in page | Accessing Google Drive settings |

---

### ✅ **Simple Example (Web App):**

1. You open a website and **log in** → Authentication.
    
2. The system checks your **role (Admin/User)** → Authorization.
    
3. You can only see pages your role allows.
    

# 🔍 **Why API testing mostly uses *Authorization* and not *Authentication***

First, let’s recall the difference:

* **Authentication** → proves *who you are* (login process).
    
* **Authorization** → checks *what you can access* (permissions after login).
    

---

### 🧠 **1\. In API testing, authentication is usually already done**

* In real applications, **authentication (login)** is done once — like logging in through UI or generating a token (JWT, OAuth token, etc.).
    
* After that, all API calls use that **token** in headers to prove identity.
    
* So, testers don’t keep re-testing login for every API; they just **use a valid token** to access endpoints.
    

**Example:**

```java
GET /api/user/profile HTTP/1.1
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6...
```

👉 Here, you are not authenticating again — you’re already authenticated.  
You’re only **authorized** to access `/api/user/profile`.

---

### ⚙️ **2\. API Testing Focus = Business Logic + Access Control**

In API testing, the main goals are:

* ✅ Check correct response/data.
    
* ✅ Check role-based access (admin vs normal user).
    
* ✅ Check unauthorized access handling (403 Forbidden).
    

That’s why testers test **authorization**, not authentication again and again.

---

### 🔑 **3\. Authentication is usually tested once (or in UI testing)**

* Authentication (like login endpoints) are tested **only once** to confirm login works.
    
* After login, all other APIs just require the token → authorization testing.
    

---

### 🧩 **4\. In short:**

| Concept | Purpose | Where Used |
| --- | --- | --- |
| **Authentication** | Verify user identity (login) | Tested once or via UI |
| **Authorization** | Check user permissions | Tested for each API |
| **Why Authorization in API Testing** | To ensure users only access allowed resources | All protected APIs |

---

### 💬 **Example in Practice**

| Role | API | Expected Result |
| --- | --- | --- |
| Admin | GET /api/users | ✅ 200 OK (can view all users) |
| Normal User | GET /api/users | ❌ 403 Forbidden (not authorized) |

👉 This is **authorization testing** — you already have a token (authenticated), now you check access control.

---

✅ **Summary:**

> In API testing, **authentication** happens once (to get a token).  
> After that, testers mainly test **authorization** — to verify what the user *can* or *cannot* access.

# 🧩 **If the application front-end is not created yet...**

That means the **UI (like website or mobile app)** doesn’t exist —  
but the **backend APIs** (server-side logic) are already built.

So, what happens to **Authentication** and **Authorization** testing?

---

### ✅ **1\. You can still test APIs — even without the front-end**

APIs are **independent** of the UI.  
They can be tested directly using tools like:

* **Postman**
    
* **cURL**
    
* **Swagger / OpenAPI**
    
* **Rest Assured (Java)**
    
* **Newman / JMeter / Karate**
    

So, you can test all backend features — login, signup, data fetching, etc. — even before the UI is ready.

---

### ⚙️ **2\. Authentication (Login) API can still be tested**

If the backend team has created a **login API** (for example `/api/login`),  
you can test **authentication** directly in Postman.

**Example:**

```java
POST /api/login
Content-Type: application/json

{
  "username": "testuser",
  "password": "1234"
}
```

**Response:**

```java
{
  "token": "eyJhbGciOiJIUzI1NiIs..."
}
```

✅ You just got a **JWT token** → that means authentication works fine.

---

### 🔑 **3\. Use that token for Authorization testing**

Once you get the **token** from login API,  
you can use it to test other **protected APIs** (authorization).

**Example:**

```java
GET /api/user/profile
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

If you’re **authorized**, you’ll get a `200 OK` response.  
If not, you’ll get `403 Forbidden` or `401 Unauthorized`.

---

### 🚀 **4\. So, API Testing covers everything even before UI exists**

You can test:

* Authentication (login API works)
    
* Authorization (role-based access)
    
* CRUD operations (Create, Read, Update, Delete)
    
* Validations (missing fields, wrong input)
    
* Status codes and response times
    

✅ You can fully verify backend logic — even if UI is still being developed.

---

### 🧠 **5\. Real-world Example**

| Step | Action | Example API | Purpose |
| --- | --- | --- | --- |
| 1 | Test login | `POST /api/login` | Authentication |
| 2 | Get token | JWT in response | Used for further calls |
| 3 | Use token in header | `Authorization: Bearer <token>` | Authorization |
| 4 | Access protected data | `GET /api/orders` | Business logic test |
| 5 | Try without token | `GET /api/orders` | Should give `401 Unauthorized` |

---

### 💬 **In simple words:**

> Even if the frontend doesn’t exist,  
> you can test everything at **API level** — authentication, authorization, data flow, error handling —  
> using tools like **Postman** or **automation frameworks**.

# 🔐 **What is Cryptography?**

**Cryptography** is the **science of protecting information** by transforming it into a secure format so that only the intended people can read or use it.

In short:

> Cryptography = “Secret Writing”  
> It keeps data **confidential, authentic, and safe** during storage or transmission.

---

## 🧠 **Main Goal of Cryptography**

| Goal | Meaning | Example |
| --- | --- | --- |
| **Confidentiality** | Only authorized users can read the data | Encrypting passwords or messages |
| **Integrity** | Data cannot be changed or tampered with | Using hash functions to verify data |
| **Authentication** | Verifies identity of sender | Login credentials or digital signatures |
| **Non-repudiation** | Sender cannot deny sending the message | Digital signatures in emails |

---

## 🔑 **Four Main Components of Cryptography**

### 1\. **Plaintext**

* The original readable data.  
    Example:
    
    ```java
    Hello123
    ```
    

### 2\. **Encryption**

* The process of converting plaintext into unreadable text.  
    Example:
    
    ```java
    Hello123 → Xy$@91Zb#
    ```
    

### 3\. **Ciphertext**

* The encrypted (unreadable) version of the data.
    
    ```java
    Xy$@91Zb#
    ```
    

### 4\. **Decryption**

* The process of turning ciphertext back into plaintext.
    
    ```java
    Xy$@91Zb# → Hello123
    ```
    

---

## 🧩 **Types of Cryptography**

### 🔹 1. **Symmetric Key Cryptography**

* Uses **one single key** for both encryption and decryption.
    
* Fast but key must be kept secret.
    
* Example algorithms: **AES, DES, 3DES, Blowfish**
    
* Used in: File encryption, secure data storage.
    

🧠 **Example:**

```java
Key = 12345
Encrypt("Hello", 12345) → "M9x2#"
Decrypt("M9x2#", 12345) → "Hello"
```

---

### 🔹 2. **Asymmetric Key Cryptography**

* Uses **two keys**:
    
    * **Public key** → for encryption
        
    * **Private key** → for decryption
        
* More secure, commonly used in web security.
    
* Example algorithms: **RSA, DSA, ECC**
    
* Used in: HTTPS, SSL/TLS, JWTs, digital signatures.
    

🧠 **Example:**

```java
Public Key → Encrypt("Hello") → "M9x2#"
Private Key → Decrypt("M9x2#") → "Hello"
```

---

### 🔹 3. **Hashing**

* Converts data into a **fixed-length string**.
    
* It’s **one-way** → can’t be decrypted back.
    
* Used for: Password storage, data integrity checks.
    
* Example algorithms: **MD5, SHA-1, SHA-256**
    

🧠 **Example:**

```java
"password123" → SHA256 → "ef92b778ba... (hash)"
```

---

## 🌐 **Where Cryptography is Used**

| Area | Use Case |
| --- | --- |
| **Web Security** | HTTPS (SSL/TLS encryption) |
| **Emails** | Encrypting messages & attachments |
| **Databases** | Encrypting stored passwords |
| **APIs** | JWT tokens use cryptographic signatures |
| **Banking** | Encrypting transaction details |
| **Blockchain** | Cryptographic hashing & digital signatures |

---

## 🧾 **Simple Summary**

| Concept | What It Does | Example |
| --- | --- | --- |
| **Encryption** | Hide data | Encrypting login info |
| **Decryption** | Reveal data | Server decrypts messages |
| **Hashing** | Check integrity | Passwords stored as hash |
| **Public/Private Keys** | Secure exchange | Used in HTTPS |

---

✅ **In one line:**

> **Cryptography** is how we **secure data** — by encrypting it, verifying it, and ensuring only the right people can use it.

## 🔐 **What is Encryption and Decryption?**

### 🔹 **Encryption**

* It means **converting plain readable data (plaintext)** into **unreadable text (ciphertext)**.
    
* The goal is to **protect data** from being read or stolen by unauthorized people.
    
* It uses a **key** (like a secret password or algorithm) to scramble the data.
    

**Example:**

```java
Plain text:   Hello123
Encrypted:    Xy$@91Zb#
```

So even if someone steals the data, they can’t understand it.

---

### 🔹 **Decryption**

* It’s the **reverse process** of encryption.
    
* It **converts ciphertext back into readable form (plaintext)** using a key.
    
* Only authorized users with the **correct key** can decrypt the data.
    

**Example:**

```java
Encrypted: Xy$@91Zb#
Decrypted: Hello123
```

---

## 🧩 **Why Encryption & Decryption are Important**

* To **protect sensitive data** (passwords, bank info, tokens).
    
* To **secure communication** (between client and server).
    
* To **prevent hacking or sniffing** during data transfer.
    

---

## 🔑 **Types of Encryption**

### 1\. **Symmetric Encryption**

* **One key** is used for both encryption and decryption.
    
* Faster, but you must keep the key **secret**.
    

**Example Algorithms:**  
AES, DES, 3DES, Blowfish

**Example Flow:**

```java
Key: 12345
Encrypt("Hello") → "M9x2#"
Decrypt("M9x2#", 12345) → "Hello"
```

🟢 Used in: File encryption, database encryption.

---

### 2\. **Asymmetric Encryption**

* Uses **two keys**:
    
    * **Public Key** → for encryption
        
    * **Private Key** → for decryption
        
* Safer for internet communication.
    

**Example Algorithms:**  
RSA, DSA, ECC

**Example Flow:**

```java
Public Key: Encrypts → "M9x2#"
Private Key: Decrypts → "Hello"
```

🟢 Used in: HTTPS, SSL/TLS, digital signatures, JWT tokens.

---

## 🌐 **Real-World Example (HTTPS)**

When you visit a secure website (like [https://google.com](https://google.com)):

1. Browser and server **exchange publi****c keys**.
    
2. Browser **encrypts** your data using the server’s public key.
    
3. Server **decrypts** it with its private key.
    
4. Result: Your passwords and data stay safe while traveling over the internet.
    

---

## 🧠 **Simple Summary Table**

| Concept | Purpose | Key Type | Example Use |
| --- | --- | --- | --- |
| **Encryption** | Hide data | Public or Secret key | Sending secure data |
| **D****ecryption** | Reveal data | Same or paired key | Reading secure data |
| **Sym****metric Encryption** | Same key for both | Secret key | Database encryption |
| **Asymmetric Encryption** | Different keys | Public/Private | HTTPS, Email security |

## 🧩 **What is Encoding and Decoding?**

### 🔹 **Encoding**

* It is the process of **converting data from one format to another** so it can be **safely transmitted or stored**.
    
* It does **not** hide information — it just changes its format.
    
* Anyone can **decode** it back.
    

✅ **Purpose:** Compatibility, transmission, or storage (not security).

**Example:**

```java
Text: Hello World
Encoded (Base64): SGVsbG8gV29ybGQ=
```

---

### 🔹 **Decoding**

* It is the **reverse process** of encoding.
    
* Converts encoded data back to its **original format**.
    

**Example:**

```java
Encoded: SGVsbG8gV29ybGQ=
Decoded: Hello World
```

---

## ⚙️ **Encoding vs Encryption**

| Feature | Encoding | Encryption |
| --- | --- | --- |
| **Purpose** | Make data compatible for systems | Make data secret and secure |
| **Readable by anyone?** | Yes | No |
| **Uses a key?** | ❌ No | ✅ Yes |
| **Example** | Base64, ASCII, URL encoding | AES, RSA, DES |
| **Focus** | Format | Security |

---

## 🔤 **Common Types of Encoding**

| Type | Description | Example |
| --- | --- | --- |
| **Base64 Encoding** | Converts binary data into text format | Used in emails, JWT tokens |
| **URL Encoding** | Converts special characters to safe ones for URLs | Space → `%20` |
| **HTML Encoding** | Converts HTML symbols to entities | `<` → `&lt;` |
| **Character Encoding** | Represents characters in bytes | UTF-8, ASCII |

---

## 💡 **Simple Real Example**

When you send data through a **URL**:

```java
Actual: https://example.com?name=John Doe
Encoded: https://example.com?name=John%20Doe
```

`%20` replaces the space — that’s **URL encoding**.

---

## 🧠 **Quick Summary**

| Term | Meaning | Example |
| --- | --- | --- |
| **Encoding** | Change format | “Hello” → “SGVsbG8=” |
| **Decoding** | Reverse format | “SGVsbG8=” → “Hello” |
| **Encryption** | Secure data | “Hello” → “@x9&!” (needs key) |

## 🔐 **Encoding vs Encryption vs Hashing**

| Feature | **Encoding** | **Encryption** | **Hashing** |
| --- | --- | --- | --- |
| **Purpose** | To convert data into a compatible format for transmission or storage | To protect data and keep it secret | To verify data integrity (not reversible) |
| **Main Goal** | Data formatting | Data confidentiality | Data verification |
| **Reversible?** | ✅ Yes (using decoding) | ✅ Yes (using decryption key) | ❌ No (one-way) |
| **Uses a Key?** | ❌ No | ✅ Yes (secret key or public/private key) | ❌ No |
| **Example Algorithms / Methods** | Base64, ASCII, URL Encoding | AES, RSA, DES | MD5, SHA-256, SHA-512 |
| **Output** | Readable text | Unreadable ciphertext | Fixed-length hash value |
| **Example Input** | `Hello123` | `Hello123` | `Hello123` |
| **Example Output** | `SGVsbG8xMjM=` | `@#7Gx!k9` | `a12d45e7f3...` |
| **Used In** | Email, URLs, data transfer | HTTPS, login, JWT | Password storage, file checksums |
| **Can be reversed?** | Yes | Yes (if key known) | No |

---

### 💡 **Easy Way to Remember**

* 🧩 **Encoding** → For **formatting** (makes data safe to transmit)
    
* 🔒 **Encryption** → For **security** (hides data from others)
    
* 🧱 **Hashing** → For **verification** (check if data changed)
    

---

### ⚙️ **Real-Life Example**

| Action | Example |
| --- | --- |
| **Encoding** | Sending data in URL → `John Doe` → `John%20Doe` |
| **Encryption** | Login data sent securely via HTTPS |
| **Hashing** | Passwords stored in DB as hashes, not plain text |

## 🔐 **1️⃣ What is Authentication in APIs?**

Authentication = verifying *who* is accessing the API.  
In other words → the API wants to know:

> “Are you really who you claim to be?”

Without authentication, APIs can be misused or attacked.

---

## 🧱 **2️⃣ Common Types of Authentication in the Market**

| **Type** | **Description** | **Used In** |
| --- | --- | --- |
| **1\. Basic Authentication** | Username + Password (Base64 encoded) | Simple internal APIs |
| **2\. Digest Authentication** | Uses hashing + nonce (safer than Basic) | Legacy secure APIs |
| **3\. Bearer Token Authentication** | Token provided after login | Modern APIs (JWT, OAuth2) |
| **4\. OAuth 1.0 / OAuth 2.0** | Token-based; allows third-party access (without password) | Google, Facebook APIs |
| **5\. API Key Authentication** | Unique key in header or query param | Public APIs (e.g., OpenWeather, YouTube) |
| **6\. JWT (JSON Web Token)** | Encoded JSON token with user info, expiry, and signature | Microservices, Secure REST APIs |
| **7\. Hawk / AWS Signature / Custom Auth** | Special cryptographic signatures | AWS, Custom enterprise APIs |

---

## ⚙️ **3️⃣ Authentication Supported by Rest Assured**

✅ **Rest Assured supports:**

1. Basic Authentication
    
2. Digest Authentication
    
3. Form Authentication
    
4. OAuth 1.0
    
5. OAuth 2.0 (Bearer Token)
    
6. Preemptive and Challenged Auth types
    

---

## 🧩 **4️⃣ Implementation Examples in Rest Assured**

Let’s see how each works 👇

---

### 🧠 **1\. Basic Authentication**

➡️ Sends username and password in header (Base64 encoded)

```java
import io.restassured.RestAssured;
import io.restassured.response.Response;

public class BasicAuthExample {
    public static void main(String[] args) {
        Response response = RestAssured
            .given()
                .auth().basic("username", "password")
            .when()
                .get("https://api.example.com/users")
            .then()
                .statusCode(200)
                .extract().response();

        System.out.println(response.asPrettyString());
    }
}
```

🔍 *Header example:*  
`Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=`

---

### ⚙️ **2\. Digest Authentication**

➡️ More secure than Basic (uses hashing & nonce)

```java
given()
    .auth().digest("username", "password")
.when()
    .get("https://api.example.com/secure")
.then()
    .statusCode(200);
```

---

### 🧾 **3\. Preemptive Basic Authentication**

➡️ Sends credentials *immediately* instead of waiting for a 401 challenge.

```java
given()
    .auth().preemptive().basic("username", "password")
.when()
    .get("https://api.example.com/data")
.then()
    .statusCode(200);
```

---

### 🔑 **4\. OAuth 2.0 (Bearer Token)**

➡️ Most common in real APIs (Google, GitHub, etc.)

```java
given()
    .auth().oauth2("your-access-token-here")
.when()
    .get("https://api.github.com/user")
.then()
    .statusCode(200);
```

🔍 Header example:  
`Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6...`

---

### 🪙 **5\. API Key Authentication**

➡️ Some APIs use an API key instead of username/password.

```java
given()
    .header("x-api-key", "YOUR_API_KEY")
.when()
    .get("https://api.openweathermap.org/data/2.5/weather?q=London")
.then()
    .statusCode(200);
```

---

### 🧾 **6\. Form Authentication**

➡️ Used for login forms that return a session cookie.

```java
given()
    .auth()
    .form("username", "password", new FormAuthConfig("/login", "username", "password"))
.when()
    .get("/home")
.then()
    .statusCode(200);
```

---

## 🔒 **5️⃣ Which One to Use When**

| Type | Use Case |
| --- | --- |
| **Basic** | Internal API, testing purpose |
| **Digest** | When Basic is not secure enough |
| **Bearer (OAuth2)** | Most modern apps (JWT tokens) |
| **API Key** | Public APIs with limited access |
| **Form** | Login-based applications |

---

## 🧠 **6️⃣ Key Interview Question Tip**

> ❓Why is OAuth2 preferred over Basic Auth?

✅ Because:

* Password is not shared directly
    
* Tokens can expire / be revoked
    
* Supports scopes (limited permissions)
    
* Safer for public APIs
    

# **RestAssur****ed**

**RestAssured** is a **Java-based library** used for **testing RESTful A****PIs**.  
It supports all **HTTP** requests (GET, POST, PUT, PATCH, DELETE, etc.) and validate responses easily without writing a lot of boilerplate code.

Lets Assume as a tool that allows you to act like a browser or mobile app, but from your test scripts — so you can **send API calls, re****ceive responses, and verify** **them**.

---

## **Key Point****s**

* **Purpose** → Automates testing of REST APIs.
    
* **Language** → Java (can also be used in Kotlin, Groovy, etc.).
    
* **Inte****gration** → Works well with TestNG, JUnit, Maven, and Jenkins.
    
* **Data f****ormats sup****ported** → JSON, XML, HTML, and plain text.
    
* **Asse****rtions** → Built-in BDD-style syntax (`given-when-then`) and **Hamcrest match****ers** for validation.
    

---

## **Why QA & Au****tomation Testers U****se It**

1. No need to manually create `HttpURLConnection` or `HttpC``lient` code.
    
2. Supports **BDD-style syntax** → `given().when().then``()` makes scripts easy to read.
    
3. Can send requests with:
    
    * Query parameters
        
    * Path parameters
        
    * Headers
        
    * Cookies
        
    * Request body (JSON, XML, POJO)
        
4. Can validate:
    
    * Status codes
        
    * Response time
        
    * Headers
        
    * JSON/XML values
        
5. Can handle authentication (Basic, OAuth, etc.).
    

## Before going Deep we need to know some of concept Below

* ## Static import
    
* ## Method chaining
    
* ## RestAssured Class Daigram
    

### Static import in java

Java introduced the static import in JDK 1.5 . static import allows public and static members, i.e, fields and methods of a class to be used in java code without using specifying the class name.

```java
import static packageName.ClassName.*;
```

let’s break down **static import in Java** with an example, especially in the context of **RestAssured**.

---

## **1️⃣ What is Static Import?**

* Normally, when you call a static method or use a static field from another class, you write the **class name** before it:
    

```java
Math.sqrt(16);
System.out.println(Math.PI);
```

* **Static import** lets you use them **directly** without prefixing the class name:
    

```java
import static java.lang.Math.sqrt;
import static java.lang.Math.PI;

System.out.println(sqrt(16));
System.out.println(PI);
```

It basically makes static members look like they are in your own class.

---

## **2️⃣ Static Import in RestAssured**

In RestAssured, methods like `given()`, `when()`, `then()`, `get()`, and matchers like `equalTo()` are **static methods** in their classes.

### Without static import:

```java
import io.restassured.RestAssured;
import org.hamcrest.Matchers;

RestAssured.given()
    .when().get("https://reqres.in/api/users/2")
    .then().statusCode(200)
    .body("data.first_name", Matchers.equalTo("Janet"));
```

### With static import:

```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

given()
    .when().get("https://reqres.in/api/users/2")
    .then().statusCode(200)
    .body("data.first_name", equalTo("Janet"));
```

✅ **Benefits:**

* Cleaner & shorter code
    
* More readable in BDD-style API tests
    
* Matches natural language style:  
    `given() → when() → then()`
    

---

## **3️⃣ Full Working Example**

```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

public class StaticImportExample {
    public static void main(String[] args) {
        given()
            .baseUri("https://reqres.in")
        .when()
            .get("/api/users/2")
        .then()
            .statusCode(200)
            .body("data.first_name", equalTo("Janet"));
    }
}
```

**Explanation:**

* **given()** → Set up request (base URI, params, headers).
    
* **when()** → Send request (GET, POST, PUT, etc.).
    
* **then()** → Verify the response.
    

### Method Chaining in java.

Suppose there is a java class and it contains 3 static/non-static methods and we call each method as below.

```java
A a1 = new A();

a1.a().b().c();
```

**NOTE: To acheive method chaining**

1. A method return type should not void.
    
2. A method can return current class object.
    
3. A method can return other class object as well.
    
4. A method can return other interface reference object as well .
    

**Advantage of method chaining is the code optimization.**

### Rest Assured Class Architecture

## 🧩 Core Components of RestAssured

### 1\. **RestAssured (Class)**

* **Role**: Serves as the entry point for initiating API requests.
    
* **Key Methods**:
    
    * `given()`: Prepares a new request specification.
        
    * `when()`: Specifies the HTTP method to be executed.
        
    * `then()`: Validates the response and provides assertion methods.
        
    * `baseUri()`, `basePath()`, `port()`: Set global configurations for the API base URI, path, and port.
        
    * `auth()`: Configures authentication mechanisms.
        
    * `proxy()`: Sets up proxy configurations.
        
    * `config()`: Allows customization of the RestAssured configuration.
        

### 2\. **RequestSpecification (Interface)**

* **Role**: Defines the structure and configuration of an HTTP request.
    
* **Key Methods**:
    
    * `header()`, `queryParam()`, `formParam()`: Add headers and parameters to the request.
        
    * `body()`: Sets the request body.
        
    * `auth()`: Configures authentication for the request.
        
    * `config()`: Sets specific configurations for this request.
        
    * `spec()`: Allows reuse of existing request specifications.
        

### 3\. **RequestSender (Interface)**

* **Role**: Represents the action of sending an HTTP request.
    
* **Key Methods**:
    
    * `get()`, `post()`, `put()`, `delete()`, `patch()`: Execute the corresponding HTTP methods.
        
    * `then()`: Returns a `Response` object for further validation.
        

### 4\. **Response (Interface)**

* **Role**: Represents the HTTP response received after executing a request.
    
* **Key Methods**:
    
    * `getStatusCode()`, `getBody()`, `getHeader()`: Retrieve status code, body, and headers from the response.
        
    * `jsonPath()`, `xmlPath()`: Parse the response body as JSON or XML.
        
    * `then()`: Returns a `ValidatableResponse` for assertions.
        

### 5\. **ValidatableResponse (Interface)**

* **Role**: Provides methods to validate and assert the response.
    
* **Key Methods**:
    
    * `statusCode()`, `body()`, `header()`: Assert specific aspects of the response.
        
    * `log()`: Logs the response for debugging purposes.
        
    * `extract()`: Extracts data from the response for further use.
        

### 6\. **AuthenticationSpecification (Interface)**

* **Role**: Defines methods for configuring authentication mechanisms.
    
* **Key Methods**:
    
    * `basic()`, `certificate()`, `oauth2()`: Configure different authentication methods.
        
    * `preemptive()`: Sets up preemptive authentication.
        

### 7\. **Filter (Interface)**

* **Role**: Allows interception and modification of requests and responses.
    
* **Key Implementations**:
    
    * `RequestLoggingFilter`, `ResponseLoggingFilter`: Log request and response details.
        
    * `AuthenticationFilter`: Handles authentication during request execution.
        
    * `LoggingFilter`: Provides logging capabilities for requests and responses.
        

---

## 🔄 Method Chaining Flow

RestAssured's design supports method chaining through interfaces that return the same type or compatible types, enabling a fluent API. For example:

```java
given()
    .baseUri("https://api.example.com")
    .header("Authorization", "Bearer token")
    .body("{ \"name\": \"John\" }")
.when()
    .post("/users")
.then()
    .statusCode(201)
    .body("name", equalTo("John"));
```

In this example:

* `given()` returns a `RequestSpecification`.
    
* Methods like `baseUri()`, `header()`, and `body()` return the same `RequestSpecification`, allowing further configuration.
    
* `when()` returns a `RequestSender`.
    
* `post()` executes the HTTP POST method and returns a `Response`.
    
* `then()` returns a `ValidatableResponse` for assertions.
    

---

## 🧩 Summary Table

| **Component** | **Type** | **Role** |
| --- | --- | --- |
| `RestAssured` | Class | Entry point for initiating requests |
| `RequestSpecification` | Interface | Defines request structure and configuration |
| `RequestSender` | Interface | Represents the action of sending a request |
| `Response` | Interface | Represents the HTTP response |
| `ValidatableResponse` | Interface | Provides methods for response validation |
| `AuthenticationSpecification` | Interface | Configures authentication mechanisms |
| `Filter` | Interface | Allows interception and modification of requests and responses |

## **1️⃣ Overview of** `RestAssured` Class

* **Package**: `io.restassured.RestAssured`
    
* **Type**: Public class
    
* **Role**:  
    The `RestAssured` class is the **entry point** for creating requests in RestAssured.  
    It provides **static methods** to configure requests, set authentication, base URIs, logging, and more.
    

---

## **2️⃣ Key Static Fields**

| Field | Type | Description |
| --- | --- | --- |
| `baseURI` | String | Base URI for all requests (e.g., [`https://reqres.in`](https://reqres.in)) |
| `basePath` | String | Base path appended to the base URI |
| `port` | int | Port number for requests |
| `authenticationScheme` | AuthenticationScheme | Default authentication scheme (basic, oauth, etc.) |
| `filters` | List&lt;Filter&gt; | Default request/response filters applied globally |
| `config` | RestAssuredConfig | Global configuration object (timeouts, encoder, decoder, SSL, etc.) |

---

## **3️⃣ Key Static Methods**

### **Request Initialization**

| Method | Return Type | Description |
| --- | --- | --- |
| `given()` | RequestSpecification | Start building a request; the most common entry point |
| `when()` | RequestSender | Start defining the HTTP method to execute |
| `then()` | ValidatableResponse | Starts response validation directly from a request |

---

### **Configuration Methods**

| Method | Description |
| --- | --- |
| `baseURI(String uri)` | Set the global base URI |
| `basePath(String path)` | Set the global base path |
| `port(int port)` | Set the global port |
| `rootPath(String rootPath)` | Default JSON/XML root path for response validation |
| `config(RestAssuredConfig config)` | Apply global configuration |
| `filters(List<Filter> filters)` | Add filters globally |
| `authentication = AuthenticationScheme` | Set default authentication globally |

---

### **Authentication Methods**

| Method | Description |
| --- | --- |
| `auth().basic(user, pass)` | Basic authentication |
| `auth().digest(user, pass)` | Digest authentication |
| `auth().oauth2(token)` | OAuth2 authentication |
| `auth().preemptive().basic(user, pass)` | Preemptive authentication |

---

### **Logging & Filters**

* `filters()` – Apply global filters (logging, reporting)
    
* Common filters:
    
    * `RequestLoggingFilter`
        
    * `ResponseLoggingFilter`
        
    * `CustomFilter` (user-defined)
        

---

### **Example Usage**

```java
import static io.restassured.RestAssured.*;

public class RestAssuredExample {
    public static void main(String[] args) {
        // Global configuration
        baseURI = "https://reqres.in";
        port = 443;
        basePath = "/api";

        // Sending a POST request
        given()
            .header("Content-Type", "application/json")
            .body("{\"name\":\"John\", \"job\":\"Developer\"}")
        .when()
            .post("/users")
        .then()
            .statusCode(201)
            .log().all();
    }
}
```

**Explanation**:

* `given()` – Starts the request specification.
    
* `when().post("/users")` – Sends the HTTP POST request.
    
* `then()` – Validates the response.
    
* `baseURI`, `basePath`, and `port` are global static fields of `RestAssured`.
    

---

### **4️⃣ Internal Architecture of RestAssured Class**

1. **Static entry points**: `given()`, `when()`, `then()`
    
2. **Global configurations**: Base URI, base path, port, filters, and authentication.
    
3. **Delegation**:
    
    * `given()` returns `RequestSpecificationImpl`
        
    * `when()` returns `RequestSender`
        
    * `then()` returns `ValidatableResponseImpl`
        
4. **Filters & logging** are applied either globally (via `RestAssured.filters()`) or per request (via `RequestSpecification.filters()`).
    

---

### ✅ **Key Points**

* `RestAssured` is a **static utility class**; you rarely instantiate it.
    
* Most operations use **method chaining** starting from `given()`.
    
* It acts as a **facade** hiding the internal request/response objects.
    
* Supports **global configuration** and **per-request customization**.
    

## **1️⃣ Overview of RequestSpecification**

* **Package:** `io.restassured.specification`
    
* **Type:** Interface
    
* **Role:**  
    `RequestSpecification` represents a **request configuration** in RestAssured.  
    It contains **headers, query/form parameters, body, cookies, authentication, and more**.
    
* Returned by `RestAssured.given()` and acts as the starting point for building a request.
    

---

## **2️⃣ Key Methods of RequestSpecification**

### **A. Base Configuration**

| Method | Description |
| --- | --- |
| `baseUri(String uri)` | Sets the base URI for the request. |
| `basePath(String path)` | Sets the base path to append to the URI. |
| `port(int port)` | Sets the port for the request. |
| `rootPath(String path)` | Sets a default root path for JSON/XML response validation. |
| `config(RestAssuredConfig config)` | Apply request-specific configuration (timeouts, encoder/decoder, SSL). |

---

### **B. Headers and Cookies**

| Method | Description |
| --- | --- |
| `header(String name, Object value)` | Adds a single header. |
| `headers(Map<String,Object>)` | Add multiple headers at once. |
| `cookie(String name, Object value)` | Add a single cookie. |
| `cookies(Map<String,Object>)` | Add multiple cookies. |

---

### **C. Query, Form, Path Parameters**

| Method | Description |
| --- | --- |
| `queryParam(String name, Object value)` | Add a query parameter to the URL. |
| `queryParams(Map<String,Object>)` | Add multiple query parameters. |
| `pathParam(String name, Object value)` | Add path parameter for dynamic URL segments. |
| `formParam(String name, Object value)` | Add form parameters for `application/x-www-form-urlencoded` POST requests. |

---

### **D. Request Body**

| Method | Description |
| --- | --- |
| `body(Object object)` | Set the request body as string, JSON, or POJO. |
| `body(String body)` | Set the raw string body. |
| `body(byte[] bytes)` | Set binary data as body. |
| `multiPart(String controlName, Object file)` | Add file or form parts for multipart requests. |

---

### **E. Authentication**

| Method | Description |
| --- | --- |
| `auth()` | Returns `AuthenticationSpecification` for configuring authentication. |
| `auth().basic(user, pass)` | Basic auth. |
| `auth().digest(user, pass)` | Digest auth. |
| `auth().oauth2(token)` | OAuth2 token auth. |
| `auth().preemptive().basic(user, pass)` | Preemptive authentication. |

---

### **F. Logging and Filters**

| Method | Description |
| --- | --- |
| `log().all()` | Log all request details. |
| `log().headers()` | Log only headers. |
| `filters(List<Filter> filters)` | Apply filters (logging, reporting, custom). |

---

### **G. Miscellaneous**

| Method | Description |
| --- | --- |
| `accept(String mimeType)` | Set the Accept header. |
| `contentType(String mimeType)` | Set the Content-Type header. |
| `spec(RequestSpecification spec)` | Reuse an existing request specification. |
| `sessionId(String sessionId)` | Set session ID for request. |

---

## **3️⃣ Example Usage**

```java
import static io.restassured.RestAssured.*;
import io.restassured.specification.RequestSpecification;

public class RequestSpecExample {
    public static void main(String[] args) {
        RequestSpecification request = given()
            .baseUri("https://reqres.in")
            .basePath("/api")
            .header("Content-Type", "application/json")
            .queryParam("page", 2)
            .body("{\"name\":\"John\",\"job\":\"Developer\"}")
            .auth().basic("user", "pass");

        request
            .when().post("/users")
            .then().statusCode(201)
            .log().all();
    }
}
```

**Explanation**:

1. `given()` → Returns `RequestSpecification`.
    
2. `.baseUri()`, `.basePath()`, `.header()`, `.body()` → Configure request.
    
3. `.auth()` → Add authentication.
    
4. `request.when().post()` → Send request.
    
5. `.then()` → Validate response.
    

---

## **4️⃣ Internal Flow**

```java
RestAssured.given() → RequestSpecificationImpl
    └─ Stores all headers, params, body, cookies, authentication
    └─ Can attach filters and logging
    └─ Supports method chaining
RequestSpecification → RequestSender (when()) → Response → ValidatableResponse (then())
```

---

## **5️⃣ Key Points**

* `RequestSpecification` is **chainable**; most methods return the same object.
    
* Can be **global or reusable** by defining a `RequestSpecification` and passing it via `.spec()`.
    
* Encapsulates **all aspects of an HTTP request**: headers, params, body, cookies, authentication, logging.
    
* Core interface in **all RestAssured tests**.
    

## **1️⃣ Overview of** `RequestSender`

* **Package:** `io.restassured.specification`
    
* **Type:** Interface
    
* **Role:**  
    `RequestSender` is responsible for **sending the HTTP request** built via `RequestSpecification`.  
    It provides the HTTP method calls like `get()`, `post()`, `put()`, `delete()`, `patch()`, etc.
    
* Typically returned by `.when()` in RestAssured:
    

```java
given()            // RequestSpecification
.when()            // returns RequestSender
    .get("/users") // executes request
.then();           // ValidatableResponse
```

---

## **2️⃣ Key Methods of RequestSender**

### **A. HTTP Methods**

| Method | Description |
| --- | --- |
| `get(String path, Object... pathParams)` | Sends an HTTP GET request to the specified path. |
| `post(String path, Object... pathParams)` | Sends an HTTP POST request to the specified path. |
| `put(String path, Object... pathParams)` | Sends an HTTP PUT request to the specified path. |
| `delete(String path, Object... pathParams)` | Sends an HTTP DELETE request to the specified path. |
| `patch(String path, Object... pathParams)` | Sends an HTTP PATCH request to the specified path. |
| `head(String path, Object... pathParams)` | Sends an HTTP HEAD request to the specified path. |
| `options(String path, Object... pathParams)` | Sends an HTTP OPTIONS request to the specified path. |

> All HTTP methods return a `Response` object.

---

### **B. Formatted Requests**

* Methods also exist to **send requests with dynamic path parameters**:
    

```java
get("/users/{id}", 2)       // id=2 will replace {id} in path
post("/users/{id}", 3)      // id=3 will replace {id} in path
```

* This supports **path templating**.
    

---

### **C. Asynchronous and Specialized Requests**

* Some versions/extensions of RestAssured support **async requests** using `async()` (advanced usage).
    
* Multipart requests are typically configured via `RequestSpecification` rather than `RequestSender`.
    

---

## **3️⃣ Example Usage**

```java
import static io.restassured.RestAssured.*;

public class RequestSenderExample {
    public static void main(String[] args) {
        given()
            .baseUri("https://reqres.in")
            .basePath("/api")
            .queryParam("page", 2)
        .when()
            .get("/users")  // RequestSender executes GET
        .then()
            .statusCode(200)
            .log().all();
    }
}
```

**Flow Explained:**

1. `given()` → Returns `RequestSpecification`.
    
2. `.when()` → Returns `RequestSender`.
    
3. `.get("/users")` → Sends HTTP GET, returns `Response`.
    
4. `.then()` → Converts `Response` to `ValidatableResponse` for assertions.
    

---

## **4️⃣ Internal Flow**

```java
RequestSpecification → when() → RequestSender
    └─ Executes HTTP request via Apache HttpClient / Java HTTP client
    └─ Applies headers, body, params, cookies, filters
    └─ Returns Response
Response → then() → ValidatableResponse
```

---

## **5️⃣ Key Points**

* `RequestSender` is **stateless**; it simply executes the request built by `RequestSpecification`.
    
* Supports **all HTTP methods** (`GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, `OPTIONS`).
    
* Integrates **path parameters** and **query parameters** during execution.
    
* Works with **filters**, **authentication**, and **logging** applied in `RequestSpecification`.
    

---

If you want, I can prepare a **full RestAssured architecture diagram** showing **RequestSpecification → RequestSender → Response → ValidatableResponse**, including **filters and authentication flow** — it’s perfect for interview prep.

## **1️⃣ Overview of** `Response`

* **Package:** `io.restassured.response`
    
* **Type:** Interface
    
* **Role:**  
    `Response` encapsulates all the information received from the server after an HTTP request.  
    It provides **methods to access status codes, headers, cookies, body content**, and allows **parsing JSON/XML responses**.
    
* Returned by `RequestSender` methods like `get()`, `post()`, `put()`, `delete()`, etc.
    

```java
Response response = given()
                        .baseUri("https://reqres.in")
                        .basePath("/api")
                    .when()
                        .get("/users/2");
```

---

## **2️⃣ Key Methods of Response**

### **A. Status and Line**

| Method | Description |
| --- | --- |
| `getStatusCode()` | Returns HTTP status code (e.g., 200, 404). |
| `getStatusLine()` | Returns the full HTTP status line (e.g., "HTTP/1.1 200 OK"). |
| `getDetailedCookies()` | Returns cookies as a map. |
| `getContentType()` | Returns the Content-Type header. |

---

### **B. Headers**

| Method | Description |
| --- | --- |
| `getHeader(String name)` | Returns the value of a specific header. |
| `getHeaders()` | Returns all headers as `Headers` object. |
| `hasHeaderWithName(String name)` | Checks if a header exists. |

---

### **C. Cookies**

| Method | Description |
| --- | --- |
| `getCookie(String name)` | Get a specific cookie. |
| `getCookies()` | Returns all cookies as a `Map<String, String>`. |

---

### **D. Response Body**

| Method | Description |
| --- | --- |
| `getBody()` | Returns the body as a `ResponseBody` object. |
| `asString()` | Returns body as a raw string. |
| `asByteArray()` | Returns body as bytes. |
| `as(InputStream.class)` | Returns body as input stream. |

---

### **E. JSON/XML Parsing**

| Method | Description |
| --- | --- |
| `jsonPath()` | Returns `JsonPath` object to query JSON body using GPath expressions. |
| `xmlPath()` | Returns `XmlPath` object to query XML body using GPath expressions. |

**Example:**

```java
String firstName = response.jsonPath().getString("data.first_name");
String lastName = response.jsonPath().getString("data.last_name");
```

---

### **F. Validations**

* `then()` → Converts `Response` into `ValidatableResponse` for assertions.
    
* Example:
    

```java
response.then().statusCode(200).body("data.id", equalTo(2));
```

---

### **G. Miscellaneous**

| Method | Description |
| --- | --- |
| `prettyPrint()` | Prints response body in readable format. |
| `prettyPeek()` | Prints response and returns it for chaining. |
| `peek()` | Prints a summary of the response (status, headers). |
| `path(String path)` | Extracts value from body using GPath. |
| `as(Class<T> cls)` | Deserialize response body into a POJO. |

---

## **3️⃣ Example Usage**

```java
import static io.restassured.RestAssured.*;
import io.restassured.response.Response;

public class ResponseExample {
    public static void main(String[] args) {
        Response response = given()
                                .baseUri("https://reqres.in")
                                .basePath("/api")
                            .when()
                                .get("/users/2");

        // Status and headers
        System.out.println(response.getStatusCode());
        System.out.println(response.getHeader("Content-Type"));

        // Body as string
        System.out.println(response.asString());

        // Extract JSON value
        String firstName = response.jsonPath().getString("data.first_name");
        System.out.println(firstName);

        // Validatable
        response.then().statusCode(200).body("data.id", equalTo(2));
    }
}
```

---

## **4️⃣ Internal Flow**

```java
RequestSpecification → RequestSender (when()) → Response
    └─ Captures HTTP status code, headers, cookies, body
    └─ Provides methods for parsing (JSON, XML)
    └─ Supports logging and validation via then()
```

---

## **5️⃣ Key Points**

* `Response` is **immutable**; it reflects the server’s returned data.
    
* Works seamlessly with **JSON/XML parsing**, **POJO deserialization**, and **GPath expressions**.
    
* Enables **method chaining** by converting into `ValidatableResponse`.
    
* Supports both **raw data access** (asString(), asByteArray()) and **structured access** (jsonPath(), xmlPath()).
    

---

If you want, I can continue with a **detailed deep dive into** `ValidatableResponse` next, completing the RestAssured **core interface chain** from `RequestSpecification → RequestSender → Response → ValidatableResponse`.

## **1️⃣ Overview of** `ValidatableResponse`

* **Package:** `io.restassured.response`
    
* **Type:** Interface
    
* **Role:**  
    `ValidatableResponse` represents a **response after execution** that can be **validated/asserted**.  
    It is returned by `Response.then()` and supports **method chaining** for fluent assertions.
    

```java
ValidatableResponse validatable = 
    given().when().get("/users/2").then();
```

---

## **2️⃣ Key Methods of ValidatableResponse**

### **A. Status Code & Line Validation**

| Method | Description |
| --- | --- |
| `statusCode(int expected)` | Validate exact HTTP status code. |
| `statusLine(String expected)` | Validate the full status line. |
| `statusCode(Matcher<Integer> matcher)` | Use Hamcrest matcher for status code validation. |

**Example:**

```java
response.then().statusCode(200).statusLine("HTTP/1.1 200 OK");
```

---

### **B. Header Validation**

| Method | Description |
| --- | --- |
| `header(String name, Matcher<?> matcher)` | Validate a specific header with a matcher. |
| `headers(String name1, Matcher<?> m1, String name2, Matcher<?> m2, ...)` | Validate multiple headers at once. |
| `contentType(String expected)` | Validate Content-Type header. |

---

### **C. Body Validation**

| Method | Description |
| --- | --- |
| `body(String path, Matcher<?> matcher)` | Validate JSON/XML response body using GPath. |
| `body(Matcher<?> matcher)` | Validate full body content. |
| `body(String path, Object... expectedValues)` | Validate body values at given path. |

**Example:**

```java
response.then()
        .body("data.id", equalTo(2))
        .body("data.first_name", equalTo("Janet"));
```

---

### **D. Cookie Validation**

| Method | Description |
| --- | --- |
| `cookie(String name, Matcher<?> matcher)` | Validate a specific cookie. |
| `cookies(Matcher<Map<String, ?>> matcher)` | Validate all cookies. |

---

### **E. Logging**

| Method | Description |
| --- | --- |
| `log().all()` | Log status, headers, body. |
| `log().headers()` | Log only headers. |
| `log().body()` | Log only body. |
| `log().ifValidationFails()` | Log only if a validation fails. |

---

### **F. Extracting Data**

* `extract()` returns `ExtractableResponse<Response>` to extract data for later use.
    
* Example:
    

```java
String firstName = response.then()
                           .extract()
                           .path("data.first_name");
```

---

### **G. Advanced Validation**

* Supports **Hamcrest matchers** for complex assertions:
    

```java
response.then()
        .body("data.id", allOf(greaterThan(0), lessThan(10)))
        .body("data.first_name", startsWith("J"));
```

* Supports **multiple path assertions** in a single call.
    

---

## **3️⃣ Example Usage**

```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;

public class ValidatableResponseExample {
    public static void main(String[] args) {
        given()
            .baseUri("https://reqres.in")
            .basePath("/api")
        .when()
            .get("/users/2")
        .then()
            .statusCode(200)
            .contentType("application/json; charset=utf-8")
            .body("data.id", equalTo(2))
            .body("data.first_name", equalTo("Janet"))
            .log().all();
    }
}
```

**Explanation:**

* `then()` → Converts `Response` into `ValidatableResponse`.
    
* `.statusCode()`, `.body()` → Validate status code and response body.
    
* `.log().all()` → Logs response details.
    

---

## **4️⃣ Internal Flow**

```java
RequestSpecification → RequestSender → Response → then() → ValidatableResponse
    └─ Provides assertion methods
    └─ Supports logging
    └─ Allows extraction for further processing
```

---

## **5️⃣ Key Points**

* `ValidatableResponse` is **immutable** and **chainable**.
    
* Supports **status, headers, body, cookies, and content-type validation**.
    
* Works seamlessly with **Hamcrest matchers** for flexible and readable assertions.
    
* `.extract()` allows you to **reuse response data** for subsequent requests or assertions.
    
* Usually the **last step in RestAssured chain** for validation.
    

---

✅ After this, we have fully covered **the RestAssured core chain**:

```java
RequestSpecification → RequestSender → Response → ValidatableResponse
```

## **1️⃣ Overview of** `ResponseSpecification`

* **Package:** `io.restassured.specification`
    
* **Type:** Interface
    
* **Role:**  
    `ResponseSpecification` defines **reusable response expectations**.  
    Instead of writing the same assertions repeatedly, you can define a **response specification** and reuse it across multiple requests.
    

```java
ResponseSpecification responseSpec = new ResponseSpecBuilder()
                                        .expectStatusCode(200)
                                        .expectContentType("application/json")
                                        .build();
```

* Returned by `Response.then()` after applying a `ResponseSpecification`.
    

---

## **2️⃣ Key Methods**

### **A. Status & Headers**

| Method | Description |
| --- | --- |
| `expectStatusCode(int statusCode)` | Expect a specific status code. |
| `expectStatusLine(String statusLine)` | Expect a full status line. |
| `expectHeader(String name, Matcher<?> matcher)` | Expect a header with a specific value. |
| `expectHeaders(Map<String, ?> headers)` | Expect multiple headers. |
| `expectContentType(String contentType)` | Expect Content-Type of response. |

---

### **B. Body Validation**

| Method | Description |
| --- | --- |
| `expectBody(String path, Matcher<?> matcher)` | Expect JSON/XML path value using GPath. |
| `expectBody(Matcher<?> matcher)` | Expect full body content to match. |

---

### **C. Cookies**

| Method | Description |
| --- | --- |
| `expectCookie(String name, Matcher<?> matcher)` | Expect a specific cookie. |
| `expectCookies(Map<String, ?> cookies)` | Expect multiple cookies. |

---

### **D. Miscellaneous**

| Method | Description |
| --- | --- |
| `apply(Response response)` | Apply the specification to a `Response`. |
| `log()` | Logging of response validation. |

---

## **3️⃣ Example Usage**

```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;
import io.restassured.builder.ResponseSpecBuilder;
import io.restassured.specification.ResponseSpecification;

public class ResponseSpecExample {
    public static void main(String[] args) {
        // Define a reusable response specification
        ResponseSpecification responseSpec = new ResponseSpecBuilder()
            .expectStatusCode(200)
            .expectContentType("application/json; charset=utf-8")
            .expectBody("data.id", equalTo(2))
            .build();

        // Use it in a request
        given()
            .baseUri("https://reqres.in")
            .basePath("/api")
        .when()
            .get("/users/2")
        .then()
            .spec(responseSpec)
            .log().all();
    }
}
```

**Explanation:**

* `ResponseSpecBuilder` → Builds a reusable `ResponseSpecification`.
    
* `.expectStatusCode()`, `.expectBody()` → Define assertions.
    
* `.spec(responseSpec)` → Applies specification to the current response.
    
* `.log().all()` → Logs the validated response.
    

---

## **4️⃣ Benefits of ResponseSpecification**

1. **Reusability:** Define common expectations once, use in multiple tests.
    
2. **Readability:** Keeps test code clean.
    
3. **Maintainability:** Update the spec once, all tests using it reflect changes.
    
4. **Integration with ValidatableResponse:** Applied via `.spec()` after `then()`.
    

---

## **5️⃣ Flow in RestAssured Chain**

```java
RequestSpecification → RequestSender → Response → then() → ValidatableResponse
                                                                │
                                                                └─ spec(ResponseSpecification)
```

* `ResponseSpecification` is **not mandatory**, but it’s great for **reusable validations**.
    

## **1️⃣ Overview of** `ResponseSpecification`

* **Package:** `io.restassured.specification`
    
* **Type:** Interface
    
* **Role:**  
    `ResponseSpecification` defines **reusable response expectations**.  
    Instead of writing the same assertions repeatedly, you can define a **response specification** and reuse it across multiple requests.
    

```java
ResponseSpecification responseSpec = new ResponseSpecBuilder()
                                        .expectStatusCode(200)
                                        .expectContentType("application/json")
                                        .build();
```

* Returned by `Response.then()` after applying a `ResponseSpecification`.
    

---

## **2️⃣ Key Methods**

### **A. Status & Headers**

| Method | Description |
| --- | --- |
| `expectStatusCode(int statusCode)` | Expect a specific status code. |
| `expectStatusLine(String statusLine)` | Expect a full status line. |
| `expectHeader(String name, Matcher<?> matcher)` | Expect a header with a specific value. |
| `expectHeaders(Map<String, ?> headers)` | Expect multiple headers. |
| `expectContentType(String contentType)` | Expect Content-Type of response. |

---

### **B. Body Validation**

| Method | Description |
| --- | --- |
| `expectBody(String path, Matcher<?> matcher)` | Expect JSON/XML path value using GPath. |
| `expectBody(Matcher<?> matcher)` | Expect full body content to match. |

---

### **C. Cookies**

| Method | Description |
| --- | --- |
| `expectCookie(String name, Matcher<?> matcher)` | Expect a specific cookie. |
| `expectCookies(Map<String, ?> cookies)` | Expect multiple cookies. |

---

### **D. Miscellaneous**

| Method | Description |
| --- | --- |
| `apply(Response response)` | Apply the specification to a `Response`. |
| `log()` | Logging of response validation. |

---

## **3️⃣ Example Usage**

```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;
import io.restassured.builder.ResponseSpecBuilder;
import io.restassured.specification.ResponseSpecification;

public class ResponseSpecExample {
    public static void main(String[] args) {
        // Define a reusable response specification
        ResponseSpecification responseSpec = new ResponseSpecBuilder()
            .expectStatusCode(200)
            .expectContentType("application/json; charset=utf-8")
            .expectBody("data.id", equalTo(2))
            .build();

        // Use it in a request
        given()
            .baseUri("https://reqres.in")
            .basePath("/api")
        .when()
            .get("/users/2")
        .then()
            .spec(responseSpec)
            .log().all();
    }
}
```

**Explanation:**

* `ResponseSpecBuilder` → Builds a reusable `ResponseSpecification`.
    
* `.expectStatusCode()`, `.expectBody()` → Define assertions.
    
* `.spec(responseSpec)` → Applies specification to the current response.
    
* `.log().all()` → Logs the validated response.
    

---

## **4️⃣ Benefits of ResponseSpecification**

1. **Reusability:** Define common expectations once, use in multiple tests.
    
2. **Readability:** Keeps test code clean.
    
3. **Maintainability:** Update the spec once, all tests using it reflect changes.
    
4. **Integration with ValidatableResponse:** Applied via `.spec()` after `then()`.
    

---

## **5️⃣ Flow in RestAssured Chain**

```java
RequestSpecification → RequestSender → Response → then() → ValidatableResponse
                                                                │
                                                                └─ spec(ResponseSpecification)
```

* `ResponseSpecification` is **not mandatory**, but it’s great for **reusable validations**.
    

## **1️⃣ Overview of** `ResponseSpecBuilder`

* **Package:** `io.restassured.builder`
    
* **Type:** Class
    
* **Role:**  
    `ResponseSpecBuilder` helps you **create reusable** `ResponseSpecification` objects.  
    Instead of writing the same assertions for multiple tests, you define them once with a builder.
    

```java
ResponseSpecification responseSpec = new ResponseSpecBuilder()
                                        .expectStatusCode(200)
                                        .expectContentType("application/json")
                                        .build();
```

* `build()` → Returns a `ResponseSpecification` object.
    

---

## **2️⃣ Key Methods of ResponseSpecBuilder**

### **A. Status and Line**

| Method | Description |
| --- | --- |
| `expectStatusCode(int statusCode)` | Expect a specific HTTP status code. |
| `expectStatusLine(String statusLine)` | Expect a full HTTP status line. |
| `expectStatusCode(Matcher<Integer> matcher)` | Use Hamcrest matcher for status code. |

---

### **B. Headers**

| Method | Description |
| --- | --- |
| `expectHeader(String name, Matcher<?> matcher)` | Expect a specific header value. |
| `expectHeaders(Map<String, ?> headers)` | Expect multiple headers at once. |
| `expectContentType(String contentType)` | Expect a specific Content-Type header. |

---

### **C. Body Validation**

| Method | Description |
| --- | --- |
| `expectBody(String path, Matcher<?> matcher)` | Validate JSON/XML response body at a given path using GPath. |
| `expectBody(Matcher<?> matcher)` | Validate entire response body. |
| `expectBody(String path, Object... expectedValues)` | Validate body values for given path. |

---

### **D. Cookies**

| Method | Description |
| --- | --- |
| `expectCookie(String name, Matcher<?> matcher)` | Expect a specific cookie. |
| `expectCookies(Map<String, ?> cookies)` | Expect multiple cookies. |

---

### **E. Logging**

| Method | Description |
| --- | --- |
| `log()` | Enable logging for response validation (optional). |

---

### **F. Build**

| Method | Description |
| --- | --- |
| `build()` | Builds the `ResponseSpecification` object. |

---

## **3️⃣ Example Usage**

```java
import static io.restassured.RestAssured.*;
import static org.hamcrest.Matchers.*;
import io.restassured.builder.ResponseSpecBuilder;
import io.restassured.specification.ResponseSpecification;

public class ResponseSpecBuilderExample {
    public static void main(String[] args) {
        // Build reusable response specification
        ResponseSpecification responseSpec = new ResponseSpecBuilder()
            .expectStatusCode(200)
            .expectContentType("application/json; charset=utf-8")
            .expectBody("data.id", equalTo(2))
            .build();

        // Apply the response spec in a request
        given()
            .baseUri("https://reqres.in")
            .basePath("/api")
        .when()
            .get("/users/2")
        .then()
            .spec(responseSpec)   // Apply reusable spec
            .log().all();
    }
}
```

**Explanation:**

* `ResponseSpecBuilder` → Define common response expectations once.
    
* `.build()` → Returns `ResponseSpecification`.
    
* `.spec(responseSpec)` → Apply the specification to a response.
    

---

## **4️⃣ Benefits**

1. **Reusability:** Define common response validations once and reuse.
    
2. **Readability:** Keeps test code clean and avoids repeated assertions.
    
3. **Maintainability:** Update the spec once, all tests reflect changes.
    
4. **Supports Method Chaining:** Fluent API for building complex validation rules.
    

---

✅ After this, we have covered all **builders in RestAssured**:

```java
RequestSpecBuilder → RequestSpecification → RequestSender → Response → ValidatableResponse → ResponseS
```

## **1️⃣ Overview of** `AuthenticationScheme`

* **Package:** `io.restassured.authentication`
    
* **Type:** Interface
    
* **Role:**  
    `AuthenticationScheme` is the **base interface** for all authentication types in RestAssured.  
    It allows **RequestSpecification** to set authentication when sending requests.
    
* Implemented by classes like:
    
    * `BasicAuthScheme` → Basic Authentication
        
    * `DigestAuthScheme` → Digest Authentication
        
    * `OAuth2Scheme` → OAuth2 Authentication
        
    * `PreemptiveBasicAuthScheme` → Preemptive Basic Auth
        
* Typically used via `RequestSpecification.auth()`:
    

```java
given().auth().basic("username", "password");
```

Internally, `basic()` creates a `BasicAuthScheme` object implementing `AuthenticationScheme`.

---

## **2️⃣ Key Methods of AuthenticationScheme**

| Method | Description |
| --- | --- |
| `void authenticate(RequestSpecification requestSpec)` | Applies the authentication to the request. |
| `String getUsername()` | Returns username (for Basic/Digest). |
| `String getPassword()` | Returns password (for Basic/Digest). |
| `String getAccessToken()` | Returns access token (for OAuth2). |

> Note: Exact methods depend on the implementing class. The interface ensures **any authentication scheme** can be applied to a request.

---

## **3️⃣ Common Implementations**

### **A. BasicAuthScheme**

* Implements `AuthenticationScheme`.
    
* Adds **Basic HTTP authentication header**.
    

```java
given().auth().basic("user", "pass");
```

### **B. DigestAuthScheme**

* Implements `AuthenticationScheme`.
    
* Handles **Digest authentication** challenge-response.
    

```java
given().auth().digest("user", "pass");
```

### **C. OAuth2Scheme**

* Implements `AuthenticationScheme`.
    
* Adds **Bearer token** to `Authorization` header.
    

```java
given().auth().oauth2("token");
```

### **D. PreemptiveBasicAuthScheme**

* Implements `AuthenticationScheme`.
    
* Sends **Basic Auth header immediately** without waiting for server challenge.
    

```java
given().auth().preemptive().basic("user", "pass");
```

---

## **4️⃣ Usage Example**

```java
import static io.restassured.RestAssured.*;

public class AuthenticationExample {
    public static void main(String[] args) {
        given()
            .baseUri("https://reqres.in")
            .basePath("/api")
            .auth().basic("user", "pass")   // BasicAuthScheme applied
        .when()
            .get("/users/2")
        .then()
            .statusCode(200)
            .log().all();
    }
}
```

**Explanation:**

1. `auth().basic()` → Creates a `BasicAuthScheme`.
    
2. `AuthenticationScheme.authenticate()` → Internally adds header to the request.
    
3. Request is executed with authentication.
    

---

## **5️⃣ Key Points**

* `AuthenticationScheme` is **an interface**, so new authentication types can be added.
    
* Used by **RequestSpecification** to apply authentication before sending requests.
    
* Supports multiple types:
    
    * Basic
        
    * Digest
        
    * OAuth1/OAuth2
        
    * Preemptive authentication
        
* Works seamlessly with **RequestSpecBuilder** or **RequestSpecification** for reusable authentication.
    

---

If you want, I can now create a **complete UML class/interface diagram for RestAssured** showing:

```java
RestAssured → RequestSpecification → RequestSender → Response → ValidatableResponse → ResponseSpecification
+ RequestSpecBuilder, ResponseSpecBuilder
+ AuthenticationScheme → Basic/Digest/OAuth
+ Filters & Logging
```

### Sample Test Using Method chaining.

### Before static import»»»

```java
package sampleTest;

import org.testng.annotations.Test;

import io.restassured.RestAssured;
import io.restassured.response.Response;

public class SampleTsetUsingMethodChaning {
	@Test
	public static void getAllEmployeesAvailable() {
		
	Response resp = RestAssured.get("http://49.249.28.218:8091/all-employees");
	resp.prettyPeek();
	}

}
```

Here we use the class name to use the **get()** method.

### After static import»»»

```java
package sampleTest;

import static io.restassured.RestAssured.*;

import org.testng.annotations.Test;

public class SampleTsetUsingMethodChaning2 {
	@Test
	public static void getAllEmployeesAvailable() {
		
	get("http://49.249.28.218:8091/all-employees")
	.prettyPeek();
	}

}
```

Here we not using the class name as reference ,this is the magic of **static** import.