````
# ⚡️ Electron Learning Resource: Beginner to Advanced

---

## 📘 1. What is Electron?

- **Electron** lets you build **native desktop apps** using **JavaScript, HTML, and CSS**.
- It combines **Chromium** and **Node.js** into a single runtime.
- Apps built with Electron:
  - **VS Code**
  - **Slack**
  - **Discord**
  - **Figma**
  - **Notion**

---

## 🚀 2. Prerequisites

Make sure you’re comfortable with:

- 🟩 JavaScript (ES6+)
- 🧩 Node.js & npm
- 🖼 HTML/CSS
- 💻 Terminal/CLI basics

---

## 🏗 3. Project Setup

### 🔧 Install Electron

```bash
mkdir electron-app && cd electron-app
npm init -y
npm install electron --save-dev
````

### 📁 Project Structure

```
electron-app/
├── main.js         // Main process
├── preload.js      // Secure bridge (optional)
├── renderer.js     // UI logic (optional)
├── index.html      // App UI
├── package.json    // App metadata
```

---

## 🧪 4. First Working Example

### main.js

```js
const { app, BrowserWindow } = require('electron')
const path = require('path')

function createWindow () {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js'),
      contextIsolation: true
    }
  })

  win.loadFile('index.html')
}

app.whenReady().then(createWindow)
```

### index.html

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Hello from Electron</h1>
    <button onclick="window.api.showMsg()">Click me</button>
    <script src="renderer.js"></script>
  </body>
</html>
```

### preload.js

```js
const { contextBridge, ipcRenderer } = require('electron')

contextBridge.exposeInMainWorld('api', {
  showMsg: () => ipcRenderer.send('show-msg')
})
```

### Add to main.js

```js
const { ipcMain, dialog } = require('electron')

ipcMain.on('show-msg', () => {
  dialog.showMessageBox({ message: 'Hello from Main Process!' })
})
```

---

## 🧠 5. Core Concepts

| Concept          | Description                                       |
| ---------------- | ------------------------------------------------- |
| Main Process     | Controls app lifecycle & native modules           |
| Renderer Process | Runs HTML/CSS/JS UI                               |
| Preload Script   | Bridge between main & renderer                    |
| IPC              | Communication between processes                   |
| Security         | Use `contextIsolation`, disable `nodeIntegration` |

---

## 🛠 6. Intermediate Projects

1. ✅ Hello World App
2. 📁 File Explorer
3. 📝 Markdown Editor
4. 🔒 Secure Login App
5. 🧾 PDF Generator
6. 🗂 Tabbed App Interface

---

## 📦 7. Packaging & Distribution

### Install electron-builder

```bash
npm install electron-builder --save-dev
```

### package.json Example

```json
"scripts": {
  "start": "electron .",
  "build": "electron-builder"
},
"build": {
  "appId": "com.fakhir.electronapp",
  "productName": "FakhirElectronApp",
  "win": {
    "target": "nsis"
  },
  "mac": {
    "target": "dmg"
  }
}
```

### Build Command

```bash
npm run build
```

---

## 🔌 8. Useful Modules & Tools

| Module             | Use Case                     |
| ------------------ | ---------------------------- |
| `electron-store`   | Save settings & preferences  |
| `electron-builder` | Build apps for all OS        |
| `electron-updater` | Auto-update your app         |
| `sqlite3`          | Local database               |
| `node-notifier`    | Desktop system notifications |

---

## 🔐 9. Security Best Practices

* ✅ Enable `contextIsolation`
* ❌ Disable `nodeIntegration`
* ✅ Use `preload.js` to expose safe APIs only
* ✅ Validate all file paths and inputs
* ✅ Use `sandbox: true` when possible

---

## 🧑‍🎓 10. Learning Milestones

| Level        | Focus Area                              |
| ------------ | --------------------------------------- |
| Beginner     | Setup, Hello World, Load HTML           |
| Intermediate | IPC, Menus, File Dialogs                |
| Advanced     | Auto Updates, Native APIs               |
| Expert       | Custom Systems, Full-scale Desktop Apps |

---

## 🔮 11. Advanced Topics

* 🖼 Custom Menus
* 📁 Native File Access (fs, path)
* 🧠 SQLite or NeDB for storage
* 🌐 Drag/Drop from OS
* 🔐 Login/Auth simulation
* 🔄 Auto-updates with GitHub releases
* ⚛ Integrate React, Vue, or Svelte with Electron

---

## 📚 12. Official Resources

* [Electron Docs](https://www.electronjs.org/docs/latest/)
* [API Reference](https://www.electronjs.org/docs/latest/api/)
* [Security Guide](https://www.electronjs.org/docs/latest/tutorial/security)
* [electron-builder](https://www.electron.build/)

---
