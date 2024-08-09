

# Cyber Security Incident Response: Indicators of Compromise (IoC) and Mitigation Steps

This repository outlines the steps taken to identify and mitigate a compromised system in which a backdoor script (`/backdoor.sh`) was discovered. The objective of this guide is to provide a clear understanding of how to detect, investigate, and remove malicious activities from a compromised system.

## Overview

A compromised system can display various Indicators of Compromise (IoC), such as unusual files, suspicious processes, or unexpected network activities. This guide will walk you through the detection and removal process to secure your system.

## Steps to Identify and Mitigate Compromise

### 1. **Initial Identification of Malicious Files**
   - **File Detected:** `/backdoor.sh`
   - **Risk:** This file allows attackers to execute malicious commands on the system.
   - **Detection:** Security tools or manual inspection led to the discovery of this script.

### 2. **Detection of Malicious Activity**
   - **Focus:** Investigate any files that indicate potentially malicious activity.
   - **Command:** 
     ```bash
     ls -al /etc/
     ```
   - **Command:** 
     ```bash
     cat /etc/passwd
     ```
   - **Command:** 
     ```bash
     ls -al /root/
     ```

### 3. **Attack Investigation**
   - **Procedure:** Investigate the presence of the malicious `backdoor.sh` file by checking related logs, processes, and other signs of compromise.
   - **Commands:**
     - List scheduled tasks:
       ```bash
       crontab -l
       ```
     - Check running processes:
       ```bash
       ps aux | grep cron
       ps aux | grep crond
       ```

### 4. **Data Exfiltration Assessment**
   - **Objective:** Since `backdoor.sh` could be used for unauthorized data exfiltration, assume that attackers may have accessed sensitive data.
   - **Check network activity:**
     ```bash
     ifconfig
     ```
   - **Check scheduled tasks again:**
     ```bash
     crontab -e
     ```

### 5. **Investigation of Compromised Components**
   - **Procedure:** Verify which system components are compromised.
   - **Tools:**
     - **`ps` command:** Check if unauthorized programs are running.
     - **`ls` command:** Identify any unfamiliar files in critical directories.

### 6. **Network Traffic Analysis**
   - **Objective:** Analyze network traffic to identify any ongoing malicious activities.
   - **Tool:** 
     ```bash
     iftop
     ```

### 7. **Immediate Remediation Steps**
   - **Stop the SSH Service:**
     ```bash
     service ssh stop
     ```
   - **Remove Unauthorized SSH Keys:**
     ```bash
     rm /root/.ssh/authorized_keys
     rm /home/[username]/.ssh/authorized_keys
     ```

### 8. **Review and Remove the Malicious Cron Job**
   - **Objective:** Remove any malicious cron jobs that execute the backdoor script.
   - **Steps:**
     1. Open the crontab editor:
        ```bash
        crontab -e
        ```
     2. Locate and remove the following line:
        ```bash
        * * * * * root sh /backdoor.sh 2>&1
        ```
     3. Save and exit:
        - **GNU nano:** Press `CTRL + X`, then `Y`, and finally `Enter`.
        - **Vim:** Press `Esc`, then type `:wq`, and press `Enter`.

### 9. **Ensure the Attacker’s Access is Revoked**
   - **Objective:** Ensure that the attacker cannot regain access through the SSH service.
   - **Command:** 
     ```bash
     service ssh stop
     ```
   - **Permanently remove the attacker’s SSH keys:**
     ```bash
     rm -rf /root/.ssh/authorized_keys
     ```

### 10. **Final Cleanup**
   - **Remove the Backdoor Script:**
     ```bash
     rm /backdoor.sh
     ```
   - **Verify No Other Unauthorized Access Exists:**
     ```bash
     ps aux | grep ssh
     ```

### 11. **Report the Incident**
   - **Action:** Document the findings and report the incident to the relevant parties, including theft of private financial data, if applicable.

### 12. **Post-Incident Actions**
   - **Objective:** Write a comprehensive analysis of the incident, including all actions taken to mitigate the threat.
   - **Deliverable:** A final report detailing the incident, actions taken, and recommendations to prevent future attacks.

## Conclusion

This guide provides a clear procedure to follow when dealing with a system compromise due to a backdoor script. Following these steps will help mitigate the immediate threat and prevent further exploitation of the compromised system. 

Please ensure that all actions are taken carefully and that a thorough analysis is performed to avoid missing any potential threats.

