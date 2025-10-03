---
title: "XPath for Automation Tester"
datePublished: Fri Sep 26 2025 05:25:06 GMT+0000 (Coordinated Universal Time)
cuid: cmg0ee8cd000002lcc8a9d26w
slug: xpath-for-automation-tester
tags: codewithnini

---

## Link for Xpath PlayGround below

[Click on Xpath Playground Link](https://xpath-by-nini.netlify.app/)

## **1\. Introduction**

## **What is XPath?**

**XPath (XML Path Language)** is a query language used to navigate and select nodes in an XML or HTML document.  
In Selenium, XPath is widely used to locate elements when `id`, `name`, or `class` attributes are dynamic or missing.

**Why XPath?**

* Can locate elements anywhere in the DOM.
    
* Works when other locators fail.
    
* Supports complex conditions.
    

In automation, XPath is often used when:

* No **unique ID, name, or CSS selector** is available.
    
* You need to locate **dynamic elements**.
    
* You want to traverse **parent/child/sibling** relationships.
    

---

* ## 🔹 Limitations of XPath 1.0
    
    * No advanced string functions like `matches()` (available in XPath 2.0).
        
    * Cannot directly use **regular expressions**.
        
    * Limited numeric and date handling.
        
    
    ### **✅ Key Notes**
    
    * XPath 1.0 is **widely used in Selenium**.
        
    * **Does not support** ends-with(), date functions, or regex (XPath 2.0 only).
        
    * Combine **axes + predicates + functions** to locate complex elements.
        
    * Use **normalize-space()**, `contains()`, `starts-with()` for dynamic XPath.
        
    
    ### **History and Versions**
    
    | Version | Year | Key Features | Notes |
    | --- | --- | --- | --- |
    | XPath 1.0 | 1999 | Basic node selection, axes, string/boolean/numeric functions | Supported in browsers & Selenium/Playwright |
    | XPath 2.0 | 2007 | Sequences, regex, FLWOR expressions | Not supported in browsers/automation |
    | XPath 3.0 | 2014 | Higher-order functions, conditional expressions | Not supported in browsers/automation |
    | XPath 3.1 | 2017 | JSON support, arrays, maps | Only XML/XQuery processors |
    
    ### **Importance in Automation**
    
    * Used in **Selenium, Playwright, Cypress** for **robust locators**.
        
    * Can handle **dynamic IDs, classes, and complex hierarchies**.
        
    * Essential for **table data extraction and nested elements**.
        
    
    ---
    
    ## **2\. XPath Basics**
    
    ### **Syntax and Rules**
    
    # 📘 **XPath Syntax & Rules – Detailed Table**
    
    | **Concept** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | **Basic Syntax** | XPath uses `/`, `//`, `@`, `[]`, `()`, `*`, `text()`, `node()`, and functions to navigate XML/HTML | `//div[@id='main']/ul/li[2]/a` | Combines node selection, attributes, and predicates |
    | **Case Sensitivity** | XPath is **case-sensitive** | `//div` ≠ `//Div` | Always use correct tag and attribute case in HTML |
    | **Quotes in Strings** | Use single `' '` or double `" "` quotes | `//input[@type='text']` or `//input[@type="text"]` | If string contains single quotes, wrap with double quotes |
    | **Use of** `/` | Single `/` selects from **root** | `/html/body/div` | Absolute path; rarely used in dynamic automation |
    | **Use of** `//` | Double `//` selects **anywhere** in DOM | `//div[@class='container']` | Preferred in automation; finds node regardless of depth |
    | **Predicates** `[]` | Used to filter nodes by position, attribute, or text | `//ul/li[1]`, `//input[@id='username']` | Can combine multiple predicates for robust locators |
    | **Wildcard** `*` | Matches any element | `//div/*` | Useful when tag names are unknown or dynamic |
    | **Attribute Selection** `@` | Selects attribute of an element | `//input[@type='text']` | Most common method for locating elements in automation |
    | **Text Selection** | `text()` selects **text node** | `//button[text()='Submit']` | Useful for verifying button, label, or link text |
    | **Node Selection** | `node()` selects **any type of node** | `//div/node()` | Can select element, text, comment, etc. |
    | **Function Usage** | XPath functions can be used in predicates | `//a[contains(@href,'login')]` | Functions make locators **dynamic and robust** |
    
    ---
    
    ### **Automation Tips**
    
    1. Always **start with** `//` for relative XPath to make scripts more reliable.
        
    2. Combine **attributes, text, and functions** to handle dynamic elements.
        
    3. Use **wildcards (**`*`, `@*`) and `node()` when DOM structure is complex or dynamic.
        
    4. **Test all XPath in browser DevTools** before using in Selenium/Playwright.
        
    5. Remember **XPath is case-sensitive**; HTML tag names and attributes must match exactly.
        
    
    ### **Absolute vs Relative XPath**
    
    # 📘 **XPath – Absolute vs Relative – Detailed Table**
    
    | **Type** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | **Absolute XPath** | Starts from the **root node** `/` and follows the full path to the element | `/html/body/div[2]/div[1]/ul/li[3]/a` | Fragile for automation; breaks if page structure changes |
    | **Relative XPath** | Starts from **anywhere in the document** `//` | `//div[@id='main']/ul/li[3]/a` | Preferred in automation; more robust for dynamic pages |
    | **Advantages of Absolute XPath** | Precise path from root | `/html/body/div[1]` | Useful for **quick testing or learning DOM hierarchy** |
    | **Disadvantages of Absolute XPath** | Very brittle; depends on exact DOM structure | `/html/body/div[2]/div[1]/ul/li[3]/a` | Not recommended for dynamic websites or production automation |
    | **Advantages of Relative XPath** | Flexible and reliable | `//button[text()='Submit']` | Works even if DOM structure changes, as long as attributes or text remain the same |
    | **Disadvantages of Relative XPath** | Slightly slower in very large DOMs | `//div[@class='container']//input[@type='text']` | Usually negligible; modern browsers handle it efficiently |
    
    ---
    
    ### **Automation Tips**
    
    1. **Prefer relative XPath** (`//`) over absolute (`/`) in Selenium/Playwright.
        
    2. **Use attributes, text, or functions** to make relative XPath **robust and dynamic**:
        
    
    ```bash
    //button[contains(@class,'submit')]
    //input[@type='text' and @name='username']
    ```
    
    3. **Absolute XPath** is useful for **learning DOM structure** or quickly locating elements in static pages.
        
    4. Always **test XPath in DevTools** before using in automation scripts.
        
    
    ### **Selecting Nodes**
    
    # 📘 **XPath – Selecting Nodes – Detailed Table**
    
    | **Selection Method** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | **Absolute Path** | Starts from the root node `/` | `/html/body/div` | Rarely used in automation; fragile if page structure changes |
    | **Relative Path** | Starts from anywhere in the document `//` | `//div[@id='main']` | Preferred in automation; more robust for dynamic pages |
    | **Current Node** | Refers to the current context node `.` | `.` | Useful inside predicates or axes for relative selection |
    | **Select All Elements** | Wildcard `*` matches any element | `//div/*` | Selects all child elements of a parent node |
    | **Select Any Attribute** | `@*` matches all attributes of a node | `//input/@*` | Useful when attribute names are dynamic or unknown |
    | **Select Any Node** | `node()` matches any node type | `//div/node()` | Selects all child nodes including elements, text, and comments |
    | **Select by Tag Name** | Matches specific element tags | `//p` | Commonly used to select headings, paragraphs, table rows, etc. |
    | **Select by Attribute** | Matches nodes with specific attributes | `//input[@id='username']` | Most common method in automation |
    | **Select by Text** | Matches nodes by exact text | `//button[text()='Submit']` | Useful for buttons, links, and labels |
    | **Select by Partial Text** | Matches nodes containing text | `//a[contains(text(),'Login')]` | Handles dynamic text or partial matches |
    
    ---
    
    ### **Automation Tips**
    
    1. **Relative XPath (**`//`) is preferred over absolute (`/`) for robust automation locators.
        
    2. **Attribute-based selection** is the most reliable method to locate elements.
        
    3. **Text-based selection** is useful for buttons, labels, and dynamic UI text.
        
    4. **Wildcards (**`*`, `@*`, `node()`) make locators flexible when tags or attributes are dynamic.
        
    5. Always **test XPath expressions** in browser DevTools before using them in Selenium/Playwright.
        
    
    ### **Wildcards**
    
    # 📘 **XPath Wildcards – Detailed Table**
    
    | **Wildcard** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | `*` | Matches **any element node** | `//div/*` → selects all child elements of `<div>` | Useful when the exact tag is unknown or dynamic |
    | `@*` | Matches **any attribute** of an element | `//input/@*` → selects all attributes of `<input>` | Helps when attribute names are dynamic or unknown |
    | `node()` | Matches **any type of node** (element, text, comment, etc.) | `//div/node()` → selects all child nodes of `<div>` | Useful to iterate over all children regardless of type |
    
    ---
    
    ### **Automation Tips**
    
    1. `*` is commonly used in **dynamic locators** when element tag may change:
        
    
    ```
    //*[@class='btn-primary']  // matches any element with class 'btn-primary'
    ```
    
    2. `@*` is useful when **any attribute** might be required for validation or extraction:
        
    
    ```bash
    //input[@*]  // selects input elements with any attribute
    ```
    
    3. `node()` can be combined with **predicates** to process all child nodes:
        
    
    ```bash
    //div[node()[position()=1]]  // first child node of div
    ```
    
    4. Wildcards help make **XPath locators robust** for **dynamic web pages**.
        
    
    ---
    
    ## **3\. XPath Node Types**
    
    # 📘 **XPath Node Types – Detailed Table**
    
    | **Node Type** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | **Element Node** | Represents HTML/XML elements | `<div>` → `//div` | Most commonly used in automation; select by tag, class, or ID |
    | **Attribute Node** | Represents element attributes | `@id` → `//input/@id` | Essential for locating elements by ID, class, name, type, etc. |
    | **Text Node** | Represents text content inside elements | `<p>Hello</p>` → `//p/text()` | Use to verify text or extract values in tables, labels, buttons |
    | **Comment Node** | Represents comments in HTML/XML | `<!-- Comment -->` → `//comment()` | Rarely used in automation, mostly for debugging |
    | **Root Node** | Top-level node of the document | `/` or `/html` | Absolute XPath starts from root; used to select the whole document |
    | **Namespace Node** | Represents XML namespace declarations | `xmlns:ns="..."` | Important in XML; rarely used in HTML automation |
    | **Processing Instruction Node** | Represents XML processing instructions | `<?xml-stylesheet ... ?>` | Used in XML; not common in UI automation |
    
    ---
    
    ### **Automation Tips**
    
    1. **Element nodes** are the primary target in Selenium/Playwright automation.
        
    2. **Attribute nodes** are widely used for dynamic locators:
        
    
    ```
    //input[@id='username']
    //button[@class='btn-primary']
    ```
    
    3. **Text nodes** help verify UI text or extract values from tables and labels.
        
    4. **Root node** `/` is rarely used directly in automation; relative XPath `//` is preferred.
        
    5. **Comment, namespace, and processing instruction nodes** are mostly for XML testing or debugging.
        
    
    ---
    
    ## **4\. XPath Axes**
    
    # 📘 **XPath Axes – Detailed Table**
    
    | **Axis** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | `child::` | Selects **direct children** of the current node | `//ul/child::li` | Equivalent to `//ul/li`; use when you need explicit axis |
    | `parent::` | Selects the **parent node** of the current node | `//li/parent::ul` | Useful to navigate upward in DOM |
    | `ancestor::` | Selects **all ancestors** of the current node | `//li/ancestor::div` | Helpful to find container divs or forms |
    | `descendant::` | Selects **all descendants** (children, grandchildren, etc.) | `//div/descendant::p` | Use to locate nested elements inside a container |
    | `following-sibling::` | Selects all **sibling nodes after** the current node | `//li/following-sibling::li` | Useful for lists or menus where you want elements after a specific node |
    | `preceding-sibling::` | Selects all **sibling nodes before** the current node | `//li/preceding-sibling::li` | Useful for selecting previous elements in a list |
    | `self::` | Selects the **current node itself** | `//li/self::li` | Rarely used alone; often combined in complex XPath |
    | `descendant-or-self::` | Selects the **current node and all descendants** | `//div/descendant-or-self::p` | Helps when you want to include the container itself plus nested elements |
    | `ancestor-or-self::` | Selects the **current node and all ancestors** | `//span/ancestor-or-self::div` | Useful to include the node plus its containing hierarchy |
    
    ---
    
    ### **Automation Tips**
    
    1. **Use** `child::` and `descendant::` to navigate through nested containers and lists.
        
    2. `ancestor::` and `parent::` are helpful to locate a container dynamically based on a child element.
        
    3. **Sibling axes** (`following-sibling::` and `preceding-sibling::`) are very useful in **tables, menus, and lists**.
        
    4. **Combine axes with predicates** for robust locators:
        
    
    ```
    //div[@class='container']/descendant::li[position()=2]
    ```
    
    5. `self::` and `descendant-or-self::` are useful in complex hierarchical selections.
        
    
    ---
    
    ## **5\. XPath Predicates**
    
    # 📘 **XPath Predicates – Detailed Table**
    
    | **Predicate Type** | **Example** | **Description** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | **Position-based** | `[position()=1]` | Selects the **first node** in a node-set | Use for first element in a list or table row |
    |  | `[last()]` | Selects the **last node** in a node-set | Handy for dynamic lists or last table row |
    | **Attribute-based** | `[@id='username']` | Filters nodes by **specific attribute value** | Most commonly used for locating elements by ID, class, type |
    |  | `[@class='active']` | Filters nodes by class attribute | Can combine multiple attributes for precise selection |
    | **Text-based** | `[text()='Submit']` | Filters nodes based on **exact text** | Use for buttons, links, labels |
    |  | `[contains(text(),'Login')]` | Filters nodes containing partial text | Useful when text is dynamic or has extra spaces |
    | **Logical / Negation** | `[not(@disabled)]` | Selects nodes where condition is false | Often used to ignore disabled fields or buttons |
    | **Combined / Multiple Predicates** | `//input[@type='text'][position()<=3]` | Apply multiple filters on a single node | Combine position, attributes, and text for robust locators |
    | **Complex Predicates** | `//div[@class='container']//ul/li[position()>=2 and contains(@class,'active')]` | Combines multiple conditions and axes | Powerful for selecting nested or dynamic elements |
    
    ---
    
    ### **Automation Tips**
    
    1. **Always test predicates in browser dev tools** before using in automation.
        
    2. **Combine attributes and text** to make locators robust against dynamic pages.
        
    3. **Position functions** like `position()` and `last()` are essential for lists, tables, and repeated elements.
        
    4. **Negation with** `not()` ensures you interact only with enabled/visible elements.
        
    5. **Use multiple predicates** carefully; order matters:
        
    
    ```
    //ul/li[@class='active'][position()=1]
    ```
    
    ---
    
    # **6\. XPath Functions**
    
    ## 📘 XPath 1.0 String Functions – Detailed Table
    
    | **Function** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | `contains()` | Checks if a string contains a substring | `//a[contains(@href,'github')]` | Useful for dynamic classes, IDs, or partial text matches |
    | `starts-with()` | Checks if a string starts with a specific prefix | `//input[starts-with(@id,'user')]` | Helps handle dynamic IDs or prefixes in locators |
    | `string()` | Converts a node or value to a string | `string(//p[1])` | Use when node value might be numeric but you want to treat as text |
    | `concat()` | Concatenates multiple strings | `concat('Hello ','World')` → `Hello World` | Can dynamically combine text or attributes in XPath |
    | `substring()` | Extracts part of a string | `substring('Hello',2,3)` → `ell` | Useful to match partial text in complex locators |
    | `normalize-space()` | Trims leading/trailing spaces and normalizes inner spaces | `normalize-space(//p)` | Ideal for ignoring extra spaces in UI text during automation |
    | `translate()` | Replaces characters in a string | `translate('Hello','e','a')` → `Hallo` | Useful for simple character replacement or case normalization |
    | `string-length()` | Returns the length of a string | `string-length(//p)` | Can be used to validate text length or presence |
    
    ---
    
    ### **Automation Tips**
    
    1. `contains()` and `starts-with()` are **widely used in Selenium/Playwright** for dynamic XPath.
        
    
    ```bash
    //div[contains(@class,'active')]
    ```
    
    2. `normalize-space()` helps when **UI text has extra spaces or newlines**.
        
    3. `translate()` can be used for **case-insensitive matching**:
        
    
    ```bash
    //span[translate(text(),'ABCDEFGHIJKLMNOPQRSTUVWXYZ','abcdefghijklmnopqrstuvwxyz')='submit']
    ```
    
    4. `concat()` is useful for **combining dynamic strings** in advanced locators.
        
    5. `string-length()` can **validate if a text node exists** or is empty.
        
    
    ## 📘 XPath 1.0 Boolean Functions – Detailed Table
    
    | **Function** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | `boolean()` | Converts a value or node-set to `true` or `false` | `boolean(//div[@id='main'])` | Returns `true` if node exists; commonly used to check element presence |
    | `not()` | Returns the logical NOT of a boolean expression | `//input[not(@disabled)]` | Select nodes **where a condition is false**, e.g., enabled input fields |
    | `true()` | Returns the boolean value `true` | `//div[true()]` | Rarely used directly, mainly in advanced XPath conditions |
    | `false()` | Returns the boolean value `false` | `//div[false()]` | Rarely used directly; can be combined in complex conditions |
    
    ---
    
    ### **Automation Tips**
    
    1. `boolean()` is very useful in **Selenium or Playwright** to check if an element exists:
        
    
    ```bash
    const exists = await page.locator('xpath=boolean(//div[@id="main"])').evaluate(el => el);
    ```
    
    2. `not()` is handy for **ignoring disabled, hidden, or inactive elements**:
        
    
    ```bash
    //button[not(@disabled)]
    ```
    
    3. `true()` and `false()` are less commonly used but can **simplify conditional predicates** in complex XPath expressions.
        
    4. Boolean functions can be **combined with logical operators** (`and`, `or`) for robust locators.
        
    
    ## 📘 **XPath 1.0 Numeric Functions – Detailed Table**
    
    | **Function** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | `number()` | Converts a string or node value to a numeric value | `number(//span[@id='price'])` | Useful for performing arithmetic or comparisons on element text |
    | `sum()` | Returns the sum of a node-set of numeric values | `sum(//td[@class='amount'])` | Commonly used for summing table column values |
    | `floor()` | Returns the largest integer less than or equal to a number | `floor(3.7)` → `3` | Can be used for rounding down prices, counts, or indices |
    | `ceiling()` | Returns the smallest integer greater than or equal to a number | `ceiling(3.2)` → `4` | Can be used for rounding up |
    | `round()` | Rounds a number to the nearest integer | `round(3.5)` → `4` | Useful for rounding prices, totals, or indices |
    
    ---
    
    ### **Automation Tips**
    
    1. `number()` helps **convert text nodes** to numeric values for calculations.
        
    2. `sum()` is very handy for **verifying total amounts in tables or invoices**.
        
    3. `floor()` and `ceiling()` are used to **normalize numbers** in comparisons or loops.
        
    4. `round()` is useful for **financial calculations or UI validations** in tests.
        
    5. Always ensure the **node contains numeric text**, otherwise `number()` may return `NaN`.
        
        ---
        
    
    ## 📘 **XPath 1.0 Node-set Functions – Detailed Table**
    
    | **Function** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | `last()` | Returns the **last node** in the current node-set | `//ul/li[last()]` | Useful to select the last item in a list or table row |
    | `position()` | Returns the **position of a node** in a node-set | `//ul/li[position()=2]` | Select a specific node by its order |
    | `count()` | Returns the **number of nodes** in a node-set | `count(//table[@id='data']//tr)` | Useful for counting table rows or list items |
    | `id()` | Selects elements by their **unique ID** | `id('username')` | Can directly locate elements with ID in XML/HTML |
    | `name()` | Returns the **name of the node** | `name(//div[1])` → `'div'` | Helps identify element type or debug node selection |
    
    ---
    
    ### **Automation Tips**
    
    1. `last()` is **commonly used** to interact with the last row or last element in a dynamic list.
        
    2. `position()` allows you to **iterate or select nodes by index**, e.g., first, second, third item.
        
    3. `count()` helps in **validation**, like verifying table row count.
        
    4. `id()` can simplify XPath when elements have **unique IDs**.
        
    5. `name()` is useful for **debugging or conditional selection** when you need to check node types.
        
    
    ---
    
    ## 📘 **XPath 1.0 Operators – Detailed Table**
    
    | **Operator Type** | **Operator** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- | --- |
    | **Arithmetic** | `+` | Addition of numbers | `//price + 10` | Add numeric values from node text or attributes |
    |  | `-` | Subtraction | `//price - 5` | Subtract numeric values from node text or attributes |
    |  | `*` | Multiplication | `//price * 2` | Multiply numeric node values |
    |  | `div` | Division | `//price div 2` | Divide numeric node values; use `div` instead of `/` |
    |  | `mod` | Modulus | `//price mod 10` | Get remainder of numeric node values |
    | **Comparison** | `=` | Equal to | `//button[@id='submit']='Submit'` | Compare string or numeric values of nodes |
    |  | `!=` | Not equal | `//input[@type!='hidden']` | Filter nodes not matching a value |
    |  | `<` | Less than | `//price < 100` | Compare numeric values |
    |  | `>` | Greater than | `//price > 50` | Compare numeric values |
    |  | `<=` | Less than or equal | `//price <= 50` | Compare numeric values |
    |  | `>=` | Greater than or equal | `//price >= 50` | Compare numeric values |
    | **Logical** | `and` | Logical AND | `//input[@type='text' and @name='username']` | Both conditions must be true for the node to match |
    |  | `or` | Logical OR | `//input[@type='text' or @type='email']` | Either condition can be true |
    |  | `not()` | Logical NOT | `//input[not(@disabled)]` | Select nodes where the condition is false |
    | **Union / Node-set** | \` | \` | Combines multiple node-sets | \`//div |
    
    ---
    
    ### **Automation Tips**
    
    1. **Combine logical operators with predicates** for robust locators:
        
    
    ```bash
    //button[@type='submit' and contains(@class,'primary')]
    ```
    
    2. **Use arithmetic operators** when working with numeric node values (like table data).
        
    3. **Union operator** `|` helps select multiple types of elements at once.
        
    4. **Logical NOT** is useful for ignoring disabled or hidden elements.
        
    5. Always **test XPath in browser dev tools** before using in Selenium or Playwright.
        
    
    ---
    
    # **8\. XPath Expressions**
    
    ## 📘 **XPath Expressions – Detailed Table**
    
    | **Expression Type** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | **Absolute Path Expression** | Starts from the root `/` and follows the full DOM hierarchy | `/html/body/div[2]/ul/li[1]/a` | Fragile; breaks if DOM structure changes; rarely used in automation |
    | **Relative Path Expression** | Starts from anywhere in the document `//` | `//div[@id='main']/ul/li[1]/a` | Preferred in automation; more robust for dynamic pages |
    | **Select by Tag** | Matches elements by tag name | `//p` → selects all `<p>` tags | Useful for headings, paragraphs, table rows, or lists |
    | **Select by Attribute** | Matches elements with a specific attribute | `//input[@type='text']` | Most common and reliable method in automation |
    | **Select by Text** | Matches elements containing exact text | `//button[text()='Submit']` | Useful for buttons, links, and labels |
    | **Select by Partial Text** | Matches elements containing partial text | `//a[contains(text(),'Login')]` | Handles dynamic text or labels |
    | **Using Functions** | XPath functions in predicates for dynamic selection | `//div[contains(@class,'active')]` | Functions like `contains()`, `starts-with()`, `normalize-space()` make locators robust |
    | **Using Axes** | Navigate elements relative to current node | `//li/ancestor::ul` | Axes like `parent::`, `child::`, `following-sibling::` are powerful for nested or dynamic elements |
    | **Using Predicates** | Filter nodes by position, attribute, or conditions | `//ul/li[position()=2]` | Multiple predicates can be combined for precise selection |
    | \*\*Union Operator \` | \`\*\* | Combines multiple XPath expressions | \`//div |
    | **Dynamic XPath** | Combines functions, predicates, and axes for robust locators | `//ul/li[contains(@class,'active')][last()]` | Essential for automation on dynamic pages with changing IDs, classes, or positions |
    
    ---
    
    ### **Automation Tips**
    
    1. Prefer **relative XPath (**`//`) over absolute (`/`) for dynamic pages.
        
    2. Combine **attributes, text, and functions** for robust locators:
        
    
    ```bash
    //button[contains(@class,'submit') and text()='Login']
    ```
    
    3. Use **axes** to navigate to parent, child, sibling, or ancestor elements when structure is complex.
        
    4. Use **predicates** to select specific nodes by position or condition.
        
    5. Test all XPath in **browser DevTools** before using in Selenium/Playwright scripts.
        
    
    ---
    
    ## **9\. XPath 1.0 vs 2.0 vs 3.0**
    
    | Feature | XPath 1.0 | XPath 2.0/3.0 | Notes for Automation |
    | --- | --- | --- | --- |
    | Functions | Basic | Regex, sequences, FLWOR | XPath 1.0 only supported in browsers |
    | Browser Support | ✅ | ❌ | Selenium/Playwright use 1.0 |
    | Complexity | Simple | Complex | Use 1.0 for UI automation |
    
    ---
    
    ## **10\. Advanced XPath Topics**
    
    # 📘 **Advanced XPath Topics – Detailed Table**
    
    | **Topic** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | **Complex Predicates** | Use multiple conditions inside `[ ]` to filter nodes | `//input[@type='text' and @name='username']` | Combine attributes, text, or functions for precise element selection |
    | **Multiple Conditions** | Combine `and` / `or` inside predicates | `//button[@type='submit' or @id='loginBtn']` | Useful when an element may have dynamic attributes |
    | **Selecting Nested Nodes** | Use hierarchy to locate children or descendants | `//div[@class='container']/ul/li/span` | Helps locate deeply nested elements in tables, lists, or menus |
    | **Selecting First Node** | Use `position()` or `[1]` | `//ul/li[position()=1]` | Select the first item in a list or table row |
    | **Selecting Last Node** | Use `last()` | `//ul/li[last()]` | Useful for last element in dynamic lists or tables |
    | **Selecting Middle Node** | Combine `position()` and `last()` | `//ul/li[position()=last()-1]` | Select elements relative to the last node |
    | **Combining Axes and Functions** | Use axes like `ancestor::`, `descendant::` with functions | `//span[contains(text(),'Price')]/ancestor::tr` | Helps locate container or row of a specific element |
    | **Dynamic XPath for Automation** | Handles changing IDs, classes, or text | `//div[contains(@class,'card')][position()=2]//button` | Essential for testing dynamic web pages |
    | **Handling Nested Lists or Tables** | Use axes, predicates, and functions together | `//table[@id='orders']/tbody/tr[position()>1]/td[2]` | Extract or interact with specific cells in tables |
    | **Using Logical Predicates** | Combine `not()`, `and`, `or` | `//input[not(@disabled) and @type='text']` | Ensures only valid, interactable elements are selected |
    | **XPath for SVG or XML** | Use `local-name()` for namespaced elements | `//*[local-name()='svg']/*[local-name()='circle']` | Required for SVG elements in HTML pages or XML files |
    
    ---
    
    ### **Automation Tips**
    
    1. **Use predicates with multiple conditions** to make locators precise:
        
    
    ```bash
    //button[@type='submit' and contains(@class,'primary')]
    ```
    
    2. **Combine axes with functions** to navigate dynamically generated content.
        
    3. **Use** `last()` and `position()` for selecting first, last, or specific nodes in lists/tables.
        
    4. **Dynamic XPath** is critical for modern web applications where IDs or classes frequently change.
        
    5. **Use** `local-name()` for namespaced tags like SVG, XML, or custom elements.
        
    6. Always **test advanced XPath** in browser DevTools before automation.
        
    
    ---
    
    ## **11\. Practical XPath for Automation**
    
    # 📘 **Practical XPath for Automation – Detailed Table**
    
    | **Scenario** | **XPath Example** | **Description / Notes** |
    | --- | --- | --- |
    | **Locate element by ID** | `//input[@id='username']` | Most reliable method in automation |
    | **Locate element by Class** | `//button[contains(@class,'submit-btn')]` | Use `contains()` for dynamic class names |
    | **Locate element by Text** | `//button[text()='Login']` | Exact match of visible text |
    | **Locate element by Partial Text** | `//a[contains(text(),'Forgot')]` | Handles dynamic or partial text |
    | **Locate first element in list** | `//ul/li[1]` | Use `position()` or `[1]` for first element |
    | **Locate last element in list** | `//ul/li[last()]` | Select the last item in a list or table row |
    | **Locate nth element in list** | `//ul/li[position()=3]` | Selects the 3rd element in a list or table row |
    | **Locate element with multiple attributes** | `//input[@type='text' and @name='username']` | Combine attributes for robust locators |
    | **Locate enabled element** | `//button[not(@disabled)]` | Ignore disabled buttons or inputs |
    | **Locate nested element** | `//div[@class='container']//span[@class='price']` | Handles elements deeply nested inside parent containers |
    | **Locate element in dynamic table** | `//table[@id='orders']/tbody/tr[position()=2]/td[3]` | Extracts or interacts with specific table cells |
    | **Locate element using axes** | `//span[text()='Price']/ancestor::tr//input` | Navigate from a known child element to its container or related nodes |
    | **Locate SVG element** | `//*[local-name()='svg']/*[local-name()='circle']` | Use `local-name()` for namespaced SVG tags |
    | **Dynamic XPath with contains** | `//div[contains(@class,'card')][position()=2]//button` | Handles changing IDs, classes, or positions |
    
    ---
    
    ### **Automation Tips**
    
    1. **Prefer relative XPath (**`//`) over absolute (`/`) for dynamic pages.
        
    2. **Combine attributes, text, and functions** to make locators robust.
        
    3. **Use** `contains()`, `starts-with()`, and `normalize-space()` for dynamic text or attributes.
        
    4. **Use axes (**`ancestor::`, `descendant::`, `following-sibling::`) for nested or related elements.
        
    5. **Use** `position()` and `last()` for selecting first, last, or specific nodes in lists or tables.
        
    6. **Test XPath in DevTools** before using in Selenium/Playwright scripts.
        
    
    ---
    
    ## **12\. XPath Best Practices**
    
    # 📘 **XPath Best Practices – Detailed Table**
    
    | **Best Practice** | **Description** | **Example** | **Notes / Automation Tips** |
    | --- | --- | --- | --- |
    | **Prefer Relative XPath** | Use `//` instead of `/` for dynamic pages | `//div[@id='main']/ul/li[2]` | Absolute XPath `/html/body/div/...` is fragile |
    | **Use Attributes Over Text** | Select elements using attributes rather than visible text | `//input[@name='username']` | More reliable, especially when text changes dynamically |
    | **Use Functions for Dynamic Elements** | Functions like `contains()`, `starts-with()`, `normalize-space()` help with dynamic IDs or text | `//button[contains(@class,'submit')]` | Handles dynamic or partially changing attributes/text |
    | **Avoid Overly Long XPath** | Keep XPath concise | `//div[@id='main']//li[3]` | Very long XPaths break easily if DOM changes |
    | **Combine Predicates** | Use multiple conditions for robustness | `//input[@type='text' and @name='username']` | Ensures accurate element selection even in complex DOM |
    | **Use Axes When Necessary** | Use `ancestor::`, `descendant::`, `following-sibling::` for nested elements | `//span[text()='Price']/ancestor::tr//input` | Helps locate elements related to known nodes |
    | **Test XPath in Browser DevTools** | Always verify XPath works in Chrome/Firefox DevTools before automation | `Ctrl+F` in DevTools and paste XPath | Prevents runtime errors in Selenium/Playwright scripts |
    | **Handle Dynamic Lists/Tables** | Use `position()` and `last()` for selecting first, last, or nth element | `//ul/li[position()=last()]` | Essential for tables, dropdowns, and dynamic lists |
    | **Use** `local-name()` for Namespaced Elements | Required for SVG or XML elements | `//*[local-name()='svg']/*[local-name()='circle']` | Ensures XPath works for namespaced tags in HTML/XML |
    | **Keep XPath Readable** | Avoid overly complex or nested XPath | `//div[@class='container']//button[text()='Submit']` | Readable XPaths are easier to maintain in automation scripts |
    
    ---
    
    ### **Automation Tips**
    
    1. **Always prefer relative XPath** (`//`) over absolute for dynamic content.
        
    2. **Combine attributes and functions** for robust and flexible locators.
        
    3. **Avoid hardcoding indices** unless necessary; use `position()` or `last()` carefully.
        
    4. **Use axes and predicates** to navigate complex DOM structures.
        
    5. **Test XPath expressions** in browser DevTools before using in automation scripts.
        
    6. **Keep locators concise and readable** to maintain scripts easily.
        
    

---

## **Why XPath 1.0 is preferred in automation** (Selenium, Playwright, etc.) instead of XPath 2.0

---

## **1️⃣ Browser & Automation Support**

* **XPath 1.0 is natively supported by all major browsers** through `document.evaluate()`.
    
* **XPath 2.0 is NOT supported in browsers**; it is mainly used in **XML processors** like XSLT 2.0, Saxon, or XML databases.
    
* Automation tools like **Selenium** and **Playwright** rely on browser engines for XPath evaluation.
    
* ✅ Only XPath 1.0 works reliably in **real browser automation**.
    

---

## **2️⃣ Simplicity & Reliability**

* XPath 1.0 provides **enough functions and axes** for almost all UI automation needs:
    
    * Node selection (`//div`, `//input`)
        
    * Predicates (`[1]`, `[last()]`, `[@id='x']`)
        
    * Text filters (`contains()`, `starts-with()`)
        
* XPath 1.0 is **stable, well-documented, and easy to maintain**.
    
* XPath 2.0 features (sequences, regex, FLWOR) are **not needed for standard web automation**.
    

---

## **3️⃣ Performance Considerations**

* Browsers **optimize XPath 1.0 evaluation** internally.
    
* XPath 2.0 would require a **custom library or processor**, slowing down automation.
    
* XPath 1.0 keeps **locators fast**, lightweight, and compatible with **dynamic pages**.
    

---

## **4️⃣ Compatibility with Tools**

* **Selenium WebDriver**, **Playwright**, and **Cypress (with plugins)** all support only XPath 1.0.
    
* Using XPath 2.0 functions like `matches()` or `tokenize()` **will break locators**.
    
* XPath 1.0 ensures **cross-browser and cross-platform compatibility**.
    

---

## **5️⃣ Practical Use Cases in Automation**

| Scenario | XPath 1.0 Usage |
| --- | --- |
| Select element by text | `//button[text()='Submit']` |
| Select element with dynamic class | `//div[contains(@class,'active')]` |
| Select last item in list | `//ul/li[last()]` |
| Select first 3 items | `//ul/li[position()<=3]` |
| Click element by partial ID | `//input[starts-with(@id,'user_')]` |

---

### **✅ Summary**

* **Supported everywhere** → Works in browsers and automation tools.
    
* **Simple & maintainable** → Enough functionality for almost all UI tests.
    
* **Fast & reliable** → No additional processing required.
    
* **Future-proof** → Any XPath 1.0 expression works across Selenium, Playwright, and real browsers.
    

---

---

## 📊 **XPath 1.0 vs XPath 2.0 in Automation**

| Feature / Aspect | XPath 1.0 | XPath 2.0 | Notes for Automation |
| --- | --- | --- | --- |
| **Browser Support** | ✅ Fully supported | ❌ Not supported | XPath 2.0 needs XML processors; browsers only support 1.0 |
| **Selenium / Playwright Support** | ✅ Fully supported | ❌ Not supported | All locators in automation must be XPath 1.0 |
| **Node Types** | Element, Attribute, Text, Comment, Root, Namespace | Same + Sequences | XPath 2.0 adds sequences, which are **not usable in automation** |
| **Functions** | Basic: `contains()`, `starts-with()`, `text()`, `normalize-space()`, `count()`, `position()`, `last()` | Extended: Regex (`matches()`, `replace()`, `tokenize()`), Data Types, Aggregate functions | Only **1.0 functions** work in browser automation |
| **Predicates** | `[position()]`, `[last()]`, `[condition]`, `[not()]` | Same + sequences, type checks | Sequences cannot be used; predicates must remain 1.0 compatible |
| **Axes** | `child`, `parent`, `ancestor`, `descendant`, `following-sibling`, `preceding-sibling`, `self` | Same | Fully supported in automation |
| **Operators** | \`=, !=, &lt;, &gt;, &lt;=, &gt;=, and, or, | \` | Extended with `eq, ne, lt, gt, le, ge, intersect, except` |
| **Regex / Advanced Strings** | ❌ Not available | ✅ `matches()`, `replace()`, `tokenize()` | Not supported in browser automation; use JS string methods instead |
| **Sequences** | ❌ Not available | ✅ Supported | XPath 2.0 sequences not usable in Playwright/Selenium |
| **FLWOR Expressions** | ❌ Not available | ✅ Supported | Not supported in automation; only for XML/XSLT processors |
| **Practical Example – Button Click** | `//button[text()='Submit']` ✅ works | `//button[matches(text(),'Submit')]` ❌ fails in browser automation | Use only XPath 1.0 expressions |
| **Practical Example – Dynamic Class** | `//div[contains(@class,'active')]` ✅ works | `//div[matches(@class,'active')]` ❌ fails | Stick with `contains()` and `starts-with()` |

---

### **✅ Key Takeaways for Automation**

1. Always use **XPath 1.0** for Selenium/Playwright.
    
2. XPath 2.0 functions and sequences **will not work** in browser context.
    
3. Use **string functions (**`contains`, `starts-with`, `normalize-space`) for dynamic content.
    
4. Combine **predicates, axes, and positions** for robust locators.
    
5. For regex-like filtering, use **JavaScript string methods** after selecting elements.2️⃣ **XPath Node Types**
    

## 🎯 Topics in XPath 1.0 (to cover via questions)

Some of the main topics in XPath 1.0 that should be tested:

1. **Basic path expressions** (absolute `/`, relative `//`)
    
2. **Node tests** (`*`, `node()`, `text()`, `comment()`, `processing-instruction()`)
    
3. **Axes** (`child`, `descendant`, `parent`, `ancestor`, `following-sibling`, `preceding-sibling`, `following`, `preceding`, `attribute`, `self`, `descendant-or-self`, `ancestor-or-self`)
    
4. **Predicates** (filtering by index, conditions, boolean, multiple predicates)
    
5. **Functions** (e.g. `contains()`, `starts-with()`, `string-length()`, `normalize-space()`, `translate()`, `last()`, `position()`, `not()`, `name()`, `local-name()`)
    
6. **Operators** (`=`, `!=`, `<`, `>`, `<=`, `>=`, `and`, `or`)
    
7. **Attribute selectors** (`@attr`, combining with functions)
    
8. **Text matching** (exact match, case-insensitive matching, partial, contains)
    
9. **Combining paths, union (**`|`)
    
10. **Namespaces and local-name()**
    
11. **Dynamic / partial matches** (`starts-with`, `contains`)
    
12. **Indexing / position / last**
    
13. **Edge / tricky cases** (extra spaces, nested structures, dynamic IDs, mixed case)
    
14. **Frames / iframe context**
    
15. **SVG / nonstandard elements** (using `local-name()`)
    
16. **Limitations** (shadow DOM, etc. – more conceptual)
    

Using the playground page, one can craft questions against its HTML structure (login form, menu, table, profile section, etc.). Below are **individual questions** (you can attempt writing the XPath for each).

---

## ✅ XPath Practice Questions (each separate)

1. Select the **Username** input field in the Login Form
    
2. Select the **Password** input field
    
3. Select the **“Remember me”** checkbox or label
    
4. Select the **Login** button
    
5. Select the **“Forgot password?”** link
    
6. In the main menu, select the node corresponding to **“Admin”**
    
7. Select the **5th** menu item (if “Menu Count: 5”)
    
8. Select **all** menu items (Admin, PIM, Leave, Time, Recruitment)
    
9. Select the **Search** button in the Search Panel
    
10. Select the **“Read our PriVaCy policy”** link (case-insensitive match)
    
11. Select the **“Download Guide (PDF)”** link
    
12. Select the **Logo** image (in the Search Panel)
    
13. From the **Orders Table**, select the **row** for invoice `INV-122`
    
14. From the Orders Table, select the **Product** name cell in the `INV-122` row
    
15. From the Orders Table, select the **Price** cell in the `INV-121` row
    
16. Select the **Pay** button corresponding to `INV-123`
    
17. Select **all** `Pay` buttons in the orders table
    
18. In the Profile Section, select the **Email** label or value
    
19. In the Profile Section, select the **Country** dropdown or option with text “India”
    
20. Select the **Edit** link/button in the Profile section
    
21. Select the element with class token **“Primary CTA”**
    
22. Select the element with class token **“Secondary CTA”**
    
23. Select the element with class token **“rounded chip”**
    
24. Select the element with class token **“tiny chip”**
    
25. Select the **Email Notifications** element under ARIA section
    
26. Select the **SMS Notifications** element
    
27. Select the **SVG** icon (hint: you must use `local-name()`)
    
28. Select a **path** node inside the SVG icon
    
29. Select the **Dynamic Input** field whose `id` starts with `user_`
    
30. Select the **Dynamic Input** whose `id` contains `react-select`
    
31. Open the **Confirm modal** and select the **Cancel** button
    
32. Open the Confirm modal and select the **Delete** button
    
33. In nested structure, select an element by combining axes (e.g. select a descendant of a known parent)
    
34. Use **union (**`|`) to select both “Login” button and “Forgot password?” link
    
35. Select all nodes of type **text()** under a certain parent (e.g. in a table cell)
    
36. Select all **comment()** nodes (if present)
    
37. Select all **processing-instruction()** nodes (if present)
    
38. Use `contains()` to select the “Read our PriVaCy policy” link (case-insensitive)
    
39. Use `starts-with()` to select the `id` starting nodes (dynamic input)
    
40. Use `string-length()` to find elements whose text length &gt; some value
    
41. Use `normalize-space()` to trim extra spaces and match text
    
42. Use `translate()` to convert string to lower-case or upper-case for matching
    
43. Select the **last()** menu item (i.e. “Recruitment”)
    
44. Select the **position() = 2** menu item (“PIM”)
    
45. Use predicate combining **and / or** (e.g. products with price &gt; X and &lt; Y)
    
46. Select Orders rows where price is &gt; 300 (filter condition)
    
47. Select Orders rows where price &lt;= 1000
    
48. Select the first **two** rows of the Orders Table
    
49. Select all **cells** in the Orders Table under “Product” column
    
50. Select all **attribute** nodes (e.g. all `@id`, `@class` in a context)
    
51. Use **ancestor** or **ancestor-or-self** axes to retrieve a parent element
    
52. Use **preceding-sibling** or **following-sibling** to move between cells in a row
    
53. Use **preceding** or **following** axes for nodes before/after a given node
    
54. Use **parent::** axis explicitly to go to parent of a node
    
55. Use **descendant::** axis to get nested elements under a known node
    
56. Use **self::** or **descendant-or-self::** in a path
    
57. Use **ancestor::** or **ancestor-or-self::** from a deep node
    
58. Select nodes using **wildcard** `*` (e.g. any child element)
    
59. Select **any node** `node()` under a certain path
    
60. Combine axes and predicates (e.g. descendant::div\[@class='foo'\]\[position()=1\])
    
61. Edge case: match text with **extra spaces** around (use `normalize-space()`)
    
62. Tricky: select element when there are **nested elements or extra wrappers**
    
63. Conceptual: Explain **why XPath cannot pierce shadow DOM**, and how you'd locate elements in shadow DOM using JS
    
64. In the iframe section (if there is embedded frame) — **switch to frame first**, then inside it locate an element
    
65. Use **local-name()** to handle namespaces or elements without a fixed prefix
    
66. Use union + axes (e.g. select two different elements via different axes)
    
67. Use **not()** in a predicate (e.g. exclude nodes with some class)
    
68. Use **boolean expressions** in predicates (e.g. `[not(@disabled) and contains(@class, 'active')]`)
    
69. Use **multiple predicates in chain** (e.g. `//div[@class='x'][contains(text(),'Y')][position()=1]`)
    
70. Use **complex path chaining** combining many features above.
    

1. Username input
    

```bash
//input[@id='username']
//*[normalize-space()='Username']/following::input[1]
```

2. Password input
    

```json
//*[normalize-space()='Password']/following::input[1]
```

3. “Remember me” checkbox or label
    

```json
//*[contains(normalize-space(.),'Remember me')]
```

4. Login button
    

```json
//*[normalize-space()='Login']
```

5. “Forgot password?” link
    

```json
//*[normalize-space()='Forgot password?']
```

6. Main menu “Admin” node
    

```json
//ul/li[normalize-space()='Admin'] | //*[normalize-space()='Admin']
```

7. 5th menu item (by position)
    

```json
//ul/li[position()=5]
```

8. All menu items
    

```json
//ul/li
```

9. Search button in Search Panel
    

```json
//section//*[contains(normalize-space(),'Search') and (self::button or self::input or contains(@role,'button'))][1]
```

10. “Read our PriVaCy policy” link (case-insensitive)
    

```json
//a[contains(translate(., 'ABCDEFGHIJKLMNOPQRSTUVWXYZ', 'abcdefghijklmnopqrstuvwxyz'), 'privacy')]
```

11. “Download Guide (PDF)” link
    

```json
//a[normalize-space()='Download Guide (PDF)']
```

12. Logo image (in Search Panel)
    

```json
//section//img[contains(@alt,'Logo') or contains(@src,'logo')]|//a[.//img]
```

13. Orders table row for invoice `INV-122`
    

```json
//tr[td[normalize-space()='INV-122']] | //*[normalize-space()='INV-122']/ancestor::tr[1]
```

14. Product name cell in row `INV-122`
    

```json
//tr[td[normalize-space()='INV-122']]/td[normalize-space()!='INV-122' and position()>1][1]
```

*(alternate - explicitly Product column if table columns fixed)*

15. Price cell in row `INV-121`
    

```json
//tr[td[normalize-space()='INV-121']]/td[normalize-space()[string-length()>0] and contains(.,'.')][1]
```

16. Pay button corresponding to `INV-123`
    

```json
//tr[td[normalize-space()='INV-123']]//button[normalize-space()='Pay'] | //tr[td[normalize-space()='INV-123']]//*[normalize-space()='Pay']
```

17. All `Pay` buttons in orders table
    

```json
//table//button[normalize-space()='Pay'] | //table//*[normalize-space()='Pay']
```

18. Email label/value in Profile Section
    

```json
//section[.//h3[normalize-space()='Profile']]//*[normalize-space()='Email']/following::text()[1] | //section//*[normalize-space()='Email']
```

19. Country dropdown option “India”
    

```json
//section//*[contains(normalize-space(),'Country')]//option[normalize-space()='India'] | //*[contains(normalize-space(),'Country')]//*[normalize-space()='India']
```

20. Edit link/button in Profile section
    

```json
//section[.//h3[normalize-space()='Profile']]//*[normalize-space()='Edit']
```

21. Element with class token “Primary CTA”
    

```json
//*[contains(concat(' ', normalize-space(@class),' '), ' Primary CTA ')] | //*[normalize-space()='Primary CTA']
```

22. Element with class token “Secondary CTA”
    

```json
//*[contains(concat(' ', normalize-space(@class),' '), ' Secondary CTA ')] | //*[normalize-space()='Secondary CTA']
```

23. Element with class token “rounded chip”
    

```json
//*[contains(concat(' ', normalize-space(@class),' '), ' rounded ') and contains(concat(' ', normalize-space(@class),' '), ' chip ')] | //*[normalize-space()='rounded chip']
```

24. Element with class token “tiny chip”
    

```json
//*[contains(concat(' ', normalize-space(@class),' '), ' tiny ') and contains(concat(' ', normalize-space(@class),' '), ' chip ')] | //*[normalize-space()='tiny chip']
```

25. Email Notifications element under ARIA section
    

```json
//*[contains(normalize-space(.),'ARIA Attributes')]/following::*[contains(normalize-space(.),'Email Notifications')][1]
```

26. SMS Notifications element
    

```json
//*[contains(normalize-space(.),'SMS Notifications')]
```

27. SVG icon (using `local-name()`)
    

```json
//*[local-name()='svg']
```

28. `path` node inside the SVG icon
    

```json
//*[local-name()='svg']/*[local-name()='path']
```

29. Dynamic Input whose `id` starts with `user_`
    

```json
//*[starts-with(@id,'user_')]
```

30. Dynamic Input whose `id` contains `react-select`
    

```json
//*[contains(@id,'react-select')]
```

31. Confirm modal Cancel button
    

```json
//div[.//text()[contains(.,'Are you sure')]]//*[normalize-space()='Cancel']
```

32. Confirm modal Delete button
    

```json
//div[.//text()[contains(.,'Are you sure')]]//*[normalize-space()='Delete']
```

33. Select a descendant of a known parent (example: descendant of Profile)
    

```json
//section[.//h3[normalize-space()='Profile']]//descendant::*[normalize-space()='Email']
```

34. Union: select both “Login” button and “Forgot password?” link
    

```json
(//*[normalize-space()='Login']) | (//*[normalize-space()='Forgot password?'])
```

35. All `text()` nodes under a certain parent (example a table cell)
    

```json
//tr[td[normalize-space()='INV-120']]/td[2]/text()
```

36. All `comment()` nodes (if present)
    

```json
//comment()
```

37. All `processing-instruction()` nodes (if present)
    

```json
//processing-instruction()
```

38. Use `contains()` to select the PriVaCy policy link (case-insensitive)
    

```json
//a[contains(translate(., 'ABCDEFGHIJKLMNOPQRSTUVWXYZ','abcdefghijklmnopqrstuvwxyz'), 'privacy')]
```

39. Use `starts-with()` for dynamic `id` starting nodes
    

```json
//*[starts-with(@id,'user_')]
```

40. Use `string-length()` to find elements with text length &gt; 10 (example)
    

```json
//*[string-length(normalize-space(.)) > 10]
```

41. Use `normalize-space()` to match text trimmed of extra spaces
    

```json
//*[normalize-space()='Download Guide (PDF)']
```

42. Use `translate()` to do case-insensitive matching (lowercase example)
    

```json
//*[translate(normalize-space(.), 'ABCDEFGHIJKLMNOPQRSTUVWXYZ','abcdefghijklmnopqrstuvwxyz')='read our privacy policy']
```

43. Select the `last()` menu item (“Recruitment”)
    

```json
//ul/li[last()]
```

44. Select the menu item at `position() = 2` (“PIM”)
    

```json
//ul/li[position()=2]
```

45. Predicate combining `and` / `or` (e.g., price &gt; 300 and &lt; 700)
    

```json
//tr[td[normalize-space()='INV-123'] and number(td[3]) > 300 and number(td[3]) < 700]
```

*(adjust td index per table column layout)*

46. Orders rows where price is `> 300`
    

```json
//tr[number(td[3]) > 300]
```

47. Orders rows where price `<= 1000`
    

```json
//tr[number(td[3]) <= 1000]
```

48. First two rows of the Orders Table
    

```json
//table//tr[position() <= 2]
```

49. All cells in Orders Table under “Product” column (assumes fixed column index 2)
    

```json
//table//tr/td[2]
```

50. Select all attribute nodes in context (example: all attrs of first table row)
    

```json
//tr[1]/@*
```

51. Use `ancestor` / `ancestor-or-self` to get parent element (example from Email)
    

```json
//*[normalize-space()='Email']/ancestor::section[1]
```

52. Use `preceding-sibling` / `following-sibling` to move between cells
    

```json
//*[normalize-space()='INV-122']/following-sibling::td[1]   /* price cell if structure is flat */
```

*(or use ancestor::tr then td positions)*

53. Use `preceding` / `following` axes for nodes before/after a node
    

```json
//*[normalize-space()='INV-122']/preceding::tr[1]  /* previous row */
```

54. Use `parent::` axis explicitly
    

```json
//*[normalize-space()='INV-122']/parent::tr
```

55. Use `descendant::` axis to get nested elements under a known node
    

```json
//section[.//h3[normalize-space()='Profile']]/descendant::*
```

56. Use `self::` or `descendant-or-self::` in a path
    

```json
//*[normalize-space()='Profile' and self::h3] | //section[.//h3]/descendant-or-self::*
```

57. Use `ancestor::` or `ancestor-or-self::` from a deep node
    

```json
//*[normalize-space()='Pay']/ancestor::table[1]
```

58. Select nodes using wildcard `*` (any child element)
    

```json
//section[@id]/*      /* children of any section that has id */
```

59. Select any node `node()` under a certain path
    

```json
//section[.//h3[normalize-space()='Profile']]/node()
```

60. Combine axes and predicates (example)
    

```json
//section[.//h3[normalize-space()='Profile']]//descendant::div[contains(@class,'chip')][position()=1]
```

61. Edge: match text with extra spaces using `normalize-space()`
    

```json
//*[normalize-space()='rounded chip']
```

62. Tricky: select element when nested/wrapped (example: Product cell inside extra wrapper)
    

```json
//tr[td[normalize-space()='INV-120']]//descendant::div[normalize-space()='Keyboard'] | //tr[td[normalize-space()='INV-120']]/td[2]
```

63. Conceptual: XPath cannot pierce shadow DOM (explanatory) — locate by JS instead:
    

```json
/* Use JS: document.querySelector('selector').shadowRoot.querySelector('selector') — XPath can't penetrate */
```

64. Iframe: switch to frame, then locate an element inside (XPath for inside)
    

```json
//iframe[contains(@src,'some-frame')]
// inside after switching: //*[normalize-space()='Some inside element']
```

65. Use `local-name()` to handle namespaces / svg / unknown prefixes
    

```json
//*[local-name()='svg']//*[local-name()='path']
```

66. Union + axes (select 2 different elements via different axes)
    

```json
(//ul/li[1]) | (//*[normalize-space()='Search'])
```

67. Use `not()` in predicate (exclude nodes with some class)
    

```json
//*[not(contains(@class,'disabled')) and contains(@class,'cta')]
```

68. Boolean predicate example (not disabled and contains active)
    

```json
//*[@aria-disabled!='true' and contains(@class,'active')]
```

69. Multiple predicates in chain example
    

```json
//div[@class='x'][contains(normalize-space(.),'Y')][position()=1]
```

70. Complex path chaining combining features (example)
    

```json
//section[contains(.,'Orders Table')]//tr[number(td[3]) > 100 and not(contains(.,'Desktop'))][1]//td[2]
```