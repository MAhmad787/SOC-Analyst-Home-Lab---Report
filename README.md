# SOC Analyst Home Lab Report

## 1. Introduction

This home project is inspired by Eric Capuano’s blog “So you want to be a SOC Analyst?”. It helped me get hands-on experience with how a real SOC works. I simulated real-world attack scenarios, monitored system behavior, and responded to malicious activity using detection rules.

The goal was to understand how logs are collected, how malicious activity looks in telemetry, and how to respond using rules and automated actions.

---

## 2. Lab Setup

### Virtual Machines:
- **Windows 11** (Victim Machine)
- **Ubuntu Server** (Used as attacker + log monitoring setup)

### Tools Used:
- **Sysmon** – for detailed system activity logging  
- **LimaCharlie** – as the SIEM and detection/response engine  
- **Sliver C2** – to simulate attacker behavior  

---

## 3. Step-by-Step Walkthrough

### Environment Setup
- Installed VMware and created both VMs.
- Used Ubuntu Server for its lightweight setup.
- Turned off Windows Defender from settings and registry, and disabled Windows Updates to keep it off.

### Sysmon Configuration
- Downloaded Sysmon from the official site.
- Installed with basic config, then replaced with SwiftOnSecurity config for better log quality.

### LimaCharlie Setup
- Created account and organization.
- Generated an install key and deployed sensor on Windows.
- Linked it with Sysmon via artifact rules.

### Attacker Setup
- Installed Sliver C2 on Ubuntu.
- Generated a Windows payload (implant).
- Set up a local Python server to transfer the payload to Windows.
- Downloaded and executed the payload as Administrator to establish a session.

### C2 Interaction
- Interacted with the implant to simulate attacker activity.
- Enumerated system info and observed how that looked in LimaCharlie telemetry.

---

## 4. Detection & Response

- Observed logs and confirmed that the payload execution was detected.
- Wrote a detection rule for the specific file and command line of the payload.
- Configured automated response actions:
  - Report alert  
  - Isolate the system  
  - *(Tried process kill, but it wasn’t supported directly)*

- Tested rule on other processes to verify functionality and understand how the detection engine behaves.

---

## 5. Summary

This project helped me understand:
- How endpoint telemetry looks during real attacks.
- How to write detection rules in LimaCharlie.
- How to respond automatically to threats.

Even though some attack simulations didn’t go as planned (e.g., Procdump, SAM access), I still got valuable insight into SOC workflows, and I plan to build on this in my next project.
