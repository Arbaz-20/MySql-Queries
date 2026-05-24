# MySQL Notebooks — Practice Repository

A collection of MySQL lecture notebooks created and run using the **MySQL Shell for VS Code** extension. This README explains how to install the extension, connect to a MySQL server, open these `.mysql-notebook` files, and run the commands.

---

## Table of Contents

1. [What's in this repo](#whats-in-this-repo)
2. [Prerequisites](#prerequisites)
3. [Install MySQL Server](#1-install-mysql-server)
4. [Install the MySQL Shell for VS Code extension](#2-install-the-mysql-shell-for-vs-code-extension)
5. [Create a database connection](#3-create-a-database-connection)
6. [Open the notebooks from this repo](#4-open-the-notebooks-from-this-repo)
7. [Running commands in a notebook](#5-running-commands-in-a-notebook)
8. [Useful keyboard shortcuts](#6-useful-keyboard-shortcuts)
9. [Troubleshooting](#7-troubleshooting)

---

## What's in this repo

```
MySql Notebooks/
├── Lecture 1.mysql-notebook   # Basics: CREATE DATABASE, CREATE TABLE, INSERT
├── Lecture 2.mysql-notebook   # SELECT, WHERE, ORDER BY
├── Lecture 3.mysql-notebook   # Joins and relationships
├── Lecture 4.mysql-notebook   # Aggregations, GROUP BY, HAVING
├── Lecture 5.mysql-notebook   # Subqueries / advanced filtering
├── Lecture 6.mysql-notebook   # Functions, views, stored procedures
└── README.md
```

Each `.mysql-notebook` file is a notebook-style document (similar to a Jupyter notebook) where SQL statements are organized in cells. You can execute cells one at a time and see the result table inline.

---

## Prerequisites

You need three things installed:

| Tool | Purpose | Download |
|------|---------|----------|
| **VS Code** | Editor | https://code.visualstudio.com/ |
| **MySQL Server 8.0+** | The database engine these notebooks connect to | https://dev.mysql.com/downloads/mysql/ |
| **MySQL Shell 8.0+** | Required by the VS Code extension | Bundled with MySQL Installer, or https://dev.mysql.com/downloads/shell/ |

> On Windows, the easiest path is the **MySQL Installer for Windows** — it installs MySQL Server, MySQL Shell, and Workbench together.

---

## 1. Install MySQL Server

### Windows (recommended path)

1. Download **MySQL Installer for Windows** from https://dev.mysql.com/downloads/installer/
2. Run the installer and choose the **Developer Default** setup type — this includes Server, Shell, Workbench, and connectors.
3. During configuration:
   - Authentication method: **Use Strong Password Encryption** (default).
   - Set a **root password** — write it down, you'll need it later.
   - Keep the default port `3306`.
   - Tick **Start the MySQL Server at System Startup**.
4. Finish the installer.

### Verify the server is running

Open PowerShell and run:

```powershell
mysql -u root -p
```

Enter your root password. If you get the `mysql>` prompt, the server works. Type `exit;` to leave.

---

## 2. Install the MySQL Shell for VS Code extension

1. Open VS Code.
2. Open the **Extensions** sidebar (`Ctrl+Shift+X`).
3. Search for **`MySQL Shell for VS Code`** (publisher: **Oracle**).
4. Click **Install**.
5. After installation, a new **DB** icon appears in the left activity bar — this is the extension's main panel.

> The extension requires MySQL Shell to be installed on your machine. If it complains on first launch, install MySQL Shell from the link in [Prerequisites](#prerequisites) and reload VS Code.

---

## 3. Create a database connection

1. Click the **DB icon** in the activity bar (left side of VS Code).
2. In the **DATABASE CONNECTIONS** panel, click the **`+`** button (or right-click → *New Connection*).
3. Fill in the connection form:

   | Field | Value |
   |-------|-------|
   | Caption | `Local MySQL` (any label you want) |
   | Hostname | `localhost` |
   | Port | `3306` |
   | Username | `root` |
   | Schema | *(leave blank, or type the database you want as default)* |
   | Password | Click **Store Password in Vault** and enter your root password |

4. Click **Test Connection** — you should see a green success message.
5. Click **OK** to save.

Your new connection tile now shows up under **DATABASE CONNECTIONS**. Double-click it to open a session.

---

## 4. Open the notebooks from this repo

### Option A — Open the whole folder

1. In VS Code: **File → Open Folder…** → select the `MySql Notebooks` folder.
2. In the Explorer sidebar (`Ctrl+Shift+E`) you'll see all six `.mysql-notebook` files.
3. **Double-click any `Lecture N.mysql-notebook`** file — VS Code automatically opens it in the MySQL notebook editor (because the extension registers a handler for this file type).

### Option B — Open a single file

1. **File → Open File…** and pick a `.mysql-notebook` file directly.

> If a notebook opens as plain JSON text instead of the notebook UI, the extension isn't installed correctly. Reinstall the **MySQL Shell for VS Code** extension and reload the window (`Ctrl+Shift+P` → *Developer: Reload Window*).

---

## 5. Running commands in a notebook

When a notebook is open you'll see:

- A **connection picker** at the top — click it and select **`Local MySQL`** (or whatever you named your connection). The notebook needs an active connection to execute anything.
- **Code cells** containing SQL statements.
- A small toolbar on each cell with **Run** / **Run All** buttons.

### Running a single statement

- Place the cursor inside a SQL statement and press **`Ctrl+Enter`** — runs the current statement and shows the result table below the cell.

### Running everything in a cell

- Click the ▶ button on the left of the cell, or press **`Shift+Enter`**.

### Running the whole notebook

- Click **Run All** at the top of the editor, or use the command palette: `Ctrl+Shift+P` → *Notebook: Run All*.

### Recommended order

Run the lectures in numerical order (Lecture 1 → Lecture 6). Earlier notebooks create databases and tables that later ones may rely on.

### Selecting a default schema

Many notebooks start with:

```sql
USE some_database;
```

Make sure that statement runs successfully before executing later cells, otherwise queries will error with `No database selected`.

---

## 6. Useful keyboard shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Enter` | Run current SQL statement |
| `Shift+Enter` | Run current cell, move to next |
| `Ctrl+Shift+P` | Command palette (search for *MySQL* commands) |
| `Ctrl+S` | Save the notebook (results are saved with it) |
| `Ctrl+/` | Toggle SQL line comment |

---

## 7. Troubleshooting

**"No active connection" when running a cell**
Click the connection picker at the top of the notebook and choose your saved connection.

**`Access denied for user 'root'@'localhost'`**
The password stored in the connection is wrong. Right-click the connection → *Edit Connection* → re-enter the password and tick *Store Password in Vault*.

**`Unknown database 'xxx'`**
Run `CREATE DATABASE xxx;` first, then `USE xxx;`. The earlier lecture notebooks contain the `CREATE DATABASE` statements — make sure you ran them.

**Notebook opens as raw JSON**
The extension is missing. Install **MySQL Shell for VS Code** (Oracle) and reload the window.

**`MySQL Shell not found`**
Install MySQL Shell from https://dev.mysql.com/downloads/shell/ and restart VS Code. On Windows make sure `mysqlsh.exe` is on your `PATH`.

**Server isn't running**
Open *Services* (`services.msc` on Windows) → find **MySQL80** → right-click → *Start*.

---

## Notes

- All commands in these notebooks were written while learning MySQL — they are practice exercises, not production code.
- Feel free to edit cells, rerun them, and experiment.
