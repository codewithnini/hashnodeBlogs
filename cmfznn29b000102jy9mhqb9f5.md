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
// HelloWorld.java
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