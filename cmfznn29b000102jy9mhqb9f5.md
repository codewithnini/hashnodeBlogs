---
title: "Java Basic to Advance"
datePublished: Thu Sep 25 2025 16:56:08 GMT+0000 (Coordinated Universal Time)
cuid: cmfznn29b000102jy9mhqb9f5
slug: java-basic-to-advance
tags: codewithnini

---

# **🟢 Java**

# Hello **World**

## 🔹 **1\. What is “Hello World” Program?**

A **Hello World** program is the **simplest program** in any language, used to verify that the programming environment is correctly set up. In Java, it also introduces **classes, methods, and the** `main` method.

`Here i am using my name ,when i am using my name for giving example, i feel happy .`

---

## 🔹 **2\. Java Program Structure**

Every Java program contains at least:

1. **Class** – Java is **object-oriented**, so code is inside a class.
    
2. **main() method** – Entry point of the program.
    

---

## 🔹 **3\. Code Example**

```java
// HelloNini .java
public class HelloNini {
    public static void main(String[] args) {
        // Print message to console
        System.out.println("Hello, Nini!");
    }
}
```

---

## 🔹 **4\. Explanation of Each Part**

| Part | Purpose |
| --- | --- |
| `public class HelloWorld` | Defines a class named `HelloNini` . `public` means accessible anywhere. |
| `{ ... }` | Curly braces define the **body of class/method**. |
| `public static void main(String[] args)` | **Entry point** of Java program. JVM starts execution here. |
| `System.out.println("Hello, World!");` | Prints text to the console. `System.out` is standard output stream, `println` prints line. |

---

## 🔹 **5\. How to Run Java Program**

### Step 1: Install Java

1. Download and install **JDK** from [Oracle JDK](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html) or OpenJDK.
    
2. Set `JAVA_HOME` and add `bin` to PATH.
    

Check installation:

```java
java -version
javac -version
```

---

### Step 2: Write Code

* Save the code in a file named **HelloWorld.java** (class name = file name).
    

---

### Step 3: Compile Code

Open terminal/command prompt:

```java
javac HelloWorld.java
```

* This creates **HelloWorld.class** (bytecode file).
    

---

### Step 4: Run Code

```java
java HelloWorld
```

✅ Output:

```java
Hello, World!
```

---

## 🔹 **6\. Variations of Hello World**

### 6.1 Without `public` class

```java
class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

✅ Works, but class **cannot be public** if filename differs.

---

### 6.2 Using Variable

```java
class HelloWorld {
    public static void main(String[] args) {
        String message = "Hello, World!";
        System.out.println(message);
    }
}
```

---

### 6.3 Using Method

```java
class HelloWorld {
    public static void main(String[] args) {
        greet();
    }

    public static void greet() {
        System.out.println("Hello, World!");
    }
}
```

---

## 🔹 **7\. Key Points for Beginners**

1. Java is **case-sensitive** (`System` ≠ `system`).
    
2. Every statement ends with a **semicolon** `;`.
    
3. **Curly braces** `{}` are mandatory for class/method body.
    
4. **File name must match public class name**.
    
5. **main() method is mandatory** to run program directly.
    

---

## 🔹 **8\. Real-World Analogy**

* Class → Blueprint of a house.
    
* main() → Door where people enter.
    
* System.out.println() → Message board inside house.
    

# Java Variables and Data Types

# 🔹 **Java Variables and Data Types — Complete Tutorial**

---

## 1\. **What is a Variable?**

* A **variable** is a **named memory location** to store data.
    
* Every variable has:
    
    1. **Name** – identifier
        
    2. **Data type** – type of data it can store
        
    3. **Value** – actual data
        

**Example:**

```java
int age = 25;
String name = "John";
```

---

## 2\. **Types of Variables in Java**

| Variable Type | Declared Where | Lifetime / Scope | Example |
| --- | --- | --- | --- |
| **Instance Variable** | Inside class, outside methods | Exists as long as object exists | `int age;` |
| **Static / Class Variable** | Inside class with `static` keyword | Shared by all objects | `static String company = "OpenAI";` |
| **Local Variable** | Inside method/block | Exists only during method execution | `double salary = 50000;` |
| **Parameter Variable** | Method parameter | Exists during method execution | `void setName(String name)` |

---

### **Memory Allocation**

* **Stack Memory:** Stores **local variables** & method calls.
    
* **Heap Memory:** Stores **objects and instance variables**.
    
* **Static Memory:** Stores **static variables** (shared across objects).
    

---

## 3\. **Java Data Types**

### A. **Primitive Data Types (8 types)**

| Type | Size | Default | Example | Description |
| --- | --- | --- | --- | --- |
| byte | 1 B | 0 | `byte b = 10;` | Small integers |
| short | 2 B | 0 | `short s = 100;` | Small integers |
| int | 4 B | 0 | `int age = 25;` | Integer numbers |
| long | 8 B | 0L | `long pop = 7800000000L;` | Large integers |
| float | 4 B | 0.0f | `float price = 10.5f;` | Decimal numbers |
| double | 8 B | 0.0d | `double pi = 3.14159;` | High precision decimal |
| char | 2 B | '\\u0000' | `char grade = 'A';` | Single character |
| boolean | 1 bit | false | `boolean isActive = true;` | true/false |

---

### B. **Reference / Non-Primitive Data Types**

* Objects, Strings, Arrays, Interfaces, Classes
    
* Stored in **Heap Memory**
    
* Example:
    

```java
String name = "John";
int[] numbers = {1, 2, 3};
```

---

## 4\. **Instance vs Static vs Local Variables**

| Feature | Instance Variable | Static Variable | Local Variable |
| --- | --- | --- | --- |
| Scope | Object level | Class level | Method/block only |
| Memory | Heap | Static memory | Stack memory |
| Access | via object | via class or object | Only inside method/block |
| Default Value | Yes | Yes | No (must initialize) |

**Example:**

```java
class Employee {
    int age;                   // instance variable
    static String company = "OpenAI"; // static variable

    void setSalary(double salary) {  // local variable
        System.out.println("Salary: " + salary);
    }
}
```

---

## 5\. **Variable Naming Rules**

1. Must start with letter, `$`, or `_`
    
2. Cannot start with number
    
3. Case-sensitive (`age` ≠ `Age`)
    
4. Cannot use reserved keywords (`int`, `class`, etc.)
    

---

## 6\. **Examples**

### Example 1: Primitive Variables

```java
class Demo {
    public static void main(String[] args) {
        int age = 25;
        float salary = 50000.50f;
        char grade = 'A';
        boolean isActive = true;

        System.out.println("Age: " + age);
        System.out.println("Salary: " + salary);
        System.out.println("Grade: " + grade);
        System.out.println("Active: " + isActive);
    }
}
```

### Example 2: Reference Variables

```java
class Demo {
    public static void main(String[] args) {
        String name = "John";
        int[] numbers = {1, 2, 3};

        System.out.println("Name: " + name);
        System.out.println("Numbers[0]: " + numbers[0]);
    }
}
```

### Example 3: Instance vs Static

```java
class Employee {
    int age; // instance
    static String company = "OpenAI"; // static

    void showAge() {
        System.out.println("Age: " + age);
    }

    static void showCompany() {
        System.out.println("Company: " + company);
    }
}

public class Test {
    public static void main(String[] args) {
        Employee e1 = new Employee();
        e1.age = 25;
        Employee e2 = new Employee();
        e2.age = 30;

        e1.showAge(); // 25
        e2.showAge(); // 30
        Employee.showCompany(); // OpenAI
    }
}
```

---

## 7\. **Quick Visual Summary**

```java
Memory Allocation:

Stack:           Heap:                  Static:
---------------- -------------------    -------------------
Local vars       Instance vars          Static vars
Method calls     Objects                Shared across objects
Temporary        Live with object       Class level
```

---

✅ **Key Takeaways**

1. Primitive types → stored in stack (local) or heap (instance).
    
2. Reference types → stored in heap.
    
3. `static` → shared across objects.
    
4. Variables must be **initialized before use** (except instance/static variables).
    
5. Scope determines **visibility and lifetime**.