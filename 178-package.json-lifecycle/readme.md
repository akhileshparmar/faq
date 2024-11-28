In a Node.js `package.json` file, the **`scripts`** section allows you to define custom commands that can be executed using **npm**. These scripts are tied to specific npm commands or can be manually triggered.

---

### **Categories of Scripts in `package.json`**

1. **Lifecycle Scripts**: Automatically run at certain phases of npm commands.
2. **Custom Scripts**: User-defined scripts you can run manually.

---

### **Lifecycle Scripts**

Lifecycle scripts are pre-defined by npm and are executed automatically at various stages. Below is a list of these scripts and when they are triggered:

#### **1. Installation Lifecycle**

- `preinstall`: Runs **before** the installation of dependencies.
- `install`: Runs **during** the installation process.
- `postinstall`: Runs **after** the installation is complete.

#### **2. Build Lifecycle**

- `prepack`: Runs before creating a package tarball (e.g., with `npm pack` or `npm publish`).
- `prepare`: Runs **after dependencies are installed** and **before the package is packed or published**. Often used to build the project or run bundling tools.
- `postpack`: Runs after creating a package tarball.

#### **3. Publishing Lifecycle**

- `prepublishOnly`: Runs before `npm publish`, but after `prepare`. It ensures code is ready for publishing.
- `postpublish`: Runs after the package has been published to npm.

#### **4. Start/Stop Lifecycle**

- `prestart`: Runs before the `start` script.
- `start`: Runs when you execute `npm start`. If no `start` script is defined, it defaults to running `node server.js`.
- `poststart`: Runs after the `start` script.
- `prestop`: Runs before the `stop` script.
- `stop`: Runs when you execute `npm stop`.
- `poststop`: Runs after the `stop` script.

#### **5. Test Lifecycle**

- `pretest`: Runs before the `test` script.
- `test`: Runs when you execute `npm test`.
- `posttest`: Runs after the `test` script.

#### **6. Uninstallation Lifecycle**

- `preuninstall`: Runs before dependencies are removed.
- `uninstall`: Runs during the removal process.
- `postuninstall`: Runs after dependencies are removed.

#### **7. Version Lifecycle**

- `preversion`: Runs before the version bump (e.g., `npm version`).
- `version`: Runs when the package version is being updated.
- `postversion`: Runs after the version bump is complete.

---

### **Custom Scripts**

You can define your own scripts under the `"scripts"` section in `package.json`. These scripts are triggered with `npm run <script-name>`.

#### **Examples of Custom Scripts**

```json
{
  "scripts": {
    "start": "node app.js", // Starts your app
    "build": "webpack --mode production", // Builds the app
    "dev": "nodemon app.js", // Starts app in development mode
    "lint": "eslint src", // Lint your code
    "test": "jest", // Run tests
    "deploy": "npm run build && scp ./dist/* user@server:/path/to/deploy" // Custom deploy
  }
}
```

---

### **Default Behavior for Specific Scripts**

If no custom script is defined, npm has default behaviors for certain commands:

- `npm start`: Runs `node server.js` if no `start` script is defined.
- `npm test`: Runs `echo "Error: no test specified"` if no `test` script is defined.
- `npm stop`: No default behavior.

---

### **How Scripts Are Executed**

1. **Run lifecycle scripts automatically:**

   - Example: `npm install` automatically runs `preinstall`, `install`, and `postinstall`.

2. **Manually run custom scripts:**
   - Command: `npm run <script-name>`
   - Example:
     ```bash
     npm run build
     npm run dev
     npm run lint
     ```

---

### **Script Execution Order**

For a single command, scripts are executed in the following order:

1. `pre<command>`
2. `<command>`
3. `post<command>`

For example, for `npm start`:

1. `prestart`
2. `start`
3. `poststart`

---

### **Full Example of Scripts in `package.json`**

```json
{
  "scripts": {
    "preinstall": "echo Running preinstall script...",
    "install": "echo Installing dependencies...",
    "postinstall": "echo Postinstall script done!",
    "pretest": "echo Preparing tests...",
    "test": "jest",
    "posttest": "echo Tests completed!",
    "build": "webpack --mode production",
    "start": "node app.js",
    "dev": "nodemon app.js",
    "lint": "eslint src",
    "deploy": "echo Deploying app..."
  }
}
```

---

### **Summary**

- **Lifecycle Scripts**: Automatically triggered by npm commands (e.g., `preinstall`, `posttest`).
- **Custom Scripts**: User-defined and triggered with `npm run`.
- The execution order is: `pre<command>` → `<command>` → `post<command>`.

Use lifecycle scripts for automating repetitive tasks and custom scripts for project-specific workflows.
