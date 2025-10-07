---
title: "Jdbc Api"
datePublished: Tue Oct 07 2025 06:08:58 GMT+0000 (Coordinated Universal Time)
cuid: cmgg5t0gt000002jr3u3j90fp
slug: jdbc-api
tags: codewithnini

---

## 🧩 **1\. What is JDBC API?**

**JDBC (Java Database Connectivity)** is a **Java API** that allows Java programs to **connect to and interact with databases**.

It provides methods to:

* Establish connection with a database
    
* Send SQL queries (SELECT, INSERT, UPDATE, DELETE)
    
* Retrieve and verify data
    
* Close connections
    

---

## 🎯 **2\. Why JDBC is Important for Automation Testers**

Automation testers use JDBC to:

* **Validate data** after front-end or API actions (UI → DB verification)
    
* **Perform backend testing** directly
    
* **Cross-verify** data between UI/API and Database
    
* **Check test data setup and cleanup** before or after tests
    

Example:  
You submit a form in the UI → now you verify in DB that the record got inserted correctly.

---

## ⚙️ **3\. JDBC Architecture (4 Main Components)**

| Component | Description |
| --- | --- |
| **DriverManager** | Loads database drivers and manages connections |
| **Connection** | Represents a session between Java app and database |
| **Statement / PreparedStatement** | Executes SQL queries |
| **ResultSet** | Holds data retrieved from database (like a table of results) |

---

## 🧠 **4\. JDBC Steps (For Test Automation)**

### ➤ Step 1: Load the JDBC Driver

```typescript
Class.forName("com.mysql.cj.jdbc.Driver");
```

### ➤ Step 2: Establish Connection

```typescript
Connection con = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/employees", "root", "password");
```

### ➤ Step 3: Create Statement

```typescript
Statement stmt = con.createStatement();
```

### ➤ Step 4: Execute Query

```typescript
ResultSet rs = stmt.executeQuery("SELECT * FROM employee WHERE id=101");
```

### ➤ Step 5: Process Result

```typescript
while(rs.next()) {
    String name = rs.getString("name");
    System.out.println("Employee Name: " + name);
}
```

### ➤ Step 6: Close Connection

```typescript
rs.close();
stmt.close();
con.close();
```

---

# 💫 JDBC Practice Setup — Friendship Table.

---

## 🧱 **1️⃣ Database & Table Creation Script**

Let’s create a small social-style table to store friendships 👇

### 📘 SQL Script (Run in MySQL Workbench)

```typescript
-- Step 1: Create a new database
CREATE DATABASE IF NOT EXISTS friendship_db;

-- Step 2: Use the database
USE friendship_db;

-- Step 3: Create the friendship table
CREATE TABLE friendship (
    id INT AUTO_INCREMENT PRIMARY KEY,
    person_name VARCHAR(50) NOT NULL,
    friend_name VARCHAR(50) NOT NULL,
    friendship_level VARCHAR(20) CHECK (friendship_level IN ('Bestie', 'Close', 'Good', 'Casual')),
    connected_since DATE,
    city VARCHAR(50)
);

-- Step 4: Insert some sample data
INSERT INTO friendship (person_name, friend_name, friendship_level, connected_since, city)
VALUES 
('Nini', 'Riya', 'Bestie', '2019-03-15', 'Bangalore'),
('Nini', 'Amit', 'Good', '2020-06-11', 'Pune'),
('Nini', 'Sara', 'Close', '2021-01-25', 'Delhi'),
('Nini', 'Raj', 'Casual', '2022-08-10', 'Hyderabad');
```

✅ After running this, you’ll have:

```markdown
+----+-------------+-------------+------------------+----------------+-----------+
| id | person_name | friend_name | friendship_level | connected_since | city      |
+----+-------------+-------------+------------------+----------------+-----------+
| 1  | Nini        | Riya        | Bestie           | 2019-03-15     | Bangalore |
| 2  | Nini        | Amit        | Good             | 2020-06-11     | Pune      |
| 3  | Nini        | Sara        | Close            | 2021-01-25     | Delhi     |
| 4  | Nini        | Raj         | Casual           | 2022-08-10     | Hyderabad |
+----+-------------+-------------+------------------+----------------+-----------+
```

---

## ⚙️ **2️⃣ JDBC Connection Setup**

Same structure as before, just change DB name and table name.

```java
import java.sql.*;

public class FriendshipJDBC {
    public static void main(String[] args) {
        Connection con = null;
        Statement stmt = null;
        ResultSet rs = null;

        try {
            // Load MySQL Driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Connect to friendship_db
            con = DriverManager.getConnection(
                    "jdbc:mysql://localhost:3306/friendship_db?useSSL=false&serverTimezone=UTC",
                    "root",
                    "password" // change this to your MySQL password
            );

            System.out.println("✅ Connected to friendship_db successfully!");

            // Create statement
            stmt = con.createStatement();

            // Example query: fetch Nini’s best friends
            rs = stmt.executeQuery("SELECT * FROM friendship WHERE person_name='Nini' AND friendship_level='Bestie'");

            // Process results
            while (rs.next()) {
                System.out.println("💖 " + rs.getString("friend_name") + " is Nini’s Bestie from " +
                        rs.getString("city") + " since " + rs.getDate("connected_since"));
            }

        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                if (rs != null) rs.close();
                if (stmt != null) stmt.close();
                if (con != null) con.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
```

---

## 🧪 **3️⃣ Example Output**

When you run this class, you’ll see:

```bash
✅ Connected to friendship_db successfully!
💖 Riya is Nini’s Bestie from Bangalore since 2019-03-15
```

---

## 💡 **4️⃣ Practice Queries You Can Try**

| Goal | SQL Query Example |
| --- | --- |
| Show all Nini’s friends | `SELECT * FROM friendship WHERE person_name='Nini';` |
| Count total friends | `SELECT COUNT(*) FROM friendship WHERE person_name='Nini';` |
| Find oldest friendship | `SELECT * FROM friendship ORDER BY connected_since ASC LIMIT 1;` |
| Add a new friend | `INSERT INTO friendship (person_name, friend_name, friendship_level, connected_since, city) VALUES ('Nini', 'Kiran', 'Close', '2023-05-22', 'Mumbai');` |

---

## 🔍 **5️⃣ Interview Angle**

| Question | Example Answer |
| --- | --- |
| How can you test DB data consistency in automation? | Use JDBC to validate backend records after UI/API actions. |
| Which JDBC driver is used for MySQL? | `com.mysql.cj.jdbc.Driver` |
| What type of result does `executeQuery()` return? | `ResultSet` |
| What happens if DB credentials are wrong? | `SQLException: Access denied` is thrown. |

## 🔍 **5\. Example: Database Validation in Selenium/TestNG**

Suppose you automate a registration form:

1. Fill out and submit using Selenium.
    
2. Verify data in DB using JDBC.
    

```typescript
@Test
public void verifyUserRegistration() throws Exception {
    // Step 1: Perform UI Action
    driver.findElement(By.id("username")).sendKeys("John");
    driver.findElement(By.id("email")).sendKeys("john@test.com");
    driver.findElement(By.id("submit")).click();
    
    // Step 2: Verify in Database
    Class.forName("com.mysql.cj.jdbc.Driver");
    Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/appdb", "root", "password");
    Statement stmt = con.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT * FROM users WHERE email='john@test.com'");
    
    Assert.assertTrue(rs.next(), "User record not found in DB!");
    
    // Optional: Validate data
    Assert.assertEquals(rs.getString("username"), "John");
    
    rs.close();
    stmt.close();
    con.close();
}
```

---

## 🧰 **6\. Common Databases Supported**

* MySQL → `com.mysql.cj.jdbc.Driver`
    
* Oracle → `oracle.jdbc.driver.OracleDriver`
    
* PostgreSQL → `org.postgresql.Driver`
    
* MS SQL Server → [`com.microsoft`](http://com.microsoft)`.sqlserver.jdbc.SQLServerDriver`
    

---

## 🧾 **7\. Maven Dependency for JDBC (MySQL Example)**

```typescript
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.33</version>
</dependency>
```

---

## 🧪 **8\. Real-world Use Cases for Automation Testers**

| Scenario | How JDBC Helps |
| --- | --- |
| Verify record insertion after form submission | Fetch DB record and compare with UI input |
| Verify API response matches DB data | Compare API JSON vs SQL query result |
| Data-driven testing | Fetch test data dynamically from DB |
| Test cleanup | Delete test data from DB post execution |

---

## ⚡ **9\. Best Practices**

* Always **close connection** in `finally` block.
    
* Use **PreparedStatement** instead of Statement to prevent SQL Injection.
    
* Keep DB credentials in a **config file** (not hardcoded).
    
* Use **utility class** for DB connections (reusable methods).
    

---

## 🧱 **10\. Sample JDBC Utility Class**

```typescript
public class DBUtils {
    private static Connection con;

    public static Connection getConnection() throws Exception {
        if (con == null) {
            Class.forName("com.mysql.cj.jdbc.Driver");
            con = DriverManager.getConnection("jdbc:mysql://localhost:3306/appdb", "root", "password");
        }
        return con;
    }

    public static ResultSet executeQuery(String query) throws Exception {
        Statement stmt = getConnection().createStatement();
        return stmt.executeQuery(query);
    }

    public static void closeConnection() throws Exception {
        if (con != null)
            con.close();
    }
}
```

Then in your test:

```typescript
ResultSet rs = DBUtils.executeQuery("SELECT * FROM users");
```

---

## 🧩 **Summary for Interviews**

| Question | Short Answer |
| --- | --- |
| What is JDBC? | API that allows Java programs to connect and interact with databases. |
| Why do automation testers use JDBC? | For backend verification, data validation, and test data management. |
| Key classes? | DriverManager, Connection, Statement, ResultSet. |
| Steps to use JDBC? | Load driver → Connect → Execute → Process → Close. |
| Difference between Statement and PreparedStatement? | PreparedStatement is precompiled and prevents SQL injection. |

# 🚀 JDBC + TestNG Database Validation Framework

---

## 📂 **1\. Folder Structure (Maven Project)**

```typescript
📦 DatabaseValidationFramework
 ┣ 📂 src
 ┃ ┣ 📂 main
 ┃ ┃ ┗ 📂 java
 ┃ ┃    ┗ 📂 utils
 ┃ ┃       ┗ DBUtils.java
 ┃ ┗ 📂 test
 ┃    ┗ 📂 java
 ┃       ┗ tests
 ┃          ┗ DBValidationTest.java
 ┣ 📜 pom.xml
 ┗ 📜 testng.xml
```

---

## ⚙️ **2\. pom.xml Dependencies**

```typescript
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.dbtest</groupId>
  <artifactId>DatabaseValidationFramework</artifactId>
  <version>1.0</version>

  <dependencies>

    <!-- ✅ Selenium -->
    <dependency>
      <groupId>org.seleniumhq.selenium</groupId>
      <artifactId>selenium-java</artifactId>
      <version>4.25.0</version>
    </dependency>

    <!-- ✅ TestNG -->
    <dependency>
      <groupId>org.testng</groupId>
      <artifactId>testng</artifactId>
      <version>7.10.2</version>
      <scope>test</scope>
    </dependency>

    <!-- ✅ MySQL Connector -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.33</version>
    </dependency>

  </dependencies>
</project>
```

---

## 🧠 **3.** [**DBUtils.java**](http://DBUtils.java) **(Reusable Utility Class)**

```typescript
package utils;

import java.sql.*;

public class DBUtils {

    private static Connection con = null;
    private static Statement stmt = null;
    private static ResultSet rs = null;

    // Get connection
    public static Connection getConnection() throws Exception {
        if (con == null || con.isClosed()) {
            Class.forName("com.mysql.cj.jdbc.Driver");
            con = DriverManager.getConnection(
                    "jdbc:mysql://localhost:3306/appdb",
                    "root",
                    "password");
        }
        return con;
    }

    // Execute SELECT query
    public static ResultSet executeQuery(String query) throws Exception {
        stmt = getConnection().createStatement();
        rs = stmt.executeQuery(query);
        return rs;
    }

    // Execute UPDATE/DELETE/INSERT
    public static int executeUpdate(String query) throws Exception {
        stmt = getConnection().createStatement();
        int rows = stmt.executeUpdate(query);
        return rows;
    }

    // Close all connections
    public static void closeConnection() {
        try {
            if (rs != null) rs.close();
            if (stmt != null) stmt.close();
            if (con != null) con.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

## 🧪 **4.** [**DBValidationTest.java**](http://DBValidationTest.java) **(TestNG Test Case)**

This simulates:

* User submits data in UI (via Selenium)
    
* Data is validated in database using JDBC
    

```typescript
package tests;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.*;
import utils.DBUtils;

import java.sql.ResultSet;

public class DBValidationTest {

    WebDriver driver;

    @BeforeClass
    public void setup() {
        driver = new ChromeDriver();
        driver.manage().window().maximize();
    }

    @Test
    public void verifyUserRegistrationInDB() throws Exception {
        // Step 1: UI Action
        driver.get("https://example.com/register");
        driver.findElement(By.id("username")).sendKeys("John");
        driver.findElement(By.id("email")).sendKeys("john@test.com");
        driver.findElement(By.id("submit")).click();

        // Step 2: DB Validation
        String query = "SELECT * FROM users WHERE email='john@test.com'";
        ResultSet rs = DBUtils.executeQuery(query);

        // Step 3: Assertion
        Assert.assertTrue(rs.next(), "User not found in DB!");

        String username = rs.getString("username");
        Assert.assertEquals(username, "John", "Username mismatch in DB!");

        System.out.println("✅ User verified successfully in DB: " + username);
    }

    @AfterClass
    public void tearDown() {
        driver.quit();
        DBUtils.closeConnection();
    }
}
```

---

## ⚙️ **5\. testng.xml Configuration**

```typescript
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="DB Validation Suite">
  <test name="DatabaseValidationTest">
    <classes>
      <class name="tests.DBValidationTest" />
    </classes>
  </test>
</suite>
```

---

## 💡 **6\. Common Reusable Queries**

| Action | SQL Query Example |
| --- | --- |
| Select | `SELECT * FROM employee WHERE emp_id=1001;` |
| Insert | `INSERT INTO employee VALUES(1001, 'John', 'QA');` |
| Update | `UPDATE employee SET role='Tester' WHERE emp_id=1001;` |
| Delete | `DELETE FROM employee WHERE emp_id=1001;` |

---

## 🧩 **7\. Real-World Usage Scenarios**

| Scenario | Description |
| --- | --- |
| **UI → DB validation** | Validate if UI submission reflects correctly in DB |
| **API → DB validation** | Verify API POST creates correct record |
| **Data cleanup** | Delete old test data after suite |
| **Data-driven testing** | Fetch test data from DB dynamically |

---

## ⚡ **8\. Advantages for Automation Testers**

✅ Ensures **end-to-end validation (UI/API + DB)**  
✅ Improves test reliability  
✅ Detects backend issues early  
✅ Supports **data-driven testing**  
✅ Easy integration with **CI/CD pipelines (Jenkins)**

---

## 🧱 **9\. Interview Short Points**

| Question | Short Answer |
| --- | --- |
| What is JDBC? | Java API for connecting and querying databases. |
| Which JDBC classes are commonly used? | DriverManager, Connection, Statement, ResultSet. |
| Why use JDBC in automation? | To verify backend data consistency after UI/API operations. |
| Difference between Statement & PreparedStatement? | PreparedStatement is precompiled and prevents SQL injection. |
| How do you integrate JDBC with TestNG? | Write JDBC queries inside @Test methods and use assertions. |

---

## 🔧 **10\. Bonus: DBConfig in Properties File (Optional)**

👉 For better maintainability:  
`src/test/resources/`[`config.properties`](http://config.properties)

```typescript
db.url=jdbc:mysql://localhost:3306/appdb
db.username=root
db.password=password
```

Then load it in [`DBUtils.java`](http://DBUtils.java) using:

```typescript
Properties prop = new Properties();
prop.load(new FileInputStream("src/test/resources/config.properties"));
String url = prop.getProperty("db.url");
```

🔥 Perfect! You’re now stepping into **real enterprise-level automation** — combining  
**Database + Selenium + TestNG + Maven + Jenkins (CI/CD)** 🚀

Let’s build this step-by-step 👇

---

# 🌐 DATABASE-DRIVEN TESTING + JENKINS INTEGRATION FRAMEWORK

---

## 🧩 **1\. What is Database-Driven Testing?**

> Instead of hardcoding test data, you **fetch test data from the database** dynamically at runtime.

✅ Benefits for Automation Testers:

* No need to update test data in code.
    
* Tests use latest DB data.
    
* Helps when test data frequently changes.
    
* Useful for regression and CI/CD pipelines.
    

---

## 🧱 **2\. Folder Structure**

```typescript
📦 DatabaseDrivenAutomation
 ┣ 📂 src
 ┃ ┣ 📂 main/java/utils
 ┃ ┃ ┗ DBUtils.java
 ┃ ┗ 📂 test/java/tests
 ┃    ┗ DBDataDrivenTest.java
 ┣ 📜 pom.xml
 ┣ 📜 testng.xml
 ┗ 📜 config.properties
```

---

## ⚙️ **3\. config.properties**

```typescript
db.url=jdbc:mysql://localhost:3306/appdb
db.username=root
db.password=password
browser=chrome
baseUrl=https://example.com/register
```

---

## 🧰 **4\. Updated DBUtils.java (Dynamic Configurable Connection)**

```typescript
package utils;

import java.io.FileInputStream;
import java.sql.*;
import java.util.Properties;

public class DBUtils {
    private static Connection con = null;
    private static Statement stmt = null;

    public static Connection getConnection() throws Exception {
        if (con == null || con.isClosed()) {
            Properties prop = new Properties();
            prop.load(new FileInputStream("src/test/resources/config.properties"));

            String url = prop.getProperty("db.url");
            String user = prop.getProperty("db.username");
            String pass = prop.getProperty("db.password");

            Class.forName("com.mysql.cj.jdbc.Driver");
            con = DriverManager.getConnection(url, user, pass);
        }
        return con;
    }

    public static ResultSet executeQuery(String query) throws Exception {
        stmt = getConnection().createStatement();
        return stmt.executeQuery(query);
    }

    public static void closeConnection() {
        try {
            if (stmt != null) stmt.close();
            if (con != null) con.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

## 🧪 **5\. DBDataDrivenTest.java (Dynamic Data Fetching)**

This test **reads input data (username, email, password)** directly from database  
and executes UI automation for each record.

```typescript
package tests;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.*;
import utils.DBUtils;

import java.sql.ResultSet;
import java.util.ArrayList;
import java.util.List;

public class DBDataDrivenTest {

    WebDriver driver;

    @BeforeClass
    public void setup() {
        driver = new ChromeDriver();
        driver.manage().window().maximize();
    }

    @DataProvider(name = "UserData")
    public Object[][] getUserData() throws Exception {
        List<Object[]> data = new ArrayList<>();
        ResultSet rs = DBUtils.executeQuery("SELECT username, email, password FROM user_testdata");
        while (rs.next()) {
            data.add(new Object[]{
                    rs.getString("username"),
                    rs.getString("email"),
                    rs.getString("password")
            });
        }

        Object[][] result = new Object[data.size()][];
        for (int i = 0; i < data.size(); i++) {
            result[i] = data.get(i);
        }
        return result;
    }

    @Test(dataProvider = "UserData")
    public void verifyRegistration(String username, String email, String password) throws Exception {
        driver.get("https://example.com/register");

        driver.findElement(By.id("username")).sendKeys(username);
        driver.findElement(By.id("email")).sendKeys(email);
        driver.findElement(By.id("password")).sendKeys(password);
        driver.findElement(By.id("submit")).click();

        // Verify record in DB after submission
        String query = "SELECT * FROM users WHERE email='" + email + "'";
        ResultSet rs = DBUtils.executeQuery(query);

        Assert.assertTrue(rs.next(), "User record not found for " + email);
        Assert.assertEquals(rs.getString("username"), username);
        System.out.println("✅ Verified user registration for: " + username);
    }

    @AfterClass
    public void tearDown() {
        driver.quit();
        DBUtils.closeConnection();
    }
}
```

---

## 🧾 **6\. testng.xml**

```typescript
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="DatabaseDrivenSuite" parallel="false">
  <test name="DataDrivenTest">
    <classes>
      <class name="tests.DBDataDrivenTest"/>
    </classes>
  </test>
</suite>
```

---

## ⚙️ **7\. Example Database Table (user\_testdata)**

| username | email | password |
| --- | --- | --- |
| john | john@test.com | 1234 |
| anita | anita@test.com | 5678 |
| sam | sam@test.com | abcd |

Each record will trigger one test execution automatically ✅

---

## 🧩 **8\. Integrating with Maven**

### Command to Run:

```typescript
mvn clean test -DsuiteXmlFile=testng.xml
```

### Maven Surefire Plugin (Add in pom.xml)

```typescript
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>3.2.5</version>
      <configuration>
        <suiteXmlFiles>
          <suiteXmlFile>testng.xml</suiteXmlFile>
        </suiteXmlFiles>
      </configuration>
    </plugin>
  </plugins>
</build>
```

---

## 🔗 **9\. Jenkins Integration (CI/CD Pipeline)**

### Step 1️⃣ — Configure Jenkins Job

* Open Jenkins → **New Item → Maven Project**
    
* In **Source Code Management (SCM):**
    
    * Connect to your GitHub repository.
        
* In **Build Section:**
    
    * Command:
        
        ```typescript
        mvn clean test -DsuiteXmlFile=testng.xml
        ```
        

### Step 2️⃣ — Add DB Credentials in Jenkins

Use Jenkins **Credentials plugin**:

* Store DB username/password as secret credentials.
    
* Fetch them in code via environment variables or properties file.
    

### Step 3️⃣ — Post-Build Reporting

* Integrate with **Extent Reports / Allure Reports** for rich HTML reports.
    
* Jenkins will display test results + database validation outcomes.
    

---

## 📊 **10\. Real-World CI/CD Workflow**

| Stage | Action | Tool |
| --- | --- | --- |
| 🧱 Build | Clone repo + compile code | Maven |
| 🧪 Test | Run Selenium + JDBC validation | TestNG |
| 🧮 Validate | Check backend data correctness | JDBC |
| 📈 Report | Generate HTML reports | TestNG/Allure |
| 🚀 Deploy | Notify or trigger next job | Jenkins |

---

## 🧠 **11\. Best Practices**

✅ Keep database credentials encrypted or externalized.  
✅ Use **PreparedStatement** for security.  
✅ Use **Connection Pooling (HikariCP)** for large test suites.  
✅ Maintain test data lifecycle (setup/cleanup).  
✅ Integrate with CI/CD to run nightly DB validation tests.

---

## 📌 **12\. Interview Short Notes**

| Question | Answer |
| --- | --- |
| What is database-driven testing? | Fetch test data dynamically from DB for execution. |
| How do you integrate JDBC with Selenium? | Use DBUtils class + TestNG assertions after UI operations. |
| How do you run DB tests in CI/CD? | Via Jenkins pipeline using Maven + TestNG commands. |
| Why prefer JDBC over Excel for test data? | Data always up-to-date and supports multi-user access. |

💥 Awesome — now we’ll take your **Database + Selenium + TestNG framework** to the next professional level by adding **Extent Reports** for rich HTML dashboards (perfect for Jenkins CI/CD integration).

---

# 🎨 JDBC + Selenium + TestNG + Extent Reports Framework

You’ll get:  
✅ Real-time HTML report (with screenshots, SQL validation logs, pass/fail summary)  
✅ Jenkins-compatible reporting  
✅ Reusable DB utilities

---

## 🧩 **1\. Updated Project Structure**

```typescript
📦 DBValidationWithExtentReport
 ┣ 📂 src
 ┃ ┣ 📂 main/java/utils
 ┃ ┃ ┣ DBUtils.java
 ┃ ┃ ┗ ReportManager.java
 ┃ ┗ 📂 test/java/tests
 ┃    ┗ DBValidationReportTest.java
 ┣ 📂 test-output
 ┣ 📜 pom.xml
 ┣ 📜 testng.xml
 ┗ 📜 config.properties
```

---

## ⚙️ **2\. pom.xml Dependencies**

Add **Extent Reports** + others you already have 👇

```typescript
<dependencies>
    <!-- ✅ Selenium -->
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.25.0</version>
    </dependency>

    <!-- ✅ TestNG -->
    <dependency>
        <groupId>org.testng</groupId>
        <artifactId>testng</artifactId>
        <version>7.10.2</version>
        <scope>test</scope>
    </dependency>

    <!-- ✅ MySQL JDBC -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.33</version>
    </dependency>

    <!-- ✅ Extent Reports -->
    <dependency>
        <groupId>com.aventstack</groupId>
        <artifactId>extentreports</artifactId>
        <version>5.1.1</version>
    </dependency>

    <!-- ✅ WebDriverManager (for easy browser setup) -->
    <dependency>
        <groupId>io.github.bonigarcia</groupId>
        <artifactId>webdrivermanager</artifactId>
        <version>5.8.0</version>
    </dependency>
</dependencies>
```

---

## 🧰 **3.** [**DBUtils.java**](http://DBUtils.java) **(same as before)**

*(Keep your existing version — no change needed.)*

---

## 🧱 **4.** [**ReportManager.java**](http://ReportManager.java) **(Extent Setup Utility)**

```typescript
package utils;

import com.aventstack.extentreports.ExtentReports;
import com.aventstack.extentreports.reporter.ExtentSparkReporter;

public class ReportManager {

    private static ExtentReports extent;

    public static ExtentReports getReportInstance() {
        if (extent == null) {
            String reportPath = System.getProperty("user.dir") + "/test-output/ExtentReport.html";
            ExtentSparkReporter reporter = new ExtentSparkReporter(reportPath);
            reporter.config().setReportName("Database Validation Automation Report");
            reporter.config().setDocumentTitle("Automation Execution Report");

            extent = new ExtentReports();
            extent.attachReporter(reporter);
            extent.setSystemInfo("Tester", "Shreenibas Samal");
            extent.setSystemInfo("Environment", "QA");
        }
        return extent;
    }
}
```

---

## 🧪 **5.** [**DBValidationReportTest.java**](http://DBValidationReportTest.java)

Combines Selenium + JDBC + Extent Report in a real-world test flow.

```typescript
package tests;

import com.aventstack.extentreports.*;
import io.github.bonigarcia.wdm.WebDriverManager;
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.*;
import utils.DBUtils;
import utils.ReportManager;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.sql.ResultSet;

public class DBValidationReportTest {

    WebDriver driver;
    ExtentReports extent;
    ExtentTest test;

    @BeforeSuite
    public void startReport() {
        extent = ReportManager.getReportInstance();
    }

    @BeforeClass
    public void setup() {
        WebDriverManager.chromedriver().setup();
        driver = new ChromeDriver();
        driver.manage().window().maximize();
    }

    @Test
    public void verifyUserRegistrationInDB() throws Exception {
        test = extent.createTest("Verify User Registration in DB");

        driver.get("https://example.com/register");
        test.info("Opened registration page");

        driver.findElement(By.id("username")).sendKeys("John");
        driver.findElement(By.id("email")).sendKeys("john@test.com");
        driver.findElement(By.id("submit")).click();
        test.pass("User form submitted successfully");

        String query = "SELECT * FROM users WHERE email='john@test.com'";
        ResultSet rs = DBUtils.executeQuery(query);

        if (rs.next()) {
            String dbName = rs.getString("username");
            Assert.assertEquals(dbName, "John");
            test.pass("✅ DB record verified: Username = " + dbName);
        } else {
            test.fail("❌ User not found in database!");
            takeScreenshot("user_not_found");
            Assert.fail("User not found in DB!");
        }
    }

    public void takeScreenshot(String name) throws IOException {
        File src = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
        String path = System.getProperty("user.dir") + "/test-output/screenshots/" + name + ".png";
        Files.createDirectories(new File(System.getProperty("user.dir") + "/test-output/screenshots/").toPath());
        Files.copy(src.toPath(), new File(path).toPath());
        test.addScreenCaptureFromPath(path);
    }

    @AfterClass
    public void tearDown() {
        driver.quit();
        DBUtils.closeConnection();
    }

    @AfterSuite
    public void endReport() {
        extent.flush();
    }
}
```

---

## 🧾 **6\. testng.xml**

```typescript
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="DB Validation with Extent Report Suite">
  <test name="DBValidationTest">
    <classes>
      <class name="tests.DBValidationReportTest" />
    </classes>
  </test>
</suite>
```

---

## 📊 **7\. How the Report Looks**

When you run the suite:

```typescript
mvn clean test
```

✅ Report generated here:

```typescript
test-output/ExtentReport.html
```

Report includes:

* Test name
    
* Step logs (info/pass/fail)
    
* Screenshots (for failures)
    
* Environment details
    
* Execution summary
    

---

## 🔗 **8\. Jenkins Integration Steps**

1️⃣ **Create a Maven Job**

* SCM → GitHub Repository
    
* Build command:
    
    ```typescript
    mvn clean test -DsuiteXmlFile=testng.xml
    ```
    

2️⃣ **Publish HTML Report in Jenkins**

* In Jenkins Job → Post-build actions
    
* Add **“Publish HTML reports”**
    
    * HTML directory: `test-output`
        
    * Index page: `ExtentReport.html`
        
    * Report title: `Database Validation Results`
        

3️⃣ **Trigger on Each Commit / Nightly Build**

* Use **GitHub Webhooks** or **Jenkins scheduler** (e.g., every night 2 AM).
    

---

## 💡 **9\. Bonus: Integrating Extent Report + TestNG Listeners**

For large projects, use a `TestListener` to automatically log results into Extent Reports (no need to write logs in every test).

---

## ⚙️ **10\. Real-World CI/CD Flow**

| Stage | Tool | Action |
| --- | --- | --- |
| Source | GitHub | Code checkout |
| Build | Maven | Compile + run TestNG |
| Test | Selenium + JDBC | Validate UI & DB |
| Report | Extent | Generate HTML report |
| CI | Jenkins | Execute and publish report |
| Notification | Email/Slack | Send test summary |

---

## 🧠 **11\. Interview Highlights**

| Question | Answer |
| --- | --- |
| What is Extent Report? | A customizable HTML reporting library for automation. |
| Why use it in Jenkins? | To publish detailed visual reports of test execution. |
| How do you attach screenshots? | Use `test.addScreenCaptureFromPath(path)` in Extent. |
| What’s your CI/CD setup? | Jenkins + Maven + TestNG + Extent Reports for nightly regression. |

---

## 🎯 **Next Step (Optional but Recommended)**

Would you like me to extend this setup with **Allure Reports** integration (for modern, analytics-style dashboards with graphs and step logs inside Jenkins)?  
Allure is used in 80%+ enterprise QA pipelines now.