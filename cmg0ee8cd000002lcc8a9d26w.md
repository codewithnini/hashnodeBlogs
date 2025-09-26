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
    
    ## **1\. XPath Node Types**
    
    | **Node Type** | **Description** | **Example** |
    | --- | --- | --- |
    | Root | Top of XML/HTML | `/` |
    | Element | HTML/XML element | `//div` |
    | Attribute | Element attributes | `//@id` |
    | Text | Inner text of element | `//div/text()` |
    | Namespace | Namespace in XML | `namespace::*` |
    
    ---
    
    ## **2\. XPath Operators**
    
    ### **Arithmetic**
    
    | **Operator** | **Description** |
    | --- | --- |
    | `+` | Addition |
    | `-` | Subtraction |
    | `*` | Multiplication |
    | `div` | Division |
    | `mod` | Modulus |
    
    ### **Comparison**
    
    | **Operator** | **Description** |
    | --- | --- |
    | `=` | Equals |
    | `!=` | Not equals |
    | `<` | Less than |
    | `>` | Greater than |
    | `<=` | Less or equal |
    | `>=` | Greater or equal |
    
    ### **Logical**
    
    | **Operator** | **Description** |
    | --- | --- |
    | `and` | Both conditions true |
    | `or` | Either condition true |
    
    ---
    
    ## **3\. XPath 1.0 Functions**
    
    ### **String Functions**
    
    | **Function** | **Description** | **Example** |
    | --- | --- | --- |
    | `contains(string, substring)` | Checks substring | `//input[contains(@id,'user')]` |
    | `starts-with(string, prefix)` | Checks start of string | `//a[starts-with(@href,'https')]` |
    | `string-length(string)` | Length of string | `string-length(//input/@value)` |
    | `normalize-space(string)` | Trim & normalize spaces | `normalize-space(//div[@id='desc'])` |
    | `substring(string,start,length)` | Substring | `substring('HelloWorld',1,5)` → `Hello` |
    | `substring-before(string,substr)` | Text before substring | `substring-before('`[`user@example.com`](mailto:user@example.com)`','@')` → `user` |
    | `substring-after(string,substr)` | Text after substring | `substring-after('`[`user@example.com`](mailto:user@example.com)`','@')` → [`example.com`](http://example.com/) |
    | `concat(string1,string2,...)` | Join strings | `concat('Hello',' ','World')` → `Hello World` |
    | `translate(string,chars1,chars2)` | Replace characters | `translate('abc','a','x')` → `xbc` |
    | `string(object)` | Convert object to string | `string(//div[@class='title'])` |
    
    ### **Numeric Functions**
    
    | **Function** | **Description** | **Example** |
    | --- | --- | --- |
    | `number(string)` | Convert string to number | `number('123')` → 123 |
    | `sum(node-set)` | Sum node values | `sum(//price)` |
    | `floor(number)` | Round down | `floor(3.7)` → 3 |
    | `ceiling(number)` | Round up | `ceiling(3.2)` → 4 |
    | `round(number)` | Round nearest | `round(3.5)` → 4 |
    
    ### **Boolean Functions**
    
    | **Function** | **Description** | **Example** |
    | --- | --- | --- |
    | `boolean(object)` | Convert to boolean | `boolean(//div[@id='desc'])` |
    | `not(expression)` | Negates boolean | `not(@disabled)` |
    | `true()` | Returns true | `//input[@enabled=true()]` |
    | `false()` | Returns false | `//input[@checked=false()]` |
    
    ### **Node Functions**
    
    | **Function** | **Description** | **Example** |
    | --- | --- | --- |
    | `last()` | Last node | `//li[last()]` |
    | `position()` | Current node | `//li[position()=2]` |
    | `count(node-set)` | Number of nodes | `count(//div)` |
    | `name(node)` | Node name | `name(//div)` → `div` |
    | `local-name(node)` | Local name without namespace | `local-name(//ns:div)` → `div` |
    
    ---
    
    ## **4\. XPath 1.0 Axes**
    
    | **Axis** | **Description** | **Example** |
    | --- | --- | --- |
    | `child` | Direct children | `//div/child::p` |
    | `parent` | Parent node | `//span/parent::div` |
    | `ancestor` | All ancestors | `//span/ancestor::div` |
    | `descendant` | All descendants | `//div/descendant::p` |
    | `following-sibling` | Siblings after current | `//h2/following-sibling::p` |
    | `preceding-sibling` | Siblings before current | `//h2/preceding-sibling::p` |
    | `self` | Current node | `//div/self::div` |
    | `descendant-or-self` | Self + descendants | `//div/descendant-or-self::span` |
    | `ancestor-or-self` | Self + ancestors | `//span/ancestor-or-self::div` |
    
    ---
    
    ## **5\. XPath 1.0 Predicates**
    
    * Predicates are **conditions in** `[ ]` to filter nodes.
        
    
    **Examples:**
    
    ```sql
    //input[@type='text']                   // All text inputs
    //li[position()=1]                      // First <li> element
    //li[last()]                            // Last <li> element
    //div[contains(text(),'Login')]         // Div with "Login" text
    //a[starts-with(@href,'https')]         // Links starting with https
    //tr[td='Admin']                        // Table row where td='Admin'
    ```
    
    ---
    
    ## **6\. Combining Functions and Axes (Examples)**
    
    1. **Find last element containing text**:
        
    
    ```sql
    (//li[contains(text(),'Option')])[last()]
    ```
    
    2. **Select second input inside a form**:
        
    
    ```sql
    //form/input[position()=2]
    ```
    
    3. **Parent of an element containing specific text**:
        
    
    ```sql
    //span[contains(text(),'Username')]/parent::div
    ```
    
    4. **Normalize spaces and compare text**:
        
    
    ```sql
    //div[normalize-space(text())='Login']
    ```
    
    ---
    
    ### **✅ Key Notes**
    
    * XPath 1.0 is **widely used in Selenium**.
        
    * **Does not support** ends-with(), date functions, or regex (XPath 2.0 only).
        
    * Combine **axes + predicates + functions** to locate complex elements.
        
    * Use **normalize-space()**, `contains()`, `starts-with()` for dynamic XPath.