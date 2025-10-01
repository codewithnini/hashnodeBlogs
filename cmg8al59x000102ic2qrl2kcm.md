---
title: "npm and typescript command"
datePublished: Wed Oct 01 2025 18:00:39 GMT+0000 (Coordinated Universal Time)
cuid: cmg8al59x000102ic2qrl2kcm
slug: npm-and-typescript-command
tags: codewithnini

---

# Commands

Here’s a **clean table format** for all **Node.js** and **TypeScript commands**, separated clearly for quick reference.

---

## **📘 Node.js Commands**

| Command | Description |
| --- | --- |
| `node -v` | Check Node.js version |
| `npm -v` | Check npm version |
| `npm init` | Initialize a new project (interactive) |
| `npm init -y` | Initialize a new project with default settings |
| `npm install <package>` | Install package locally |
| `npm install -g <package>` | Install package globally |
| `npm install --save <package>` | Add package to dependencies |
| `npm install --save-dev <package>` | Add package to devDependencies |
| `npm uninstall <package>` | Remove a package |
| `npm update <package>` | Update a package |
| `node app.js` | Run a JS file |
| `nodemon app.js` | Run with auto-reload (requires nodemon) |
| `npm start` | Run start script from package.json |
| `npm run <script>` | Run custom script from package.json |
| `npm list -g --depth=0` | List global packages |
| `npm outdated` | Check outdated packages |
| `node` | Start Node.js REPL (interactive console) |
| `node --inspect app.js` | Debug Node.js file using Chrome DevTools |
| `node --trace-warnings app.js` | Show runtime warnings |

---

## **📘 TypeScript Commands**

| Command | Description |
| --- | --- |
| `npm install -g typescript` | Install TypeScript globally |
| `tsc -v` | Check TypeScript version |
| `tsc --init` | Initialize a TypeScript project (`tsconfig.json`) |
| `tsc app.ts` | Compile a single TypeScript file to JavaScript |
| `tsc` | Compile project using `tsconfig.json` |
| `tsc -w` | Watch mode – automatically compile on file changes |
| `tsc app.ts --target ES6` | Compile TS file targeting ES6 JS |
| `tsc app.ts --outDir ./dist` | Set output directory for compiled JS |
| `tsc app.ts --module commonjs` | Set module system |
| `ts-node app.ts` | Run TypeScript file directly without compiling (requires `ts-node`) |
| `tsc --listFiles` | List all files compiled by TypeScript |
| `tsc --diagnostics` | Show compilation statistics |
| `tsc --init --strict` | Create `tsconfig.json` with strict mode enabled |
| `tslint -c tslint.json 'src/**/*.ts'` | Lint TypeScript files (requires `tslint`) |
| `prettier --write "src/**/*.ts"` | Format TypeScript files (requires `prettier`) |

---

✅ **Tip:**

* **Node.js commands** are mostly for runtime, package management, and debugging.
    
* **TypeScript commands** focus on compilation, type checking, and project configuration.
    

✅ Let’s make a **combined Node.js + TypeScript commands cheatsheet** in **table format**, grouped by category, and I’ll add **color-coded sections** (using emojis as “color tags” for readability).

---

# **🌐 Node.js + TypeScript Commands Cheatsheet**

---

## 🔵 **Setup & Versions**

| Command | Tool | Description |
| --- | --- | --- |
| `node -v` | Node.js | Check Node.js version |
| `npm -v` | Node.js | Check npm version |
| `tsc -v` | TypeScript | Check TypeScript version |
| `npm install -g typescript` | TypeScript | Install TypeScript globally |
| `npm install -g ts-node` | TypeScript | Install `ts-node` for direct execution |

---

## 🟢 **Project Initialization**

| Command | Tool | Description |
| --- | --- | --- |
| `npm init` | Node.js | Create project (interactive) |
| `npm init -y` | Node.js | Create project with defaults |
| `tsc --init` | TypeScript | Create `tsconfig.json` (project config) |
| `tsc --init --strict` | TypeScript | Create config with strict mode |

---

## 🟡 **Running & Execution**

| Command | Tool | Description |
| --- | --- | --- |
| `node app.js` | Node.js | Run JS file |
| `nodemon app.js` | Node.js | Run JS with auto-reload |
| `tsc app.ts` | TypeScript | Compile TS → JS |
| `tsc` | TypeScript | Compile all files (based on tsconfig.json) |
| `tsc -w` | TypeScript | Watch mode (auto-compile on changes) |
| `ts-node app.ts` | TypeScript | Run TS file directly (no manual compile) |

---

## 🟠 **Package Management**

| Command | Tool | Description |
| --- | --- | --- |
| `npm install <pkg>` | Node.js | Install dependency locally |
| `npm install -g <pkg>` | Node.js | Install dependency globally |
| `npm install --save <pkg>` | Node.js | Add to dependencies |
| `npm install --save-dev <pkg>` | Node.js | Add to devDependencies |
| `npm uninstall <pkg>` | Node.js | Remove dependency |
| `npm update <pkg>` | Node.js | Update dependency |
| `npm list -g --depth=0` | Node.js | List global packages |

---

## 🔴 **Scripts & Automation**

| Command | Tool | Description |
| --- | --- | --- |
| Add in `package.json`: `"start": "node app.js"` | Node.js | Define start script |
| `npm start` | Node.js | Run start script |
| `npm run <script>` | Node.js | Run custom script |
| Example: `"dev": "ts-node src/index.ts"` | Node.js + TS | Run TS file via npm script |

---

## 🟣 **Debugging & Utilities**

| Command | Tool | Description |
| --- | --- | --- |
| `node --inspect app.js` | Node.js | Debug with Chrome DevTools |
| `node --trace-warnings app.js` | Node.js | Show runtime warnings |
| `tsc --listFiles` | TypeScript | List all compiled files |
| `tsc --diagnostics` | TypeScript | Show compile stats |

---

✅ With this layout:

* **🔵 Setup** → install & check versions
    
* **🟢 Init** → start new project
    
* **🟡 Run** → execute JS/TS files
    
* **🟠 Packages** → manage dependencies
    
* **🔴 Scripts** → automate with npm scripts
    
* **🟣 Debugging** → troubleshoot