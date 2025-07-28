# HoneyPot Server To Detect Attack Patterns

## 1. Introduction

Cybersecurity has become an important area of concern in the digital era, where attackers constantly look at systems for vulnerabilities. One of the effective strategies for studying and defending against such attacks is the use of **HoneyPots**—systems designed to attract attackers and log their behavior. These systems act as a real service and record attempts at unauthorized access without putting actual resources at risk.

The goal of this project is to implement a honeypot using **Cowrie**, which simulates an SSH or Telnet environment, allowing detailed tracking of attacker behavior. Also integrates **Fail2Ban** to respond automatically to repeated incorrect login attempts.

Through this project, we aim to demonstrate how honeypots can be leveraged not only to collect intelligence on cyberattacks but also to enhance system resilience through automated mitigation techniques.

## 2. Abstract

The increasing sophistication of cyberattacks has necessitated the implementation of proactive defense mechanisms. This project focuses on deploying a honeypot server to detect and analyze unauthorized access attempts and attack patterns.

A **low-interaction honeypot** using **Cowrie**, a well-known SSH and Telnet honeypot, was deployed on a virtual Ubuntu server. Attackers attempting to connect to the server through SSH were logged, including details such as IP addresses, attempted credentials, and packet-level information.

To further strengthen the setup, **Fail2Ban** was integrated to automatically block IP addresses after multiple failed login attempts. This system not only aids in understanding common attack vectors but also serves as an effective early-warning system against brute-force attacks.

## 3. Tools Used

* **VirtualBox**: runs a virtualized instance of an OS
* **Ubuntu Server**: The operating system used to host the honeypot environment
* **Cowrie**: a medium-interaction SSH and Telnet honeypot designed to log brute-force attacks and the shell interaction performed by the attacker
* **Python Virtual Environment**: creates an isolated environment
* **Fail2Ban**: automatically bans IPs with multiple incorrect login attempts
* **OpenSSH**: to attempt remote connections from a different device

## 4. Steps Involved in Building the Project

### 1. Setup Ubuntu Server on VirtualBox

* Installed and setup Ubuntu Server OS on a VirtualBox

### 2. Install and Configure Cowrie

* Created a Python virtual environment
* Installed Cowrie on the virtual environment
* Configured Cowrie to run on port 2222 (`file=/etc/cowrie.config.dist`)
* Enabled logging to capture SSH connection attempts

### 3. SSH Connection

* Ensured port 2222 was open using firewall rules
* Connected from a second device using:

  ```bash
  ssh -p 2222 user@honeypotip
  ```
* Login attempts were captured in the Cowrie log files, including source IP, timestamps, commands issued, etc.

### 4. Log Analysis

* Reviewed Cowrie’s log files to examine:

  * Attacker IP address
  * Failed login attempts
  * Commands entered after login

### 5. Fail2Ban Integration

* Installed and configured Fail2Ban
* Wrote a custom jail and filter for Cowrie logs
* Set the rule: block IP after 3 failed attempts
* Tested and confirmed that the IP was banned after 3 wrong login attempts
* Reviewed the logs and verified

## 5. Conclusion

In conclusion, the project successfully demonstrates the deployment and operation of a honeypot server using **Cowrie** to detect and analyze attack patterns on a server.
By logging connection attempts and attacker behavior, the honeypot offers valuable insight into potential threats. Integration with **Fail2Ban** adds an active defense layer, preventing repeated brute-force attacks from the same source.

