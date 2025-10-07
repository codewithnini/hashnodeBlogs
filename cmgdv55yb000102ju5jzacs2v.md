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

1. Browser and server **exchange publi\*\*\*\*c keys**.
    
2. Browser **encrypts** your data using the server’s public key.
    
3. Server **decrypts** it with its private key.
    
4. Result: Your passwords and data stay safe while traveling over the internet.
    

---

## 🧠 **Simple Summary Table**

| Concept | Purpose | Key Type | Example Use |
| --- | --- | --- | --- |
| **Encryption** | Hide data | Public or Secret key | Sending secure data |
| **D\*\*\*\*ecryption** | Reveal data | Same or paired key | Reading secure data |
| **Sym\*\*\*\*metric Encryption** | Same key for both | Secret key | Database encryption |
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
    

# **RestAssur\*\*\*\*ed**

**RestAssured** is a **Java-based library** used for **testing RESTful A\*\*\*\*PIs**.  
It supports all **HTTP** requests (GET, POST, PUT, PATCH, DELETE, etc.) and validate responses easily without writing a lot of boilerplate code.

Lets Assume as a tool that allows you to act like a browser or mobile app, but from your test scripts — so you can **send API calls, re\*\*\*\*ceive responses, and verify** **them**.

---

## **Key Point\*\*\*\*s**

* **Purpose** → Automates testing of REST APIs.
    
* **Language** → Java (can also be used in Kotlin, Groovy, etc.).
    
* **Inte\*\*\*\*gration** → Works well with TestNG, JUnit, Maven, and Jenkins.
    
* **Data formats supported** → JSON, XML, HTML, and plain text.
    
* **Asse\*\*\*\*rtions** → Built-in BDD-style syntax (`given-when-then`) and **Hamcrest match\*\*\*\*ers** for validation.
    

---

## **Why QA & Automation Testers Use It**

1. No need to manually create `HttpURLConnection` or `HttpClient` code.
    
2. Supports **BDD-style syntax** → `given().when().then()` makes scripts easy to read.
    
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

# Rest Assured Class Architecture

# 🧩 REST ASSURED ALL COMPONENTS

## 1\. `io.restassured.RestAssured` (Main entry & config class)

**Purpose / How used:**

* Global configuration entry point
    
* Static methods for starting requests
    
* Holds static fields for default request/response specs and config
    

| Method / Field | Return / Type | Use / Shortcut | Notes |
| --- | --- | --- | --- |
| `baseURI` | `String` | Set base URI for all requests | e.g. `RestAssured.baseURI = "`[`https://api.example.com`](https://api.example.com)`"` |
| `basePath` | `String` | Set base path appended to baseURI | e.g. `RestAssured.basePath = "/v1"` |
| `port` | `int` | Set default port | e.g. `RestAssured.port = 443` |
| `requestSpecification` | `RequestSpecification` | Global default request spec | All requests use this if no spec given |
| `responseSpecification` | `ResponseSpecification` | Global default response spec | Apply default validation |
| `defaultParser` | `Parser` | Default parser for unknown content-types | e.g. `Parser.JSON` |
| `authentication` | `AuthenticationScheme` | Default authentication scheme | Applied to all requests |
| `urlEncodingEnabled(boolean)` | void | Enable or disable URL encoding | `RestAssured.urlEncodingEnabled = false` |
| `given()` | `RequestSpecification` | Start building a request | `given().header(...).when().get(...)` |
| `with()` | `RequestSpecification` | Alias for `given()` | Same as `given()` |
| `when()` | `RequestSpecification` / `RequestSender` | For readability / chaining | Usually after `given()` |
| `expect()` | `ResponseSpecification` | Validation alias (older style) | Equivalent to `.then()` |
| `get(String path)` | `Response` | Send GET to path | Shortcut for `given().when().get(path)` |
| `post(String path)` | `Response` | Send POST to path |  |
| `put(String path)` | `Response` | Send PUT to path |  |
| `delete(String path)` | `Response` | Send DELETE to path |  |
| `patch(String path)` | `Response` | Send PATCH to path |  |
| `options(String path)` | `Response` | Send OPTIONS |  |
| `head(String path)` | `Response` | Send HEAD |  |
| `config(RestAssuredConfig config)` | void | Set config settings | e.g. timeouts, SSL, encoders |
| `reset()` | void | Reset all RestAssured config to defaults | Useful between tests |
| `registerParser(String contentType, Parser parser)` | void | Custom mapping for content-type | e.g. for `text/plain` as JSON |

---

## 2\. `io.restassured.specification.RequestSpecification` (Interface)

**Purpose / How used:**

* Builders for HTTP request: headers, query params, body, cookies, auth
    
* Returned by `given()` / `with()`
    

| Method | Return Type | Use / Shortcut | Notes |
| --- | --- | --- | --- |
| `baseUri(String uri)` | `RequestSpecification` | Set URI for this request | Overrides global baseURI |
| `basePath(String path)` | `RequestSpecification` | Set request base path |  |
| `port(int port)` | `RequestSpecification` | Set request port |  |
| `header(String name, Object value)` | `RequestSpecification` | Add single header |  |
| `headers(Map<String, ?> headers)` | `RequestSpecification` | Add many headers |  |
| `accept(String contentType)` | `RequestSpecification` | Set Accept header |  |
| `contentType(String contentType)` | `RequestSpecification` | Set Content-Type header |  |
| `body(Object body)` | `RequestSpecification` | Set request body | Accepts POJO, String, byte\[\], etc. |
| `param(String name, Object value)` | `RequestSpecification` | Add parameter (query or form) |  |
| `queryParam(String name, Object value)` | `RequestSpecification` | Add query parameter |  |
| `pathParam(String name, Object value)` | `RequestSpecification` | Add path param |  |
| `formParam(String name, Object value)` | `RequestSpecification` | For form data |  |
| `cookie(String name, Object value)` | `RequestSpecification` | Add cookie |  |
| `cookies(Map<String, ?> cookies)` | `RequestSpecification` | Add multiple cookies |  |
| `auth()` | `AuthenticationSpecification` | For auth (basic, digest, oauth) |  |
| `filter(Filter filter)` | `RequestSpecification` | Add filter (e.g. logging) |  |
| `log()` | `RequestSpecification` | Logging DSL | Then `.all()`, `.headers()`, `.body()`, `.ifValidationFails()` |
| `relaxedHTTPSValidation()` | `RequestSpecification` | Ignore SSL certificate issues | Useful in test env |
| `spec(RequestSpecification specification)` | `RequestSpecification` | Apply an existing spec | Reuse prebuilt spec |
| `when()` | `RequestSender` / `RequestSpecification` | Move to sending request stage | Usually next is `.get()`, `.post()`, etc. |

---

## 3\. `io.restassured.specification.ResponseSpecification` (Interface)

**Purpose / How used:**

* Define expected response behaviors that you reuse (status, body, headers)
    
* Used in `.then().spec(...)`
    

| Method | Return Type | Use / Shortcut | Notes |
| --- | --- | --- | --- |
| `expectStatusCode(int code)` | `ResponseSpecification` | Expect HTTP code |  |
| `statusCode(int code)` | `ResponseSpecification` | Alias in newer versions |  |
| `expectContentType(String type)` | `ResponseSpecification` | Expected content-type |  |
| `expectHeader(String name, Matcher<?> matcher)` | `ResponseSpecification` | Validate header |  |
| `expectHeader(String name, String value)` | `ResponseSpecification` | Exact header value |  |
| `expectBody(String path, Matcher<?> matcher)` | `ResponseSpecification` | Validate JSON/xml body |  |
| `body(String path, Matcher<?> matcher)` | `ResponseSpecification` | Alias or newer style |  |
| `log()` | `ResponseSpecification` | Logging DSL (response) | `.all()`, `.body()`, `.headers()` |
| `spec(ResponseSpecification specification)` | `ResponseSpecification` | Combine specs | Chain validations |

---

## 4\. `io.restassured.builder.RequestSpecBuilder`

**Purpose / How used:**

* To build a `RequestSpecification` in a modular / reusable way
    

| Method | Return Type | Use / Shortcut | Notes |
| --- | --- | --- | --- |
| `setBaseUri(String uri)` | `RequestSpecBuilder` | Set base URI |  |
| `setBasePath(String path)` | `RequestSpecBuilder` | Set base path |  |
| `setPort(int port)` | `RequestSpecBuilder` | Set port |  |
| `addHeader(String name, Object value)` | `RequestSpecBuilder` | Add header |  |
| `addQueryParam(String name, Object value)` | `RequestSpecBuilder` | Add query param |  |
| `addPathParam(String name, Object value)` | `RequestSpecBuilder` | Add path param |  |
| `setContentType(ContentType contentType)` | `RequestSpecBuilder` | Set content-type |  |
| `setBody(Object body)` | `RequestSpecBuilder` | Add body |  |
| `addCookie(String name, Object value)` | `RequestSpecBuilder` | Add cookie |  |
| `setAuth(AuthenticationScheme auth)` | `RequestSpecBuilder` | Set auth scheme |  |
| `setConfig(RestAssuredConfig config)` | `RequestSpecBuilder` | Set config for this spec |  |
| `log(LogDetail detail)` | `RequestSpecBuilder` | Log detail |  |
| `build()` | `RequestSpecification` | Create spec instance |  |

---

## 5\. `io.restassured.builder.ResponseSpecBuilder`

**Purpose / How used:**

* Build `ResponseSpecification` in reusable ways
    

| Method | Return Type | Use / Shortcut | Notes |
| --- | --- | --- | --- |
| `expectStatusCode(int code)` | `ResponseSpecBuilder` | Expect HTTP code |  |
| `expectContentType(ContentType type)` | `ResponseSpecBuilder` | Expect content type |  |
| `expectHeader(String name, String value)` | `ResponseSpecBuilder` | Expected header |  |
| `expectHeader(String name, Matcher<?> matcher)` | `ResponseSpecBuilder` | Header matcher |  |
| `expectBody(String path, Matcher<?> matcher)` | `ResponseSpecBuilder` | Body assertion |  |
| `expectResponseTime(Matcher<Long> matcher)` | `ResponseSpecBuilder` | Response time check |  |
| `log(LogDetail detail)` | `ResponseSpecBuilder` | Logging detail for response |  |
| `build()` | `ResponseSpecification` | Create the spec |  |

---

## 6\. `io.restassured.response.Response` (and associated interfaces)

**Purpose / How used:**

* Represents HTTP response
    
* Methods to extract status, headers, body, cookies, JSON/XML paths
    

| Method | Return Type | Use / Shortcut | Notes |
| --- | --- | --- | --- |
| `getStatusCode()` | `int` | HTTP status code |  |
| `getStatusLine()` | `String` | HTTP status line |  |
| `getBody()` | `ResponseBody` | Response body object |  |
| `asString()` | `String` | Body as string | Equivalent to `getBody().asString()` |
| `getHeader(String name)` | `String` | Single header |  |
| `getHeaders()` | `Headers` | All headers |  |
| `getCookie(String name)` | `String` | Cookie value |  |
| `getCookies()` | `Map<String, String>` | All cookies |  |
| `jsonPath()` | `JsonPath` | JSON path parser |  |
| `xmlPath()` | `XmlPath` | XML path parser |  |
| `time()` | `long` | Response time in ms |  |
| `then()` | `ValidatableResponse` | Move to validation | Use `.then().statusCode(...)` etc. |
| `peek()` | `Response` | Print response to console, return response |  |
| `prettyPrint()` | `String` | Print formatted body |  |
| `as(Class<T> cls)` | `<T>` | Deserialize body into POJO |  |
| `path(String path)` | generics | Extract value via json/xml path |  |

---

## 7\. `io.restassured.response.ValidatableResponse` / `ValidatableResponseOptions`

**Purpose / How used:**

* Returned by `.then()` or `.expect()`
    
* Used to validate response with matchers
    

| Method | Return Type | Use / Shortcut | Notes |
| --- | --- | --- | --- |
| `statusCode(int code)` | `ValidatableResponse` | Validate HTTP status code |  |
| `body(String path, Matcher<?> matcher)` | `ValidatableResponse` | Validate response body |  |
| `header(String name, Matcher<?> matcher)` | `ValidatableResponse` | Validate header |  |
| `contentType(ContentType type)` | `ValidatableResponse` | Validate content type |  |
| `spec(ResponseSpecification spec)` | `ValidatableResponse` | Apply a spec |  |
| `time(Matcher<Long> matcher)` | `ValidatableResponse` | Validate response time |  |
| `log().all()` / `log().body()` / `log().headers()` | `ValidatableResponse` | Logging methods in validation stage |  |

---

## 8\. `io.restassured.specification.AuthenticationSpecification`

**Purpose / How used:**

* For specifying authentication (basic, digest, OAuth) in request building
    

| Method | Return Type | Use / Shortcut | Notes |
| --- | --- | --- | --- |
| `basic(String username, String password)` | `RequestSpecification` | Use Basic authentication |  |
| `digest(String username, String password)` | `RequestSpecification` | Digest auth |  |
| `preemptive()` | `PreemptiveAuthSpec` | For preemptive auth | Used before `.basic()` or `.oauth2()` |
| `oauth2(String token)` | `RequestSpecification` | Use OAuth2 token |  |
| `none()` | `RequestSpecification` | No auth |  |

---

## 9\. Logging & Filter-related classes (partial)

**Purpose / How used:**

* For debugging / intercepting requests & responses
    

| Class / Interface | Methods / Use | Shortcut / Typical Use |
| --- | --- | --- |
| `Filter` | `Response filter(FilterableRequestSpecification, FilterableResponseSpecification, FilterContext)` | Add to request spec, used to log or modify requests/responses |
| `RequestLoggingFilter` | Uses Filter interface | `given().filter(new RequestLoggingFilter())` |
| `ResponseLoggingFilter` | Logs response | `given().filter(new ResponseLoggingFilter())` |
| `SessionFilter` | Captures session cookies | `SessionFilter session = new SessionFilter(); given().filter(session)...` |
| `SpecificationQuerier` | `query(RequestSpecification)` & `query(ResponseSpecification)` | Inspect spec internals |

---

# 🧩 REST ASSURED – MISCELLANEOUS & SUPPORT CLASSES

## 🔹 10. `io.restassured.path.json.JsonPath`

**Purpose / How:** Extract values from JSON responses using path expressions (like XPath for JSON).

| Method | Return Type | Description / Use |
| --- | --- | --- |
| `get(String path)` | `Object` | Get value using JSON path |
| `getInt(String path)` | `int` | Extract integer value |
| `getString(String path)` | `String` | Extract string value |
| `getList(String path)` | `List<?>` | Extract list |
| `getMap(String path)` | `Map<?,?>` | Extract map |
| `setRoot(String path)` | `JsonPath` | Change root element |
| `prettify()` | `String` | Pretty print JSON |
| `from(String json)` | `JsonPath` | Static: create JsonPath from String |
| `getBoolean(String path)` | `boolean` | Extract boolean |
| `getDouble(String path)` | `double` | Extract double |
| `param(String key, Object value)` | `JsonPath` | Add parameter in path expression |

✅ Example:

```java
String name = response.jsonPath().getString("data[0].employee_name");
```

---

## 🔹 11. `io.restassured.path.xml.XmlPath`

**Purpose / How:** Extract values from XML responses.

| Method | Return Type | Description |
| --- | --- | --- |
| `get(String path)` | `Object` | Get value from XML |
| `getString(String path)` | `String` | Extract text |
| `getList(String path)` | `List<?>` | Extract list |
| `getMap(String path)` | `Map<?,?>` | Extract map |
| `from(String xml)` | `XmlPath` | Create from string |
| `setRoot(String path)` | `XmlPath` | Set XML root path |

✅ Example:

```java
XmlPath xml = new XmlPath(response.asString());
String city = xml.getString("Response.City");
```

---

## 🔹 12. `io.restassured.config.RestAssuredConfig`

**Purpose / How:** Central configuration for RestAssured.

| Method | Return Type | Description / Use |
| --- | --- | --- |
| `newConfig()` | `RestAssuredConfig` | Create new config |
| `encoderConfig(EncoderConfig config)` | `RestAssuredConfig` | Configure encoding |
| `decoderConfig(DecoderConfig config)` | `RestAssuredConfig` | Configure decoding |
| `logConfig(LogConfig config)` | `RestAssuredConfig` | Control logging |
| `sessionConfig(SessionConfig config)` | `RestAssuredConfig` | Manage sessions |
| `sslConfig(SSLConfig config)` | `RestAssuredConfig` | Manage SSL certificates |
| `httpClientConfig(HttpClientConfig config)` | `RestAssuredConfig` | Configure Apache HTTPClient options |
| `redirectConfig(RedirectConfig config)` | `RestAssuredConfig` | Manage redirect behavior |

✅ Example:

```java
RestAssured.config = RestAssuredConfig.newConfig()
     .sslConfig(new SSLConfig().relaxedHTTPSValidation())
     .logConfig(new LogConfig().enableLoggingOfRequestAndResponseIfValidationFails());
```

---

## 🔹 13. `io.restassured.http.ContentType`

**Purpose / How:** Enum for supported content types.

| Constant | Meaning |
| --- | --- |
| `ContentType.JSON` | `application/json` |
| `ContentType.XML` | `application/xml` |
| `ContentType.TEXT` | `text/plain` |
| `ContentType.HTML` | `text/html` |
| `ContentType.URLENC` | `application/x-www-form-urlencoded` |
| `ContentType.BINARY` | `application/octet-stream` |
| `ContentType.ANY` | `*/*` |

✅ Example:

```java
given().contentType(ContentType.JSON)
```

---

## 🔹 14. `io.restassured.parsing.Parser`

**Purpose / How:** Defines how to parse response based on content type.

| Constant | Description |
| --- | --- |
| `Parser.JSON` | Parse as JSON |
| `Parser.XML` | Parse as XML |
| `Parser.HTML` | Parse as HTML |
| `Parser.TEXT` | Parse as plain text |
| `Parser.NONE` | No parsing |

✅ Example:

```java
RestAssured.registerParser("text/plain", Parser.JSON);
```

---

## 🔹 15. `io.restassured.authentication.*`

### 🔸 Common Classes:

| Class / Interface | Purpose / Description |
| --- | --- |
| `AuthenticationScheme` | Parent interface for all authentication schemes |
| `FormAuthScheme` | Handles form-based authentication |
| `BasicAuthScheme` | For HTTP Basic Auth |
| `OAuth2Scheme` | For OAuth 2.0 token auth |
| `PreemptiveAuthSpec` | For sending auth header before server challenge |

✅ Example:

```java
given().auth().preemptive().basic("user", "pass");
```

---

## 🔹 16. `io.restassured.filter.Filter` & Related

**Purpose / How:**

* Intercept requests/responses like middleware.
    

| Filter Class | Description |
| --- | --- |
| `RequestLoggingFilter` | Logs all request details |
| `ResponseLoggingFilter` | Logs all response details |
| `ErrorLoggingFilter` | Logs only when validation fails |
| `FilterContext` | Holds context for filters |
| `SessionFilter` | Captures session for login reuse |
| `TimeFilter` | Measures request/response time |

✅ Example:

```java
given()
  .filter(new RequestLoggingFilter())
  .filter(new ResponseLoggingFilter())
  .when()
  .get("/friends");
```

---

## 🔹 17. `io.restassured.module.jsv.JsonSchemaValidator`

**Purpose / How:** Validate JSON body against schema.

| Method | Return Type | Description |
| --- | --- | --- |
| `matchesJsonSchema(File schemaFile)` | Matcher&lt;?&gt; | Validate JSON schema |
| `matchesJsonSchemaInClasspath(String path)` | Matcher&lt;?&gt; | Validate schema from resources |

✅ Example:

```java
.then().body(matchesJsonSchemaInClasspath("friend_schema.json"));
```

---

## 🔹 18. `io.restassured.internal.ValidatableResponseImpl`

**Purpose:**  
Internal implementation of `ValidatableResponse`.  
Automation testers rarely use directly, but good to know it powers `.then()` validations.

---

## 🔹 19. `io.restassured.matcher.RestAssuredMatchers`

**Purpose / How:**  
Extra matchers for XML / time / status validations.

| Method | Matcher Type | Description |
| --- | --- | --- |
| `matchesXsd(File xsdFile)` | XML | Validate XML schema |
| `matchesXsdInClasspath(String path)` | XML | Validate schema from resources |
| `hasXPath(String expression)` | XML | Validate XML with XPath |
| `hasXPath(String expression, Matcher<?> matcher)` | XML | Validate XML node value |
| `hasStatusCode(int code)` | HTTP | Check status code |
| `hasResponseTime(Matcher<Long> matcher)` | Performance | Validate response time |

✅ Example:

```java
.then().body(RestAssuredMatchers.hasXPath("/friends/name", equalTo("Nini")));
```

---

## 🔹 20. `io.restassured.common.mapper.TypeRef<T>`

**Purpose / How:** Helps deserialize complex JSON objects into generic types like `List<Map<String,Object>>`.

✅ Example:

```java
List<Map<String, Object>> friends =
    response.as(new TypeRef<List<Map<String, Object>>>() {});
```

---

## 🔹 21. `io.restassured.path.json.config.JsonPathConfig`

| Method | Purpose |
| --- | --- |
| `defaultParserType(JsonPathConfig.NumberReturnType type)` | Control numeric parsing |
| `charset(String charset)` | Define charset for JSON |
| `defaultDeserializer(ObjectMapperDeserializer deserializer)` | Set default deserializer |

---

## 🔹 22. `io.restassured.path.xml.config.XmlPathConfig`

| Method | Purpose |
| --- | --- |
| `namespaceAware(boolean aware)` | Handle namespaces |
| `declareNamespace(String prefix, String uri)` | Map prefix for XPath |
| `charset(String charset)` | Set charset |

---

## 🔹 23. `io.restassured.internal.mapping.ObjectMapperType`

**Purpose:** Defines which object mapper to use.

| Enum | Description |
| --- | --- |
| `GSON` | Use Gson for JSON |
| `JACKSON_1` | Old Jackson |
| `JACKSON_2` | Modern Jackson |
| `JAXB` | For XML |

✅ Example:

```java
RestAssured.config = RestAssured.config()
     .objectMapperConfig(objectMapperConfig().defaultObjectMapperType(ObjectMapperType.JACKSON_2));
```

---

## 🔹 24. `io.restassured.module.mockmvc.RestAssuredMockMvc`

**Purpose / How:**  
For **testing Spring REST controllers** without starting a full server.

✅ Example:

```java
given()
  .standaloneSetup(new FriendController())
.when()
  .get("/friend/1")
.then()
  .statusCode(200);
```

---

# ✅ Summary – What You Now Have

You now have a **complete master RestAssured API reference** for automation testers:

* ✅ All core classes & interfaces
    
* ✅ All builder classes (specs)
    
* ✅ All filters, matchers, parsers, and configs
    
* ✅ JSON/XML path & schema validation utilities
    
* ✅ Plus extras (MockMVC, TypeRef, ObjectMapper)