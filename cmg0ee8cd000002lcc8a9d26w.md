---
title: "XPath for Automation Tester"
datePublished: Fri Sep 26 2025 05:25:06 GMT+0000 (Coordinated Universal Time)
cuid: cmg0ee8cd000002lcc8a9d26w
slug: xpath-for-automation-tester
tags: codewithnini

---

## link for Xpath PlayGround below

[Click on Xpath Playground Link](https://xpath-by-nini.netlify.app/)

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
    
    ## 🔹 Limitations of XPath 1.0
    
    * No advanced string functions like `matches()` (available in XPath 2.0).
        
    * Cannot directly use **regular expressions**.
        
    * Limited numeric and date handling.
        
    
    ### **✅ Key Notes**
    
    * XPath 1.0 is **widely used in Selenium**.
        
    * **Does not support** ends-with(), date functions, or regex (XPath 2.0 only).
        
    * Combine **axes + predicates + functions** to locate complex elements.
        
    * Use **normalize-space()**, `contains()`, `starts-with()` for dynamic XPath.
        

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
    

```json
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