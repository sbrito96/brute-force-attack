# Brute-Force Attack Simulation Project

## Overview

This project simulates a brute-force attack against a network system to demonstrate how weak passwords can be compromised. The target system is an Ubuntu Server with OpenSSH enabled, and the attack is performed from a Kali Linux virtual machine.

## Objectives

* Set up a virtualized lab environment.
* Configure network settings to allow communication between virtual machines.
* Perform a brute-force attack against an SSH service.
* Implement security measures to mitigate brute-force attacks.

## Environment

* **Attacker:** Kali Linux (Virtual Machine)
* **Target:** Ubuntu Server (Virtual Machine)

## Steps

### 1. Environment Setup

1.  **Virtual Network Configuration:**
    * Configured both Kali Linux and Ubuntu Server VMs to use an internal network in VirtualBox.
    * Ensured both VMs were in the same internal network to allow communication.
2.  **Static IP Configuration (Ubuntu Server):**
    * Assigned a static IP address (192.168.1.100) to the Ubuntu Server using Netplan.
    * Configured gateway and DNS settings.
    * Verified the IP configuration using `ip a`.
3.  **OpenSSH Installation and Configuration (Ubuntu Server):**
    * Installed the OpenSSH server using `sudo apt update && sudo apt install -y openssh-server`.
    * Verified the SSH service status using `sudo systemctl status ssh`.
    * Allowed SSH connections through the firewall using `sudo ufw allow ssh`.
    * Verified the firewall status with `sudo ufw status`.

### 2. Brute-Force Attack Simulation (Kali Linux)

1.  **Network Configuration (Kali Linux):**
    * Realized that Kali Linux was using NetworkManager instead of Netplan.
    * Configured a static IP address (192.168.1.101) using the NetworkManager GUI.
    * Verified the IP configuration using `ip a`.
2.  **Nmap Scan:**
    * Performed an Nmap scan to verify that the SSH port (22) was open on the Ubuntu Server: `nmap -p 22 192.168.1.100`.
3.  **Hydra Brute-Force Attack:**
    * Executed a brute-force attack using Hydra with the rockyou.txt dictionary: `hydra -l ubuntuserver -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.100`.
    * Resolved an error where rockyou.txt was compressed, and uncompressed the file using the command `sudo gunzip rockyou.txt.gz`.
    * Hydra successfully found the SSH password.
4.  **Verification:**
    * Verified the cracked password by logging into the Ubuntu Server via SSH.

### 3. Mitigation and Security Recommendations

* **Strong Passwords:** Emphasized the importance of using strong, unique passwords.
* **Public Key Authentication:** Recommended using SSH public key authentication.
* **Change SSH Port:** Suggested changing the default SSH port to a non-standard port.
* **Fail2Ban:** Recommended implementing Fail2Ban to block automated attacks.
* **Security Updates:** Highlighted the need to keep systems and software updated.

## Conclusion

This project successfully demonstrated the risks of weak passwords and the importance of implementing robust security measures.



