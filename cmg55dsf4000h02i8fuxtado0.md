---
title: "Basics Before Learning Web Automation Testing"
datePublished: Mon Sep 29 2025 13:11:39 GMT+0000 (Coordinated Universal Time)
cuid: cmg55dsf4000h02i8fuxtado0
slug: basics-before-learning-web-automation-testing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1759151977945/da843099-0d42-440e-b651-50188601e8ff.png
tags: codewithnini

---

## **What is software?**

• A Software is a collection of computer programs that helps us to perform a task.

**• Types of Software:**

• **System software** Ex: Device drivers, OS, Servers, Utilities, etc.

• **Programming software** Ex: compilers, debuggers, interpreters, etc.

• **Application software** Ex: industrial automation, business software, games, telecoms, etc.

## 1️⃣ Types of **Software Applications**

### A. Based on Platform

1. **Desktop Applications**
    
    * Installed and run locally on a PC/laptop.
        
    * Example: MS Word, Photoshop, VLC Media Player.
        
    * ✅ Why? Because they don’t require internet (except for updates), and execution happens on the user’s machine.
        
2. **Web Applications**
    
    * Accessed through a browser (Chrome, Firefox, Edge).
        
    * Hosted on a server, not installed locally.
        
    * Example: Gmail, Facebook, Amazon, Jira.
        
    * ✅ Why? Because all business logic runs on a server, and the client (browser) just sends requests & shows responses.
        
3. **Mobile Applications**
    
    * Installed on mobile devices (iOS/Android).
        
    * Example: WhatsApp, Uber, Instagram.
        
    * ✅ Why? Designed for mobile OS with touch, push notifications, GPS, etc.
        
4. **Hybrid Applications**
    
    * Combination of web + mobile (single codebase runs on multiple platforms).
        
    * Example: Twitter app, Uber app.
        
    * ✅ Why? Built using web technologies (HTML, CSS, JS) but wrapped for mobile devices.
        

---

### B. Based on Functionality

1. **System Software**
    
    * Manages hardware & system resources.
        
    * Example: Windows OS, Linux, Drivers.
        
    * ✅ Why? Because it supports and runs other applications.
        
2. **Application Software**
    
    * Helps users perform tasks.
        
    * Example: MS Office, Photoshop.
        
    * ✅ Why? Directly used by end-users for productivity.
        
3. **Utility Software**
    
    * Provides supporting tools.
        
    * Example: Antivirus, File Compression tools.
        
    * ✅ Why? Assists system/application software with maintenance.
        

---

## 2️⃣ Types of **Web Applications**

Web apps themselves can be categorized further:

1. **Static Web Applications**
    
    * Only display content, no interaction.
        
    * Example: Simple portfolio website, company info page.
        
    * ✅ Why? HTML/CSS only, no DB or backend logic.
        
2. **Dynamic Web Applications**
    
    * Interactive, connected with database.
        
    * Example: Facebook, Twitter.
        
    * ✅ Why? Data changes dynamically based on user input.
        
3. **E-commerce Applications**
    
    * Online shopping systems.
        
    * Example: Amazon, Flipkart.
        
    * ✅ Why? Because they involve product catalog, payment gateway, cart system.
        
4. **Content Management Systems (CMS)**
    
    * Allow non-technical users to manage content.
        
    * Example: WordPress, Joomla.
        
    * ✅ Why? Designed to handle blogs, websites easily.
        
5. **Portal Web Applications**
    
    * Provide information in a categorized way.
        
    * Example: University student portal, Job portal.
        
    * ✅ Why? Because they serve role-based access to multiple modules.
        
6. **Single Page Applications (SPA)**
    
    * Works like a mobile app, loads once, then updates dynamically.
        
    * Example: Gmail, Trello.
        
    * ✅ Why? Built using Angular, React, Vue; fast and smooth UX.
        
7. **Progressive Web Apps (PWA)**
    
    * Web apps that behave like mobile apps (offline support, push notifications).
        
    * Example: Twitter Lite, Starbucks PWA.
        
    * ✅ Why? They combine best of web and mobile.
        

---

✅ **In short**:

* **Desktop App** → Runs on PC/laptop.
    
* **Web App** → Runs on browser (client-server model).
    
* **Mobile App** → Runs on smartphone OS.
    
* **Hybrid App** → Same app works on multiple platforms.
    
* **Web Types** → Static, Dynamic, E-commerce, CMS, Portal, SPA, PWA.
    

## ✅ How to Test Different Types of Software Applications

## 1️⃣ Desktop Applications

* **What it is**: Installed on PC, runs on OS (e.g., MS Word, Photoshop).
    
* **How to Test**:
    
    * 🖥️ **Installation Testing** → Does the app install/uninstall correctly?
        
    * 🔑 **Functional Testing** → Verify features (open, save, edit, print).
        
    * 🧪 **Regression Testing** → After updates, old features still work.
        
    * ⚡ **Performance Testing** → App launch time, memory usage, CPU load.
        
    * 🔒 **Security Testing** → Check data storage, encryption, license validation.
        
    * 🌍 **Compatibility Testing** → Runs properly on different OS (Windows 10/11, Linux, Mac).
        

---

## 2️⃣ Web Applications

* **What it is**: Runs on a browser, hosted on a server (e.g., Gmail, Facebook).
    
* **How to Test**:
    
    * 🌐 **Functional Testing** → Verify forms, login, navigation, CRUD operations.
        
    * 🖱️ **UI/UX Testing** → Layout, alignment, responsiveness on different screen sizes.
        
    * 🧭 **Cross-Browser Testing** → Chrome, Firefox, Edge, Safari.
        
    * 📶 **Performance Testing** → Page load speed, stress test with multiple users.
        
    * 🔒 **Security Testing** → SQL Injection, XSS, CSRF, authentication.
        
    * 📱 **Responsive Testing** → Mobile vs desktop view (using tools like BrowserStack).
        
    * 🔗 **API Testing** (if backend services exist).
        

---

## 3️⃣ Mobile Applications

* **What it is**: Native apps on Android/iOS (e.g., WhatsApp, Uber).
    
* **How to Test**:
    
    * 📱 **Installation & Launch Testing** → APK/IPA install, permissions.
        
    * ✋ **Functional Testing** → Call, message, GPS, push notifications.
        
    * 📶 **Network Testing** → Behavior on Wi-Fi, 3G/4G/5G, airplane mode.
        
    * 📏 **UI/UX Testing** → Different screen sizes & resolutions.
        
    * ⚡ **Performance Testing** → Battery usage, app startup speed, crash recovery.
        
    * 🔒 **Security Testing** → Data encryption, secure login, app permissions.
        
    * 🌍 **Compatibility Testing** → Different devices, OS versions (Android 12 vs 14, iOS 16 vs 17).
        

---

## 4️⃣ Hybrid Applications (Web + Mobile)

* **What it is**: Built with web tech (React Native, Flutter) but runs as mobile apps.
    
* **How to Test**:
    
    * Combination of **Web Testing** + **Mobile Testing**.
        
    * Check offline functionality (PWA mode).
        
    * Validate performance compared to native apps.
        

---

# ✅ Web Application Types Testing

| **Web App Type** | **How to Test** |
| --- | --- |
| **Static Website** | Check content, links, responsiveness, SEO tags. |
| **Dynamic Website** | Functional + DB validation (content updates dynamically). |
| **E-commerce** | Cart, checkout, payment gateway, discounts, refund flow. |
| **CMS** | Content publishing, role-based access, plugin compatibility. |
| **Portal** | Role-specific access, authentication, personalized dashboards. |
| **SPA (Single Page App)** | Navigation without reload, API calls, browser history handling. |
| **PWA (Progressive Web App)** | Offline support, add-to-home-screen, push notifications. |

---

## ✅ Test Strategy by Type

* ### **Desktop** → Focus on **installation, OS compatibility, performance**.
    
* **Web** → Focus on **browser compatibility, UI/UX, security**.
    
* **Mobile** → Focus on **network, device compatibility, battery**.
    
* **Hybrid** → Focus on **cross-platform consistency**.
    

---

👍 let’s build **real-time example test cases** for each type (Desktop, Web, Mobile).

# ✅ Real-Time Example Test Cases

## 1️⃣ Desktop Application – **MS Word (Desktop App Example)**

| **TC ID** | **Scenario** | **Steps** | **Expected Result** |
| --- | --- | --- | --- |
| D-001 | Verify application installation | Run MS Word installer and complete setup | MS Word should be installed successfully |
| D-002 | Verify opening a new document | Open MS Word → File → New | A blank new document should appear |
| D-003 | Verify saving a document | Type some text → Save As → choose path → Save | File should be saved at given location |
| D-004 | Verify compatibility with different OS | Install on Windows 10 & 11 | MS Word should run smoothly on all supported OS |
| D-005 | Verify application performance | Open large 200-page file | File should open without crashing |

---

## 2️⃣ Web Application – **Login Page of Gmail (Web App Example)**

| **TC ID** | **Scenario** | **Steps** | **Expected Result** |
| --- | --- | --- | --- |
| W-001 | Verify login with valid credentials | Go to [gmail.com](http://gmail.com) → enter valid email & password → click login | User should land on inbox page |
| W-002 | Verify login with invalid password | Enter valid email but wrong password | Error message: *"Wrong password. Try again"* |
| W-003 | Verify cross-browser support | Open Gmail in Chrome, Firefox, Edge, Safari | Gmail should work consistently |
| W-004 | Verify responsiveness | Open Gmail on desktop, tablet, mobile browser | Layout should adjust automatically |
| W-005 | Verify security | Try SQL injection in username field | System should not allow login & display error |

---

## 3️⃣ Mobile Application – **WhatsApp (Mobile App Example)**

| **TC ID** | **Scenario** | **Steps** | **Expected Result** |
| --- | --- | --- | --- |
| M-001 | Verify installation on Android | Download WhatsApp from Play Store & install | App should install successfully |
| M-002 | Verify first-time login | Enter phone number → receive OTP → enter OTP | User should be logged in and profile setup should open |
| M-003 | Verify sending a message | Open chat → type text → send | Message should be delivered with ✔ |
| M-004 | Verify behavior in airplane mode | Turn on airplane mode → try sending message | Message should not send; show “Clock icon” pending state |
| M-005 | Verify battery consumption | Use WhatsApp for 1 hour with video call | Battery consumption should be within acceptable range (not drain abnormally) |

---

### 📌 Key Takeaway

* **Desktop Testing** → Focus on installation, OS compatibility, file handling, performance.
    
* **Web Testing** → Focus on login, forms, browser compatibility, security.
    
* **Mobile Testing** → Focus on installation, network (Wi-Fi, 4G, airplane mode), battery usage.
    

---

# 👉 Do you think when to test, see below.

When we develop software, we don’t just “start coding.” We follow a **structured process** called the **Software Development Life Cycle (SDLC)**.

This ensures the software is **high quality, meets user needs, delivered on time, and within budget**.

---

# ✅ Software Development Procedures (SDLC)

## 1️⃣ **Requirement Gathering & Analysis**

* **Goal**: Understand what the client/user wants.
    
* **Activities**:
    
    * Meet stakeholders, collect business needs.
        
    * Document Functional (what system should do) & Non-functional requirements (performance, security, scalability).
        
    * Create Requirement Specification Document (SRS).
        
* **Example**: For a Login page → username, password, forgot password, remember me.
    

---

## 2️⃣ **Feasibility Study / Planning**

* **Goal**: Check if project is doable (cost, technology, time).
    
* **Activities**:
    
    * Technical feasibility (Do we have the tech?).
        
    * Financial feasibility (Is budget enough?).
        
    * Resource feasibility (Do we have team members?).
        
    * Risk analysis.
        
* **Deliverable**: Project Plan, Risk Plan.
    

---

## 3️⃣ **System Design**

* **Goal**: Create a blueprint of the software.
    
* **Activities**:
    
    * High-Level Design (HLD): Architecture, modules, DB design.
        
    * Low-Level Design (LLD): Detailed logic of each module, class diagrams.
        
    * UI/UX design (wireframes, mockups).
        
* **Example**: Login Page wireframe, DB schema with Users table.
    

---

## 4️⃣ **Development (Coding)**

* **Goal**: Build the actual software.
    
* **Activities**:
    
    * Developers write code in chosen language (Java, Python, etc.).
        
    * Follow coding standards (naming, documentation, version control with Git).
        
    * Unit testing by developers.
        
* **Deliverable**: Working application build.
    

---

## 5️⃣ **Testing**

* **Goal**: Verify the software works as expected & is bug-free.
    
* **Activities**:
    
    * Test Types: Functional, Regression, Integration, Performance, Security.
        
    * Manual + Automation testing (Selenium, JUnit, TestNG, Appium, etc.).
        
    * Bug reporting & tracking (Jira, Bugzilla).
        
* **Deliverable**: Tested software, Test Report, Defect Logs.
    

---

## 6️⃣ **Deployment**

* **Goal**: Release software to users.
    
* **Activities**:
    
    * Deploy to **staging** environment → final testing (UAT).
        
    * Deploy to **production** environment → live use.
        
    * CI/CD pipelines (Jenkins, GitHub Actions).
        
* **Deliverable**: Software available to end users.
    

---

## 7️⃣ **Maintenance & Support**

* **Goal**: Keep the software running smoothly.
    
* **Activities**:
    
    * Fix bugs after release.
        
    * Provide updates (new features, performance improvements).
        
    * Monitor system performance & security.
        
* **Deliverable**: Stable, updated software.
    

---

## ✅ Popular SDLC Models

Different companies follow different **models** of SDLC:

* **Waterfall** → Sequential steps (best for small projects).
    
* **Agile** → Iterative, flexible, continuous feedback (most popular today).
    
* **Scrum** → Agile framework with sprints (2-4 weeks).
    
* **V-Model** → Testing activities mapped to each development stage.
    
* **Spiral Model** → Focuses on risk analysis.
    

---

📌 **In short**:  
**Steps to develop software** = Requirement → Feasibility → Design → Development → Testing → Deployment → Maintenance.

## As we Know Testing is Done In SDLC process .

## &

## What is Software Testing?

• Software Testing is a part of software development process.

• Software Testing is an activity to detect and identify the defects in the software.

• The objective of testing is to release quality product to the client.

As we know Testing the functionallity of an application according to **CRS (Customer Requirement Specification)** is called **Software Testing**.

**Software Testing can be done by two way.**

1. Manual Testing
    
2. Automation Testing
    

## **👉 NOTE: Here i explain about Web-Automation Only , not others.**

## Types of Testing in Web Automation.

### Classification of Different Types of Testing

**Testing is divided into two types –**

* **Functional Testing**
    
* **Non Functional** **Testing**
    
* ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733984424558/0ce4f51b-e5ae-4c8d-bb8f-6e366ea80ca1.jpeg align="center")
    

## ✅ Software Testing Types

| **Testing Type** | **Definition (Short)** | **Example** |
| --- | --- | --- |
| **Unit Testing** | Test smallest piece of code (function/class). | Test login() method returns correct status. |
| **Integration Testing** | Test interaction between modules. | Check login module works with DB. |
| **System Testing** | Test complete application end-to-end. | Verify full e-commerce workflow (login → cart → payment). |
| **Sanity Testing** | Quick check of specific functionality. | After bug fix, check only “Forgot Password.” |
| **Smoke Testing** | Initial check if build is stable. | Verify app opens and login works. |
| **Regression Testing** | Ensure old features work after new changes. | After adding “Remember Me,” verify login/logout still works. |
| **Functional Testing** | Verify software functions as per requirements. | Verify login accepts valid credentials only. |
| **Non-Functional Testing** | Test performance, security, usability. | Check website loads under 2 sec. |
| **Acceptance Testing (UAT)** | Validate app with client/business requirements. | Client verifies payroll system calculates salary correctly. |
| **Alpha Testing** | Internal testing before release. | Company QA team tests beta version. |
| **Beta Testing** | Testing by limited real users. | Selected users test new Instagram feature. |
| **Performance Testing** | Check speed, stability, scalability. | Measure response time under load. |
| **Load Testing** | Test system under expected user load. | 1,000 users login at same time. |
| **Stress Testing** | Test system beyond limits. | 10,000 users login → system should handle or fail gracefully. |
| **Security Testing** | Find vulnerabilities & data protection issues. | Try SQL Injection on login form. |
| **Usability Testing** | Check ease of use & user-friendliness. | Verify buttons are clickable and navigation is simple. |
| **Compatibility Testing** | Check app on different OS, browsers, devices. | Test site on Chrome, Firefox, Safari, mobile. |
| **Exploratory Testing** | Tester explores app without predefined cases. | Randomly click through modules to find bugs. |
| **Ad-hoc Testing** | Informal/random testing without plan. | Randomly enter special characters in form fields. |
| **Recovery Testing** | Verify system recovers after failure/crash. | Restart app after sudden power cut. |
| **Installation Testing** | Verify installation/uninstallation process. | Install app with wrong config and check error. |
| **Accessibility Testing** | Ensure app usable by differently-abled people. | Screen reader reads all labels correctly. |
| **UI Testing** | Validate look, feel, alignment, fonts. | Check login button color, size, alignment. |
| **End-to-End Testing** | Verify entire business flow. | In banking app → create account → deposit → withdraw → logout. |

---

## But if you want to learn Automation Testing, Think Only about

## PASS & FAIL

## Initially don’t mess-up with the Process What’s Running in-side compony . Just do focous On Coding Part & then know as per need step by step .