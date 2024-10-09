# SSH Honeypot Setup Guide

This README provides step-by-step instructions for setting up a Cowrie SSH honeypot using two virtual machines: one acting as the attacker (Kali Linux) and the other as the victim (Parrot OS).

## Prerequisites

- Two VMs:
  - **Attacker VM**: Kali Linux
  - **Victim VM**: Parrot OS
- Internet connection for downloading packages
- Basic knowledge of terminal commands

## Step 1: Setting Up the VMs

1. **Create Two VMs**:
   - Use your preferred virtualization software (e.g., VirtualBox, VMware).
   - Allocate sufficient resources (CPU, RAM) to both VMs.
   - Install Kali Linux as the attacker VM and Parrot OS as the victim VM.

2. **Network Configuration**:
   - Ensure both VMs are on the same network (e.g., Host-Only or Internal Network).

## Step 2: Installing Cowrie on the Victim Machine

This section outlines the steps to install Cowrie, an SSH honeypot, on the victim machine (Parrot OS).

### 2.1 Update the System

Before installing Cowrie, ensure your system is up-to-date:

```bash
sudo apt update && sudo apt upgrade -y
```

### 2.2 Run the docker container
```bash
docker run -p 2222:2222 cowrie/cowrie:latest
```
 - You can choose any other port and its ideal to change the port as some hackers might already be aware of this honeypot and its default port. 

If you face error with name resolution, you can update the required config file or use the **full link of the container**:
```bash
docker run -p 2222:2222 docker.io/cowrie/cowrie:latest
```

### **your personal HoneyPot has been setup!**

## Step 3: Attacking the machine

For demonstration purpose we will use Kali to attempt an **attack**

### 3.1 Running **Nmap** to find open ports:

```bash
nmap -sV <ip>
```
 - This gives us open ports available and we see that **port 2222** is running ssh with respective the version
 - The output looks too real to the attacker, which makes the machine look **legit**.

### 3.2 SSH Connection

```bash
ssh -p 2222 root@<ip>
```

 - Enter any password you like, you will get access easily.
 - But wait, **it looks too easy?** doesnt matter.

## Step 4: Observing logs and attacker's behavior
 - He has got access but to a **fake filesystem**.
 - This file system can be modified to look like an organizations default file system **(Ex: File System of a Banking companies)**
 - We can observe each step the hacker takes inside our honeypot. This not only gave off his **IP address** but also can help us understand his **motive** through his actions on the system. 



### **There you go, you have your own HoneyPot setup!. You can also spin up an EC2 server with the Honeypot and leave it open in the internet for a while, you might catch someone!**


























