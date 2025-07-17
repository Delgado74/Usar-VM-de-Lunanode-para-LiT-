# ✨ Tutorial: Pruned Bitcoin Node + LiT on Lunanode (Signet)

## 🧠 Index

1. Introduction
2. Tool Overview

   * 2.1. What is Lunanode?
   * 2.2. What is LiT (Lightning Terminal)?
3. Hands-on: Setting Up Your Environment

   * 3.1. Create an SSH Key Pair
   * 3.2. Create a Virtual Machine (VM)
   * 3.3. Remote Access and Terminal Usage
   * 3.4. Clone the Scripts from GitHub
   * 3.5. Using the Scripts
4. Pros and Cons of This Setup

---

## 🗒️ Introduction

Running a full Bitcoin node—whether to manage Lightning channels or verify your own transactions—is an excellent way to contribute to the network and use Bitcoin with sovereignty. However, keeping a node running continuously requires resources that aren’t always readily available: stable electricity, a permanent internet connection, and a computer that can stay on for weeks or months. For many people, this isn’t feasible.

That’s why cloud-based solutions like **Lunanode** provide a realistic and practical alternative. You can deploy a **virtual machine (VM)** in minutes with all the resources needed to run a pruned Bitcoin node, an LND node, and the web interface of **LiT (Lightning Terminal)**, all on the **Signet test network**—perfect for experimenting with no risk.

This tutorial walks you through the steps using the most affordable Lunanode plan and community-maintained tools like the **installation scripts by FoxtrotZulu**.

---

## 🔧 Tool Overview

### 2.1 What is Lunanode?

**Lunanode** is a cloud infrastructure provider with a technical focus and affordable pricing. It offers customizable **virtual machines (VMs)**, payments with Bitcoin and Lightning, automated snapshots, public IP addresses, and additional storage. One of its main attractions is the **\$7 USD/month plan**, which includes:

* 1 vCPU
* 2 GB RAM
* 20 GB SSD storage
* 1 public IPv4 address
* Up to 1 TB monthly bandwidth

Lunanode allows instant server deployment, SSH access, additional volume mounting, and configuration automation. It's ideal for small projects like running a pruned Bitcoin node (with 2 GB pruning) and a Lightning node—especially in educational or testing environments like **Signet**.

### 2.2 What is LiT (Lightning Terminal)?

**LiT (Lightning Terminal)** is a web suite developed by Lightning Labs that combines several essential tools to manage LND nodes in a friendly and integrated way. Key features include:

* **Web interface** to control and monitor your node via browser
* **Loop**: facilitates on-chain ↔ Lightning fund transfers
* **Pool**: liquidity market for channel creation (mainnet only)
* **Terminal CLI**: run commands remotely via browser
* **Full integration with LND**, no external tools needed

It works perfectly on testnet or signet—ideal for learning safely.

---

## ✍️ Hands-on: Setting Up Your Environment

### 3.1 Create an SSH Key Pair

On your local computer (Linux or macOS), open a terminal and run:

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

Press Enter to accept the default values. This creates two files:

* `~/.ssh/id_ed25519` (private key)
* `~/.ssh/id_ed25519.pub` (public key)

To copy the public key, run:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the entire line and paste it into:

* Your Lunanode panel (under SSH Keys)
* GitHub (if cloning with SSH)
* The server, when requested by the script

**Example:**

```
ssh-ed25519 AAAAC3... user@mail.com
```

### 3.2 Create a Virtual Machine (VM)

1. Go to [https://www.lunanode.com](https://www.lunanode.com) and create an account.
2. Log in to the control panel and add credit to your account.
3. Navigate to “Virtual Machines” → “Create VM”.
4. Choose a region (e.g., Montreal) and select Ubuntu 22.04.
5. Choose the \$7 USD/month plan (1 vCPU, 2 GB RAM, 20 GB SSD).
6. Name your VM.
7. Add your SSH public key on the left-hand panel, under SSH section.

The password will be used later when connecting via terminal using SSH.

### 3.3 Remote Access and Terminal Usage

Connect to your VM using its public IP:

```bash
ssh -i ~/.ssh/id_ed25519 ubuntu@YOUR_VM_IP
```

Now you can work on your VM as if it were a local machine. Use the password from the Lunanode web panel if prompted.

### 3.4 Clone the Scripts from GitHub

From your VM terminal:

Visit the repository:
[https://github.com/LibreriadeSatoshi/ejecuta-litd](https://github.com/LibreriadeSatoshi/ejecuta-litd)

Follow the instructions provided there to access scripts created by FoxtrotZulu:
([https://github.com/Foxtrot-Zulu?tab=repositories](https://github.com/Foxtrot-Zulu?tab=repositories))

### 3.5 Using the Scripts

Before running the scripts, edit the following files in the `scripts` folder:

```bash
cd scripts
nano bitcoin_setup.sh            # if compiling Bitcoin from source
nano bitcoin_setup_binary.sh     # if using precompiled binaries
```

Adjust these lines based on your VM's resources:

```bash
dbcache=3000   # change to 1000
prune=50000    # change to 2000
```

These settings are optimized for:

* Using just 1 GB of RAM for database cache
* Limiting blockchain size to 2 GB on disk

Then, follow the instructions in the repository's `README.md` to run the scripts. They will install:

* Pruned Bitcoin Core
* LND configured for the Signet network
* LiT accessible via browser at `YOUR_VM_PUBLIC_IP:8443`

---

## ⚖️ Pros and Cons of This Setup

### ✅ Pros

* **Affordable**: run your node 24/7 for just \$7/month
* **No dependency on local conditions**: no power or internet issues
* **User-friendly**: Lunanode's control panel is intuitive and supports quick reinstalls
* **Scalable**: upgrade resources as your project grows
* **Safe testing environment**: Signet lets you experiment with no risk
* **LiT provides a powerful and friendly UI**, ideal for beginners and advanced users alike
* **LiT works on mobile too**: just open a browser and go to `YOUR_VM_PUBLIC_IP:8443`

### ❌ Cons

* **Third-party dependency**: although you control the system, the infrastructure isn’t yours
* **Downtime or latency** possible if Lunanode’s network has issues
* **Security**: you must properly protect your SSH keys and VM access
* **No graphical interface (GUI)**: everything is done via terminal or browser
