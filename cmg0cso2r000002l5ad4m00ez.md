---
title: "API Status Code"
datePublished: Fri Sep 26 2025 04:40:20 GMT+0000 (Coordinated Universal Time)
cuid: cmg0cso2r000002l5ad4m00ez
slug: api-status-code
tags: codewithnini

---

## 🔹 What is a Status Code?

A **status code** is a **3-digit number** sent by the server in response to a client’s request (like from a browser, Postman, or an API client).

It tells the **outcome of the request** — whether it was successful, failed, redirected, or had some error.

Example:

* `200 OK` → Request worked fine.
    
* `404 Not Found` → The resource doesn’t exist.
    
* `500 Internal Server Error` → Something went wrong on the server.
    

---

## 🔹 Why is it Necessary?

Status codes are **necessary for communication** between client and server because they:

1. **Indicate Success or Failure**
    
    * Without codes, the client wouldn’t know if the request worked.
        
    * Example: `200 OK` means "everything fine," `401 Unauthorized` means "you need to log in."
        
2. **Help in Debugging**
    
    * Developers quickly identify where the issue is — client-side or server-side.
        
    * Example: `400 Bad Request` → issue with client request, `500` → server problem.
        
3. **Enable Automation & Testing**
    
    * In **API automation testing**, we use assertions like:
        
        ```sql
        response.getStatusCode() == 200
        ```
        
        to check if API works as expected.
        
4. **Improve User Experience**
    
    * Users see meaningful error messages (like “Page Not Found” for `404`).
        
    * Prevents confusion if a request fails silently.
        
5. **Support REST Principles**
    
    * REST APIs rely on status codes to follow standard communication patterns.
        
    * Example:
        
        * `201 Created` → when new resource is created.
            
        * `204 No Content` → when resource deleted successfully.
            

---

## 🔹 Analogy

Think of **status codes like traffic signals** 🚦:

* Green light (2xx) → Go ahead (success).
    
* Yellow light (3xx) → Redirect or wait (redirection).
    
* Red light (4xx, 5xx) → Stop, something’s wrong (error).
    

HTTP status codes are grouped into 5 categories:

* **1xx** → Informational
    
* **2xx** → Success
    
* **3xx** → Redirection
    
* **4xx** → Client Errors
    
* **5xx** → Server Errors
    

---

# 📘 HTTP Status Codes with Use Cases

---

## 🔹 1xx – Informational

These indicate that the request was received and is continuing to be processed.

| Code | Meaning | Example | Example Use Case |
| --- | --- | --- | --- |
| 100 | Continue | Uploading large file | Client uploads video in chunks, server says “continue”. |
| 101 | Switching Protocols | Upgrade to WebSocket | Switching from HTTP to WebSocket chat connection. |
| 102 | Processing | Long request processing | WebDAV: server is processing multiple file operations. |
| 103 | Early Hints | Preload resources | Browser preloads CSS/JS before final page load. |

---

## 🔹 2xx – Success

Request was successfully received, understood, and accepted.

| Code | Meaning | Example | Example Use Case |
| --- | --- | --- | --- |
| 200 | OK | Request successful | GET user profile → returns JSON with user data. |
| 201 | Created | Resource created | POST new user → server creates and returns user ID. |
| 202 | Accepted | Request accepted for processing | Upload request accepted, processed in background. |
| 203 | Non-Authoritative Info | Proxy response | Response returned by proxy with modified headers. |
| 204 | No Content | No response body | DELETE /users/10 → successful but no body returned. |
| 205 | Reset Content | Reset form | After submitting form, client resets form fields. |
| 206 | Partial Content | Range response | Video streaming resumes from 2 minutes. |
| 207 | Multi-Status | Multiple statuses | WebDAV: batch operation, some success, some failed. |
| 208 | Already Reported | Avoid repetition | WebDAV multistatus avoids duplicate entry. |
| 226 | IM Used | Delta encoding | Server sends only updated parts of file instead of full file. |

---

## 🔹 3xx – Redirection

Client must take additional action to complete the request.

| Code | Meaning | Example | Example Use Case |
| --- | --- | --- | --- |
| 300 | Multiple Choices | Several formats | File available in PDF, DOC, HTML. |
| 301 | Moved Permanently | URL changed | Old blog URL redirects to new URL permanently. |
| 302 | Found | Temporary redirect | Login → redirected to dashboard temporarily. |
| 303 | See Other | Redirect with GET | After payment POST → redirect to confirmation page. |
| 304 | Not Modified | Cached resource | Browser uses cached image instead of downloading. |
| 305 | Use Proxy | Must use proxy | API request restricted to specific proxy. |
| 306 | (Unused) | Reserved | No longer used. |
| 307 | Temporary Redirect | Method unchanged | POST request temporarily redirected to another endpoint. |
| 308 | Permanent Redirect | Method unchanged | API moved permanently, requests redirected. |

---

## 🔹 4xx – Client Errors

The request has issues caused by the client.

| Code | Meaning | Example | Example Use Case |
| --- | --- | --- | --- |
| 400 | Bad Request | Invalid JSON | Client sends malformed JSON in request. |
| 401 | Unauthorized | Missing token | User not logged in but requests profile. |
| 402 | Payment Required | Payment API | Premium API requires payment before use. |
| 403 | Forbidden | Access denied | User tries to access admin-only endpoint. |
| 404 | Not Found | Resource missing | GET /user/999 → no such user exists. |
| 405 | Method Not Allowed | Wrong method | Sending PUT when only GET is supported. |
| 406 | Not Acceptable | Format mismatch | Client requests XML, server supports only JSON. |
| 407 | Proxy Auth Required | Proxy login | Client behind corporate proxy needs credentials. |
| 408 | Request Timeout | Request delay | Client took too long to send request data. |
| 409 | Conflict | Data conflict | Registering with already-used email ID. |
| 410 | Gone | Resource removed | Old API version permanently removed. |
| 411 | Length Required | Missing header | Upload file without Content-Length header. |
| 412 | Precondition Failed | ETag mismatch | Update rejected due to outdated version. |
| 413 | Payload Too Large | Large request | Upload exceeds API file size limit. |
| 414 | URI Too Long | Large URL | Query string exceeds server’s limit. |
| 415 | Unsupported Media Type | Wrong format | API only accepts JSON but got XML. |
| 416 | Range Not Satisfiable | Wrong byte range | Client requests video chunk that doesn’t exist. |
| 417 | Expectation Failed | Expect header issue | Server cannot process "Expect: 100-continue". |
| 418 | I’m a Teapot | Joke code | Easter egg, not used in production APIs. |
| 421 | Misdirected Request | Wrong server | Request sent to incorrect server in HTTP/2. |
| 422 | Unprocessable Entity | Validation error | API gets JSON with invalid email field. |
| 423 | Locked | Locked resource | File locked, cannot update. |
| 424 | Failed Dependency | Dependent failed | Multi-request operation failed due to one dependency. |
| 425 | Too Early | Replay risk | Request sent too early with TLS. |
| 426 | Upgrade Required | Needs HTTPS | Client must switch from HTTP to HTTPS. |
| 428 | Precondition Required | Header required | PUT request requires If-Match header. |
| 429 | Too Many Requests | Rate limited | User exceeded API call limit (e.g., 100/min). |
| 431 | Request Header Too Large | Large headers | Request contains too many cookies or headers. |
| 451 | Unavailable For Legal Reasons | Blocked | Page blocked due to GDPR/DMCA restrictions. |

---

## 🔹 5xx – Server Errors

The request was valid, but the server failed to fulfill it.

| Code | Meaning | Example | Example Use Case |
| --- | --- | --- | --- |
| 500 | Internal Server Error | Generic error | API crashes due to null pointer. |
| 501 | Not Implemented | Not supported | PATCH method not implemented by server. |
| 502 | Bad Gateway | Invalid upstream response | Gateway gets error from microservice. |
| 503 | Service Unavailable | Server down | API under maintenance or overloaded. |
| 504 | Gateway Timeout | Timeout | Upstream microservice took too long to respond. |
| 505 | HTTP Version Not Supported | Old protocol | Server rejects outdated HTTP/1.0 request. |
| 506 | Variant Also Negotiates | Negotiation error | Error during content negotiation. |
| 507 | Insufficient Storage | No space left | WebDAV server out of storage capacity. |
| 508 | Loop Detected | Infinite loop | Cyclic dependency in request detected. |
| 510 | Not Extended | Extra info required | Server needs additional request parameters. |
| 511 | Network Authentication Required | Captive portal | Wi-Fi requires login before access. |