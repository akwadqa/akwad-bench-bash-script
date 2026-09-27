# akwad-bench

A lightweight CLI manager for Frappe v16 local development on WSL. It runs Frappe in the background via Supervisor (freeing up your terminal) with 0% idle RAM usage, and automates local Nginx DNS routing.

## ✨ Current Features

* **Zero-Idle Resources:** Background workers only run when you explicitly start them (`autostart=false`).
* **Auto DNS Routing:** Automatically configures Nginx and updates your Windows `hosts` file (e.g., `[http://crm.local](http://crm.local)`).
* **Smart Port Shifting:** Detects port collisions and automatically shifts your bench to the next available port block.
* **Interactive Logs:** A simple CLI menu to tail Web, Worker, Scheduler, or Redis logs.
* **Clean Teardown:** Safely destroys benches, databases, and routing configs in a single command.

## 🚀 Installation

*Prerequisite: Requires `jq` (`sudo dnf install jq -y`) and the standard `bench` CLI.*

Download the script and make it executable:

```bash
sudo curl -o /usr/local/bin/akwad-bench https://raw.githubusercontent.com/your-org/akwad-bench/main/akwad-bench
sudo chmod +x /usr/local/bin/akwad-bench

```

## 🛠️ Daily Workflow

Run these commands from inside your bench directory:

**1. Initialize a Standard Bench**

```bash
UV_PYTHON=3.14 bench init my-bench --frappe-branch version-16
cd my-bench

```

**2. Create & Route Your Site** (Sets up DB and local DNS)

```bash
akwad-bench add-site dev.local

```

**3. Setup Background Workers** (Registers workers but keeps them stopped)

```bash
akwad-bench setup-workers

```

**4. Start Coding** (Spins up the backend; terminal remains free)

```bash
akwad-bench start

```

**5. Stop & Save RAM** (When finished for the day)

```bash
akwad-bench stop

```

## 💻 Core Commands Reference

| Command | Action |
| --- | --- |
| `akwad-bench status` | Dashboard of all local benches and their RUNNING/STOPPED status. |
| `akwad-bench logs` | Interactive menu to stream live logs. |
| `akwad-bench auto` | Auto-detects and fixes port collisions. |
| `akwad-bench destroy` | Safely wipes the bench, routing, and databases. |
