---
title: "Automation Framework for Java Selenium"
datePublished: Mon Sep 29 2025 02:06:21 GMT+0000 (Coordinated Universal Time)
cuid: cmg4hm72z000e02ju9z1hdb15
slug: automation-framework-for-java-selenium
tags: codewithnini

---

# 🔹 1. What is an Automation Framework?

An **Automation Framework** is a **structured set of guidelines, rules, and best practices** used to create and design automated test scripts efficiently.  
It is **not a tool** but a **combination of tools, libraries, and practices** that makes automation:

* Easier to design
    
* Easier to maintain
    
* Easier to scale
    

👉 Think of it as a **blueprint or architecture** for automation testing.

---

# 🔹 2. Why do we need an Automation Framework?

Without a framework, test scripts become **unorganized, duplicated, and difficult to maintain**.  
A good framework provides:

✅ **Reusability** → Common functions (login, DB connection, API calls) can be reused.  
✅ **Maintainability** → Changes in application (like locators) require fewer updates.  
✅ **Scalability** → Can handle large test suites across multiple environments.  
✅ **Reporting** → Provides execution reports (pass/fail, logs, screenshots).  
✅ **Consistency** → All testers follow a common standard of coding.  
✅ **Integration** → CI/CD tools like Jenkins, Git, Jira, TestRail.  
✅ **Cross-platform execution** → Run tests on multiple browsers/devices (via Selenium Grid, cloud providers).

---

# 🔹 3. How to Build an Automation Framework?

Building involves combining **tools, libraries, and design patterns**.

Typical steps:

1. **Choose Technology & Tools** → (Selenium, Cypress, Playwright, RestAssured, Appium, TestNG, Maven, Jenkins, Git).
    
2. **Define Architecture** → Folder structure (src/test/java, testdata, utilities, reports).
    
3. **Implement Reusable Components**
    
    * Base class (browser setup, teardown)
        
    * Page Object Model (POM) for element management
        
    * Utility classes (Excel reader, JSON reader, DB connector)
        
4. **Use Build Tools** → Maven/Gradle for dependency management.
    
5. **Add Reporting** → Allure, ExtentReports, TestNG built-in reports.
    
6. **Continuous Integration** → Jenkins/GitHub Actions for auto execution.
    
7. **Best Practices** → Coding standards, meaningful logs, exception handling.
    

---

# 🔹 4. Types of Automation Frameworks (in detail)

### **(a) Linear Scripting Framework (Record & Playback)**

* **What**: Simple scripts, record actions and play them.
    
* **Why**: Quick to implement, no advanced coding required.
    
* **Limitations**: Not maintainable, no reusability.
    
* **Best for**: Small projects / Proof of concept.
    

---

### **(b) Modular Driven Framework**

* **What**: Application is divided into smaller modules, each having its own test script.
    
* **Why**: Reusability → same module can be called in different test cases.
    
* **Example**: Separate modules for login, product search, checkout.
    
* **Limitations**: High upfront effort in modularization.
    

---

### **(c) Data Driven Framework**

* **What**: Test data is separated from test scripts, stored in external sources (Excel, CSV, DB, JSON).
    
* **Why**: Same script can run with multiple data sets.
    
* **Example**: Login test → run with 50 usernames & passwords.
    
* **Tools**: Apache POI, Jackson, Gson, JDBC.
    

---

### **(d) Keyword Driven Framework**

* **What**: Uses keywords (actions) stored in Excel/DB to define test cases.
    
* **Why**: Non-programmers (manual testers/BA) can create test cases without coding.
    
* **Example**:
    
    | Keyword | Object | Data |
    | --- | --- | --- |
    | Click | loginButton |  |
    | Enter | username | "admin" |
    
* **Limitation**: Needs strong mapping engine.
    

---

### **(e) Hybrid Framework**

* **What**: Combination of **Data Driven + Keyword Driven + Modular**.
    
* **Why**: Most real-world companies use hybrid for flexibility.
    
* **Example**: Selenium + TestNG + POM + Data Driven + Extent Reports.
    
* **Best for**: Enterprise-level applications.
    

---

### **(f) Behavior Driven Development (BDD) Framework**

* **What**: Uses **plain English (Gherkin)** syntax for writing test cases.
    
* **Why**: Bridges gap between business analysts, developers, and testers.
    
* **Example**:
    
    ```java
    Feature: Login functionality
      Scenario: Valid login
        Given user is on login page
        When user enters valid credentials
        Then user should see homepage
    ```
    
* **Tools**: Cucumber, JBehave, SpecFlow.
    

---

### **(g) Page Object Model (POM) Framework**

* **What**: Each page of application is represented as a **class**, with elements & methods inside.
    
* **Why**: Reduces code duplication, improves readability.
    
* **Example**:
    
    ```java
    public class LoginPage {
        WebDriver driver;
        By username = By.id("user");
        By password = By.id("pass");
        By loginBtn = By.id("login");
        
        public void login(String user, String pass) {
            driver.findElement(username).sendKeys(user);
            driver.findElement(password).sendKeys(pass);
            driver.findElement(loginBtn).click();
        }
    }
    ```
    

---

### **(h) Hybrid BDD with POM (Most Popular Now)**

* Combination of **POM + Data Driven + BDD (Cucumber/TestNG)**
    
* Industry standard for large automation teams.
    

---

✅ **Summary Table**

| **Framework Type** | **Key Feature** | **Best For** |
| --- | --- | --- |
| Linear Scripting | Record & Playback | Small, quick tests |
| Modular Driven | Separate modules | Mid-sized apps |
| Data Driven | Data externalized | Multiple test datasets |
| Keyword Driven | Keywords in files | Non-coders involvement |
| Hybrid | Mix of all | Large applications |
| BDD (Cucumber) | Gherkin syntax | Collaboration (Agile) |
| POM | Page classes abstraction | Scalable UI testing |

# Components Of Framework

# **Reporting**

## **Extent Reports**

**Extent Reports is a popular reporting library used in automation testing, especially with Selenium and TestNG, to generate interactive and visually appealing HTML reports. Unlike the default TestNG reports, which are basic and plain, Extent Reports allows testers to log detailed test execution steps, including pass/fail status, informational messages, and even screenshots for failed steps. It provides a clear, structured, and easy-to-read report that helps both testers and stakeholders understand the test results quickly.**

**The advantages of Extent Reports over default TestNG reports are significant. First, it allows step-by-step logging, so you can see exactly which actions passed or failed during the test execution. Second, it supports attaching screenshots, which is very useful for debugging failed test cases. Third, it is highly customizable—you can add themes, set report names, authors, categories, and organize tests by modules or priority. Fourth, it supports multiple tests in a single report, giving a consolidated view of the entire test suite. Overall, Extent Reports makes test reporting more professional, interactive, and easier to analyze compared to standard TestNG reports.**

**In my projects, I have used Extent Reports to generate HTML reports of Selenium test execution. It shows test steps with pass/fail/skip status, environment details like OS and browser, and I can also attach screenshots for failed cases.**

How to implement extent reports.

**In my framework, I generate reports using Extent Reports library. First, I create an object of the ExtentSparkReporter class, which is used to define the report file path, title, name, and theme. Then I create an object of the ExtentReports class, which is the main class responsible for report generation, and attach the reporter to it.**

**For each test case, I use the ExtentTest interface (returned by the createTest() method of ExtentReports) to log execution steps. While logging, I use the Status enum (like** [**Status.INFO**](http://Status.INFO)**, Status.PASS,** [**Status.FAIL**](http://Status.FAIL)**, Status.SKIP) to specify the test step result. At the end, I call the flush() method of ExtentReports to actually write all the logs into the HTML report.**

```java
import com.aventstack.extentreports.ExtentReports;
import com.aventstack.extentreports.ExtentTest;
import com.aventstack.extentreports.Status;
import com.aventstack.extentreports.reporter.ExtentSparkReporter;
import com.aventstack.extentreports.reporter.configuration.Theme;

import java.util.Date;

public class ExtentReportEnhanced {

    public static void main(String[] args) {

        // Step 1: Setup Spark Reporter with timestamp in file name
        String timeStamp = new Date().toString().replace(" ", "_").replace(":", "_");
        String reportPath = "extentReport_" + timeStamp + ".html";

        ExtentSparkReporter spark = new ExtentSparkReporter(reportPath);
        spark.config().setDocumentTitle("CRM Test Report");
        spark.config().setReportName("Automation Execution Report");
        spark.config().setTheme(Theme.DARK);

        // Step 2: Create ExtentReports instance and attach reporter
        ExtentReports extent = new ExtentReports();
        extent.attachReporter(spark);

        // Step 3: Add environment/system details
        extent.setSystemInfo("OS", "Windows 10");
        extent.setSystemInfo("Browser", "Chrome 122");
        extent.setSystemInfo("Tester", "Saddam");

        // Step 4: Create a test and add logs
        ExtentTest test = extent.createTest("Login Test");
        test.log(Status.INFO, "Browser launched successfully");
        test.log(Status.PASS, "User logged in successfully");

        // Step 5: Generate the report
        extent.flush();

        System.out.println("Report generated at: " + reportPath);
    }

}
```

# 🔹 1. What is ExtentReports?

**ExtentReports** is a **reporting library** for test automation that generates **interactive, visually rich HTML reports**.  
It works as a **logging framework** where you create tests, log steps, capture screenshots, and finally flush the logs to an HTML file.

* It’s **not a testing framework** (like TestNG/JUnit) — instead, it integrates with them to **represent results better**.
    
* Think of it as a **beautiful, interactive replacement for TestNG’s default reports**.
    

---

# 🔹 2. Why ExtentReports?

Default TestNG/JUnit reports are:

* Plain, text-heavy, and not interactive.
    
* Hard for non-technical stakeholders to understand.
    
* Difficult to analyze in large projects.
    

**ExtentReports solves these problems**:  
✅ Provides a **dashboard view** with pass/fail/skip trends.  
✅ Supports **step-wise logging** (info, warning, pass, fail).  
✅ Embeds **screenshots** (path or base64).  
✅ Allows **categories**, **authors**, **devices** (helpful for parallel/CI).  
✅ Supports **multiple reporters** (HTML, Spark, Klov, Avent,Email,JSON etc.).  
✅ **CI/CD friendly** → Can be published in Jenkins, GitHub Actions, Azure DevOps.

---

# 🔹 3. Core Concepts

ExtentReports works around 3 main components:

### 1️⃣ **ExtentReports Object**

* Main class.
    
* Manages all tests.
    
* Created once, flushed at the end.
    

```java
ExtentReports extent = new ExtentReports();
extent.attachReporter(new ExtentSparkReporter("extent.html"));
```

---

### 2️⃣ **ExtentTest Object**

* Represents a single test.
    
* Logs steps, statuses, screenshots.
    

```java
ExtentTest test = extent.createTest("Login Test");
test.pass("Opened login page");
test.fail("Login failed");
```

---

### 3️⃣ **Reporters**

Define the **output format**:

* **ExtentSparkReporter** → Modern interactive HTML (most used).
    
* **ExtentHtmlReporter** → Legacy HTML.
    
* **KlovReporter** → Realtime MongoDB dashboard.
    
* **ExtentLoggerReporter** → JSON/XML.
    
* **AventRepporter** → Modern interactive HTML (most used).
    
* **EmailReporter** → ExtentEmailReporter creates an elegant, email-friendly report and support both BDD and non-BDD test styles.
    

---

# 🔹 4. Logging Levels

ExtentReports supports **log levels** similar to logging frameworks:

* `test.pass("Step passed")`
    
* [`test.fail`](http://test.fail)`("Step failed")`
    
* `test.skip("Step skipped")`
    
* [`test.info`](http://test.info)`("Information log")`
    
* `test.warning("Warning message")`
    

Example:

```java
test.info("Launching browser");
test.pass("User navigated to login page");
test.fail("Login button not found");
```

---

# 🔹 5. Attaching Screenshots

Screenshots make debugging easier. ExtentReports supports:

* **Path-based screenshots**
    

```java
test.fail("Failed Screenshot", 
    MediaEntityBuilder.createScreenCaptureFromPath("path/to/screenshot.png").build());
```

* **Base64 screenshots** (recommended in CI/CD)
    

```java
test.fail("Failed Screenshot",
    MediaEntityBuilder.createScreenCaptureFromBase64String(base64Screenshot).build());
```

👉 **Base64 is better** because no file path issues in Jenkins.

---

# 🔹 6. Features in Detail

✅ **Dashboard** → Summary view (Total, Pass, Fail, Skip).  
✅ **Category/Tagging** → Group tests as `Smoke`, `Regression`, `Sanity`.

```java
test.assignCategory("Smoke", "UI");
```

✅ **Author/Device tagging** → Track who wrote tests and where they ran.

```java
test.assignAuthor("Nini").assignDevice("Chrome 120");
```

✅ **Nested tests (Nodes)** → Log BDD steps (Given/When/Then).  
✅ **Parallel test support** → Use `ThreadLocal<ExtentTest>`.  
✅ **Multiple Reporters** → Same execution can output HTML + JSON + Klov.

---

# 🔹 7. Integration in Java + Selenium + TestNG

### 📌 Step 1: Add dependency (pom.xml)

```java
<dependency>
  <groupId>com.aventstack</groupId>
  <artifactId>extentreports</artifactId>
  <version>5.1.2</version>
</dependency>
```

---

### 📌 Step 2: Create ExtentManager (Singleton)

```java
public class ExtentManager {
    private static ExtentReports extent;

    public static ExtentReports getInstance() {
        if (extent == null) {
            ExtentSparkReporter reporter = new ExtentSparkReporter("target/extent.html");
            reporter.config().setReportName("Automation Report");
            reporter.config().setDocumentTitle("Test Results");

            extent = new ExtentReports();
            extent.attachReporter(reporter);
        }
        return extent;
    }
}
```

---

### 📌 Step 3: Create Listener (TestNG ITestListener)

```java
public class TestListener implements ITestListener {
    private static ExtentReports extent = ExtentManager.getInstance();
    private static ThreadLocal<ExtentTest> test = new ThreadLocal<>();

    @Override
    public void onTestStart(ITestResult result) {
        test.set(extent.createTest(result.getMethod().getMethodName()));
    }

    @Override
    public void onTestSuccess(ITestResult result) {
        test.get().pass("Test passed");
    }

    @Override
    public void onTestFailure(ITestResult result) {
        test.get().fail(result.getThrowable());
    }

    @Override
    public void onFinish(ITestContext context) {
        extent.flush();
    }
}
```

---

### 📌 Step 4: Add Listener in testng.xml

```java
<listeners>
    <listener class-name="listeners.TestListener"/>
</listeners>
```

---

### 📌 Step 5: Example Test Case

```java
@Test
public void loginTest() {
    WebDriver driver = new ChromeDriver();
    driver.get("https://example.com/login");
    Assert.assertTrue(driver.getTitle().contains("Login"));
    driver.quit();
}
```

---

# 🔹 8. Jenkins Integration

### ✅ Freestyle Job

1. Run tests using Maven (`mvn clean test`).
    
2. Install **HTML Publisher Plugin**.
    
3. Post-build → Publish HTML Report:
    
    * Directory: `target/`
        
    * Index page: `extent.html`
        
    * Title: `Extent Report`
        

### ✅ Jenkins Pipeline

```java
pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        sh 'mvn clean test'
      }
    }
    stage('Report') {
      steps {
        publishHTML(target: [
          allowMissing: false,
          alwaysLinkToLastBuild: true,
          keepAll: true,
          reportDir: 'target',
          reportFiles: 'extent.html',
          reportName: 'Extent Report'
        ])
      }
    }
  }
}
```

---

# 🔹 9. Advanced Usage

* **Multiple Reports**: Generate Spark + JSON in one run.
    
* **BDD Style**: Create nodes (`test.createNode("Given user is on login page")`).
    
* **Klov Reporting**: Real-time dashboard using MongoDB + Klov server.
    
* **Custom Themes**: Dark/Standard.
    
* **Parallel Execution**: Must use `ThreadLocal<ExtentTest>`.
    

---

# 🔹 10. Best Practices

✅ Use **Base64 screenshots** → avoids broken image issues in Jenkins.  
✅ Call `extent.flush()` **only once** (in `onFinish`).  
✅ Keep **report path consistent** (`target/ExtentReports/extent.html`).  
✅ Archive the **entire report folder** in CI/CD.  
✅ Tag tests with **category & author** for filtering.

---

✅ In short:

* **ExtentReports = professional-grade, interactive test reporting**.
    
* It makes your Selenium framework **stakeholder-friendly**.
    
* With **screenshots, tagging, CI/CD integration**, it becomes **standard in automation frameworks**.