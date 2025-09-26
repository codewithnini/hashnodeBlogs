---
title: "XPath for Automation Tester"
datePublished: Fri Sep 26 2025 05:25:06 GMT+0000 (Coordinated Universal Time)
cuid: cmg0ee8cd000002lcc8a9d26w
slug: xpath-for-automation-tester
tags: codewithnini

---

## **What is XPath?**

**XPath (XML Path Language)** is a query language used to navigate and select nodes in an XML or HTML document.  
In Selenium, XPath is widely used to locate elements when `id`, `name`, or `class` attributes are dynamic or missing.

**Why XPath?**

* Can locate elements anywhere in the DOM.
    
* Works when other locators fail.
    
* Supports complex conditions.
    

---

## **2\. Types of XPath**

### **A. Absolute XPath**

* Starts from the root of the HTML (`/html`) and follows the full path.
    
* **Syntax:**
    
    ```sql
    /html/body/div[1]/div[2]/input
    ```
    
* **Pros:** Exact path.
    
* **Cons:** Fragile; changes in DOM break it.
    

### **B. Relative XPath**

* Starts from anywhere in the DOM using `//`.
    
* **Syntax:**
    
    ```sql
    //tagname[@attribute='value']
    ```
    
* **Example:**
    
    ```sql
    //input[@id='username']
    ```