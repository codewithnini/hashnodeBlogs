---
title: "Jenkins For Automation Tester"
datePublished: Mon Sep 29 2025 06:41:54 GMT+0000 (Coordinated Universal Time)
cuid: cmg4rgkde000s02k35r2ghuwe
slug: jenkins-for-automation-tester
tags: codewithnini

---

# ⚙️ **Jenkins Overview**

## 1️⃣ What is Jenkins?

👉 Jenkins is an **open-source automation server** used to implement **Continuous Integration (CI)** and **Continuous Delivery/Deployment (CD)**.  
It automates:

* Building projects
    
* Running tests
    
* Deploying applications
    

So instead of manually running builds/tests/deployments, Jenkins automates everything.

---

## 2️⃣ Why Jenkins came?

Before Jenkins (early 2000s), developers:

* Built projects manually → time-consuming & error-prone.
    
* Integrated code once in a while ("integration hell").
    
* Deployment was manual, risky, and slow.
    

👉 Jenkins solved these by **automating CI/CD pipelines** → code is integrated, tested, and deployed automatically.

---

## 3️⃣ When Jenkins came?

* Jenkins was created in **2004** by **Kohsuke Kawaguchi** at Sun Microsystems.
    
* Initially called **Hudson**, renamed to **Jenkins** in **2011** (after Oracle dispute).
    

---

## 4️⃣ What problem does Jenkins solve?

* **Automation** → no manual builds/tests/deploys.
    
* **Faster feedback** → catch bugs early with CI.
    
* **Scalability** → master-agent setup for distributed builds.
    
* **Consistency** → same process across all environments.
    
* **Integration** → works with Git, Maven, Selenium, Docker, Kubernetes, etc.
    

👉 In short: Jenkins automates **software delivery pipeline** end-to-end.

---

## 5️⃣ Where can we use Jenkins?

* **Automation Testing** → run Selenium/TestNG/JUnit tests.
    
* **DevOps CI/CD** → build → test → deploy pipelines.
    
* **Infrastructure as Code** → integrate with Docker, Kubernetes, Terraform.
    
* **Monitoring** → send reports via Email/Slack.
    
* **Enterprise Projects** → distributed build and deployment pipelines.
    

---

## 6️⃣ When do we use Jenkins?

* When you want **continuous integration** → automatically test code after each commit.
    
* When you want **continuous delivery/deployment** → automatically deploy after successful tests.
    
* When working with **teams** → so every developer’s code gets integrated and tested daily.
    

---

## 7️⃣ Prerequisite Knowledge for Jenkins

Before learning Jenkins, you should know:

1. **Core Java** (for Selenium/TestNG projects).
    
2. **Maven/Gradle** (build tools Jenkins integrates with).
    
3. **Git/GitHub** (source code management).
    
4. **Basic Linux/Windows commands**.
    
5. **Automation Testing (Selenium/TestNG/JUnit)**.
    
6. (Optional) **Docker, Kubernetes, Cloud (AWS/Azure/GCP)** if you want to learn DevOps CI/CD.
    

---

✅ So in summary:

* **Maven** automates builds & dependency management.
    
* **Jenkins** automates the entire CI/CD pipeline (build → test → deploy).
    

Perfect 👍 Let’s break down **Jenkins components** in detail with their roles.

---

# 🧩 **Jenkins Components & Their Work**

---

## 1️⃣ **Jenkins Server (Master/Controller)**

* The **core of Jenkins**.
    
* Provides the **web UI** ([`http://localhost:8080`](http://localhost:8080)).
    
* Stores configuration, jobs, plugins.
    
* Assigns work to agents (slaves).
    
* Monitors builds and shows results.
    

👉 Think of it as the **brain of Jenkins**.

---

## 2️⃣ **Jenkins Nodes (Agents/Slaves)**

* Machines that **execute the jobs** assigned by the Master.
    
* Can be physical servers, VMs, or cloud instances.
    
* Each node has labels (e.g., *Windows*, *Linux*, *Docker*) so jobs can run in the right environment.
    

👉 Master tells agents *what to do*, agents actually **do the work**.

---

## 3️⃣ **Jenkins Jobs / Projects**

* A **job** is a task Jenkins performs (e.g., build, test, deploy).
    
* Types:
    
    * **Freestyle Project** → simple jobs with manual config.
        
    * **Maven Project** → integrates with Maven lifecycle.
        
    * **Pipeline Project** → scripted with `Jenkinsfile`.
        
    * **Multibranch Pipeline** → CI/CD for multiple Git branches.
        

👉 Jobs are the **heart of Jenkins automation**.

---

## 4️⃣ **Jenkins Pipelines**

* A way to define the CI/CD workflow as **code (Jenkinsfile)**.
    
* Two types:
    
    * **Declarative Pipeline** → simpler, structured.
        
    * **Scripted Pipeline** → full flexibility with Groovy scripting.
        
* Consists of **Stages** (`Build`, `Test`, `Deploy`) and **Steps** (commands inside stages).
    

👉 Pipelines = **Automation as Code**.

---

## 5️⃣ **Jenkins Plugins**

* Jenkins is lightweight by default.
    
* Plugins extend functionality:
    
    * Git plugin → SCM
        
    * Maven plugin → build automation
        
    * JUnit/TestNG plugin → test reports
        
    * Email/Slack plugin → notifications
        
    * Allure/Extent → test reporting
        
    * Docker/Kubernetes → DevOps integration
        

👉 Over **1800+ plugins** available.

---

## 6️⃣ **Jenkins Workspace**

* A **directory on the agent machine** where Jenkins checks out the project code and runs builds.
    
* Example:
    
    ```xml
    /var/lib/jenkins/workspace/MyProject/
    ```
    
* Contains source code, compiled classes, reports, and logs.
    

👉 Each job has its **own workspace**.

---

## 7️⃣ **Jenkins Build Triggers**

* Defines *when* a job runs:
    
    * **Manual Trigger** → click "Build Now".
        
    * **Poll SCM** → check Git repo every X minutes.
        
    * **Webhooks** → trigger instantly when code is pushed.
        
    * **Scheduled (Cron)** → e.g., nightly builds.
        
    * **Upstream/Downstream** → trigger job chains.
        

👉 Triggers = **automation entry point**.

---

## 8️⃣ **Jenkins Build Executors**

* Executors are **slots on an agent** that run jobs in parallel.
    
* Example:
    
    * 1 agent with 2 executors → can run 2 builds at the same time.
        

👉 Executors = **multi-tasking power of Jenkins**.

---

## 9️⃣ **Jenkins Artifacts**

* The **output** of a Jenkins job (e.g., JAR, WAR, ZIP, reports).
    
* Stored in `workspace/target` and can be **archived** in Jenkins.
    
* Used for deployments.
    

👉 Artifacts = **deliverables**.

---

## 🔟 **Jenkins Console Output (Logs)**

* Shows **step-by-step execution logs** of a job.
    
* Useful for debugging build/test failures.
    

👉 Think of it as Jenkins’ **black box recorder**.

---

## 1️⃣1️⃣ **Jenkins Security & Credentials**

* Manages **user authentication & authorization**.
    
* Stores **secrets** (API keys, passwords, SSH keys) securely.
    
* Credentials are injected into jobs when required.
    

👉 Ensures builds are **safe & secure**.

---

## 1️⃣2️⃣ **Jenkins Shared Libraries**

* Custom reusable Groovy code for pipelines.
    
* Helps maintain **DRY principle** (Don’t Repeat Yourself).
    

👉 Useful for **enterprise-level pipelines**.

---

# 🎯 Summary (One-liner for each component)

* **Server (Master/Controller)** → Brains of Jenkins.
    
* **Nodes (Agents/Slaves)** → Workers that execute jobs.
    
* **Jobs/Projects** → The actual tasks.
    
* **Pipelines** → Workflow as code.
    
* **Plugins** → Extend Jenkins features.
    
* **Workspace** → Directory for build execution.
    
* **Triggers** → When jobs run.
    
* **Executors** → Parallel job slots.
    
* **Artifacts** → Build outputs.
    
* **Console Output** → Logs.
    
* **Security & Credentials** → Safe access.
    
* **Shared Libraries** → Reusable pipeline code.
    

# **Scheduled Builds (Cron) in Jenkins – Detailed Explanation**

---

## **1️⃣ What is Scheduled Build in Jenkins?**

* A **scheduled build** is when Jenkins automatically triggers a job **at specific time intervals** without any manual action or SCM push.
    
* Useful for:
    
    * Nightly regression runs
        
    * Smoke tests every morning
        
    * Weekly full test suites
        
    * Periodic API or UI automation execution
        
* In Jenkins, this is done using **Cron syntax** in the **Build Triggers → “Build periodically”** section.
    

---

## **2️⃣ Cron Syntax in Jenkins**

Cron in Jenkins uses **five fields**:

```java
MIN HOUR DOM MON DOW
```

| Field | Meaning | Allowed Values |
| --- | --- | --- |
| MIN | Minute | 0-59 |
| HOUR | Hour | 0-23 |
| DOM | Day of Month | 1-31 |
| MON | Month | 1-12 or JAN-DEC |
| DOW | Day of Week | 0-7 (0 or 7 = Sunday) or SUN-SAT |

**Special characters:**

* `*` → every value
    
* `,` → multiple values
    
* `-` → range
    
* `/` → increments
    

---

## **3️⃣ Common Examples for Test Automation**

| Cron Expression | Meaning | Use Case |
| --- | --- | --- |
| `H 2 * * *` | Build daily at 2 AM | Nightly regression suite |
| `H/15 * * * *` | Every 15 minutes | Poll for small automation triggers |
| `0 0 * * 0` | Every Sunday at midnight | Weekly full regression |
| `0 9-17 * * 1-5` | Every hour between 9 AM–5 PM on weekdays | Business hours smoke test |
| `H 0 * * *` | Daily at midnight | Daily automated API/UI tests |

**Note:** `H` is used in Jenkins to **spread load evenly** across multiple jobs (instead of all jobs running at exact same minute).

---

## **4️⃣ How to Schedule a Maven + Selenium Job**

### Step 1: Create Jenkins Job

* Job type: Freestyle / Maven / Pipeline
    

### Step 2: Configure Build Trigger

* **Build periodically** → tick the checkbox
    
* Enter Cron expression:
    

```java
H 2 * * *   # Run daily at 2 AM
```

### Step 3: Configure Build Steps

* For Maven Project:
    

```java
mvn clean test -DsuiteXmlFile=testng.xml
```

* For Pipeline Job:
    

```java
triggers {
    cron('H 2 * * *')
}
```

### Step 4: Post-build Actions

* Archive artifacts: `target/*.html, target/screenshots/*`
    
* Publish ExtentReports / TestNG reports
    
* Send email / Slack notifications
    

---

## **5️⃣ Practical Example – Nightly Regression Pipeline**

**Jenkinsfile Example (Declarative Pipeline):**

```java
pipeline {
    agent any
    triggers {
        cron('H 1 * * *')  // Daily at 1 AM
    }
    stages {
        stage('Checkout') {
            steps { git 'https://github.com/user/automation-tests.git' }
        }
        stage('Build') {
            steps { sh 'mvn clean install' }
        }
        stage('Test') {
            steps { sh 'mvn test -DsuiteXmlFile=testng.xml' }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.html, **/target/screenshots/*', allowEmptyArchive: true
        }
        success {
            mail to: 'qa@company.com', subject: 'Nightly Build Passed', body: 'Check Jenkins report'
        }
        failure {
            mail to: 'qa@company.com', subject: 'Nightly Build Failed', body: 'Check Jenkins report'
        }
    }
}
```

**What happens:**

1. Jenkins triggers build automatically at 1 AM daily.
    
2. Pulls latest code from Git.
    
3. Runs Maven build & Selenium scripts.
    
4. Archives reports & screenshots.
    
5. Sends email notifications with results.
    

---

## **6️⃣ Best Practices for Scheduled Builds**

1. **Use** `H` instead of fixed minutes
    
    * Prevents **server overload** when multiple jobs run at the same time.
        
2. **Use Multibranch Pipelines** for multiple branches
    
    * Each feature branch can have its own schedule if needed.
        
3. **Separate Nightly and Daily Jobs**
    
    * Nightly: full regression suite
        
    * Daily: smoke test for quick validation
        
4. **Archive Artifacts**
    
    * Always keep HTML reports and screenshots for debugging
        
5. **Notify Team on Failure**
    
    * Email / Slack / Teams notifications
        
6. **Monitor Build Stability**
    
    * Avoid long-running nightly tests blocking other jobs
        
    * Use parallel execution if possible
        

---

## **7️⃣ Key Points for Automation Testers**

* Scheduled builds = automation running **without manual triggers**
    
* Use **cron expressions** in Jenkins for timing
    
* Integrates seamlessly with **Maven/Selenium/TestNG/ExtentReports**
    
* Helps ensure **regression suites run nightly** and results are shared
    
* Critical for catching **bugs early in CI/CD**
    

Perfect! Here’s a **ready-to-use Cron Schedule Table for Jenkins**, designed specifically for **automation testers**. You can directly copy these into your Jenkins job under **“Build periodically”** or pipeline triggers.

---

# **Jenkins Cron Schedule Table – Automation Testers**

| Frequency | Cron Expression | Description / Use Case |
| --- | --- | --- |
| **Every 15 minutes** | `H/15 * * * *` | Poll GitHub/SCM for new commits and run quick smoke tests |
| **Every hour** | `H * * * *` | Hourly validation of automation scripts or API checks |
| **Daily at 12 AM** | `H 0 * * *` | Run **full regression suite** every night |
| **Daily at 1 AM** | `H 1 * * *` | Nightly Selenium + TestNG + ExtentReports build |
| **Daily at 2 AM** | `H 2 * * *` | Nightly API + UI automation combined build |
| **Every weekday at 9 AM** | `H 9 * * 1-5` | Morning smoke test for QA team review |
| **Every Sunday at 12 AM** | `0 0 * * 0` | Weekly full regression build |
| **Every 1st day of the month** | `H H 1 * *` | Monthly release automation validation |
| **Every 10 minutes** | `H/10 * * * *` | Quick sanity checks on critical features |
| **Business hours every hour (9 AM – 5 PM)** | `0 9-17 * * 1-5` | Hourly smoke tests during working hours |

---

## **How to Use in Jenkins Jobs**

### **Freestyle / Maven Job**

1. Go to **Configure → Build Triggers → Build periodically**
    
2. Paste cron expression (example: `H 1 * * *`)
    
3. Save job → Jenkins will automatically schedule builds
    

### **Pipeline Job**

```java
pipeline {
    agent any
    triggers {
        cron('H 1 * * *') // nightly at 1 AM
    }
    stages {
        stage('Checkout') { steps { git 'https://github.com/user/automation.git' } }
        stage('Build & Test') { steps { sh 'mvn clean test' } }
    }
    post {
        always { archiveArtifacts artifacts: '**/target/*.html', allowEmptyArchive: true }
        failure { mail to: 'qa@company.com', subject: 'Nightly Build Failed', body: 'Check Jenkins report' }
    }
}
```

---

## **Tips for Automation Testers**

1. **Use** `H` (hash) instead of fixed minutes → balances load across jobs.
    
2. **Nightly builds** → full regression suite.
    
3. **Daily builds** → smoke tests for early detection of failures.
    
4. **Weekly / monthly builds** → long-running or release validations.
    
5. Combine with **multibranch pipelines** → each branch can have its own schedule.