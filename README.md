# Brute-Force Attack Simulation Project

## Overview

This project simulates a brute-force attack against a server to demonstrate how weak passwords can be compromised easily. The target system is an Ubuntu Server with OpenSSH enabled, and the attack is performed from a Kali Linux virtual machine.

## Objectives

* Set up a virtualized lab environment.
* Configure firewall settings to open SSH connections to the server.
* Perform a brute-force attack against an SSH service.
* Implement security measures to mitigate brute-force attacks.

## Environment

* **Attacker:** Kali Linux (left) - IP: 192.168.1.101 
* **Target:** Ubuntu Server (right) - IP: 192.168.1.100

![attacker-victim-enviroments](https://github.com/user-attachments/assets/521e046d-e97c-481c-8f25-19cae20e9cb6)

## Steps

### 1. Environment Setup

1.  **Virtual Network Configuration:**
   
    * Configured both Kali Linux and Ubuntu Server VMs to use an internal network in VirtualBox.
    * Ensured both VMs were in the same internal network to allow communication.
      
3.  **Static IP Configuration (Ubuntu Server):**
   
    * Assigned a static IP address (192.168.1.100) to the Ubuntu Server using Netplan.
    * Configured gateway and DNS settings.
    * Verified the IP configuration using `ip a`.
      
5.  **OpenSSH Installation and Configuration (Ubuntu Server):**
   
    * Installed the OpenSSH server using `sudo apt update && sudo apt install -y openssh-server`.
    * Verified the SSH service status using `sudo systemctl status ssh`.
    * Allowed SSH connections through the firewall using `sudo ufw allow ssh`.
    * Verified the firewall status with `sudo ufw status`.
  
   ![server-port22-open](https://github.com/user-attachments/assets/1143ca75-0a05-454f-abe7-de3712a553c7)


### 2. Brute-Force Attack Simulation (Kali Linux)

1.  **Network Configuration (Kali Linux):**
   
    * Configured a static IP address (192.168.1.101) using the NetworkManager GUI.
    * Verified the IP configuration using `ip a`.
      
3.  **Nmap Scan:**

    * Performed a Nmap scan to verify that the SSH port (22) was open on the Ubuntu Server: `nmap -p 22 192.168.1.100`.

  ![nmap-to-server](https://github.com/user-attachments/assets/11caca93-ea1e-4aa2-aba6-aec5e6adab83)


4.  **Hydra Brute-Force Attack:**
   
    * Executed a brute-force attack using Hydra with the rockyou.txt dictionary: `hydra -l ubuntuserver -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.100`.
    * Hydra successfully found the SSH password.

![hydra-crack-password](https://github.com/user-attachments/assets/8b2d2819-a513-4f18-88cf-1c5441180526)

  
6.  **Verification:**
   
    * Verified the cracked password by logging into the Ubuntu Server via SSH.

![ssh-server-succesful-login-from-attacker](https://github.com/user-attachments/assets/778d2d6c-8178-4f2e-8b89-bee2cfda6eff)


### 3. Mitigation and Security Recommendations

* **Strong Passwords:** Emphasized the importance of using strong, unique passwords.
* **Public Key Authentication:** The use of SSH public key authentication.
* **Change SSH Port:** Changing the default SSH port to a non-standard port.
* **Fail2Ban:** Implement Fail2Ban to block automated attacks.

## Conclusion

This project successfully demonstrated the risks of weak passwords and the importance of implementing robust security measures.



