# Web Security Attacks Project

1. Introduction
   
Web security attacks are increasingly prevalent in today's digital landscape. Websites 
and web applications, being integral to businesses, governments, and individuals, are 
prime targets for attackers seeking to exploit vulnerabilities for malicious purposes. 
These attacks can lead to data breaches, financial loss, and loss of reputation. 
Understanding common web security attack types, their techniques, and 
countermeasures is essential for improving the security posture of web applications.
This report will provide an overview of common web security attacks used to elevate 
privileges and exploit vulnerabilities, followed by testing recommendations using 
controlled environments. Lastly, a summary of potential countermeasures will be 
presented to mitigate these risks.
The goal of this Web Security Attacks Project is to enhance understanding of common 
web application vulnerabilities and attack techniques through hands-on simulation 
within a controlled environment. It aims to develop effective mitigation strategies and 
promote ethical hacking practices to protect against identified vulnerabilities. 
Ultimately, the project seeks to foster security awareness and encourage continuous 
learning among developers and stakeholders to improve the overall security posture of 
web applications.

# Overview

Web security attacks pose a significant threat to websites and web applications, often leading to data breaches, financial losses, and reputational damage. This project focuses on:

Identifying and simulating common attack types such as SQL Injection, XSS, and CSRF.
Testing vulnerabilities in a controlled environment using Damn Vulnerable Web Application (DVWA).
Proposing effective countermeasures to mitigate risks.

# Key Objectives

Understand and simulate common web attacks in a safe environment.
Enhance knowledge of tools like SQLMap, Nikto, and DVWA.
Promote secure coding practices and countermeasures for mitigating vulnerabilities.
Simulated Attacks

1. SQL Injection (SQLi)
Exploits vulnerable SQL queries to extract sensitive data or bypass authentication.
Example payload: ' OR 1=1 --
Tool: SQLMap.
2. Cross-Site Scripting (XSS)
Injects malicious scripts into web pages, affecting end-users.
Example payload: <script>alert('XSS')</script>.

4. Cross-Site Request Forgery (CSRF)
Tricks authenticated users into performing unintended actions.
Example scenario: Transferring funds without user consent.

6. File Inclusion Vulnerabilities
Exploits inclusion of external files to execute unauthorized actions.
Types: Local File Inclusion (LFI) and Remote File Inclusion (RFI).

8. Directory Traversal
Manipulates file paths to access restricted directories.
Example payload: ../etc/passwd.

10. Command Injection
Executes arbitrary system commands through vulnerable input fields.
Example payload: ; rm -rf /.


# Tools and Environment


VirtualBox: Virtualization for isolated testing.

Ubuntu: Operating system for setting up the testing environment.

Damn Vulnerable Web Application (DVWA): A deliberately insecure application for practicing attacks.

SQLMap: Detects and exploits SQL Injection vulnerabilities.

Nikto: Web vulnerability scanner.

# Setup and Installation

1. Basic Ubuntu Setup

sudo apt update && sudo apt upgrade -y

sudo apt install curl wget git -y

2. Install LAMP Stack

   
3. Apache:

sudo apt install apache2 -y

sudo systemctl start apache2

sudo systemctl enable apache2

Checking if Apache is running: 
Open a web browser in Ubuntu and type http://localhost or http://127.0.0.1. The default Apache welcome page must be displayed for successful installation.

![Picture16](https://github.com/user-attachments/assets/c4db5b76-1ebb-4486-bc39-7b96df595558)

4. Installing MySQL (database server):

MySQL is used to store and manage large amounts of data efficiently. For any web application that handles dynamic content, a database is essential, and MySQL is a popular choice.

sudo apt install mysql-server -y

sudo systemctl start mysql 
sudo systemctl enable mysq

Secure the installation: 

Securing the installation of your web server and database (such as Apache and MySQL) is critical, especially when deploying applications that may handle sensitive data or be accessible over the internet.

sudo mysql_secure_installation
sudo apt install php libapache2-mod-php php-mysql -y

5. Installing PHP: Installing PHP and its necessary modules is crucial for developing dynamic web applications that can interact with databases and handle user input

sudo apt install php libapache2-mod-php php-mysql -y

6. Restart Apache to load PHP:
   
sudo systemctl restart apache2

7. Install DVWA

cd /var/www/html sudo git clone https://github.com/digininja/DVWA.git

8. Setting file permissions:

sudo chown -R www-data:www-data /var/www/html/DVWA

sudo chmod -R 755 /var/www/html/DVWA

 9. Configuring DVWA
   
10. Editing the config file: To setup user names, passwords, public and private keys

cd /var/www/html/DVWA/config

sudo cp config.inc.php.dist config.inc.php

11. Editing the config file: To setup user names, passwords, public and private keys

sudo nano config.inc.php

![Picture17](https://github.com/user-attachments/assets/00cd2d59-b0ff-4cf9-8272-22e20434d8e3)

6. Create a database:

CREATE DATABASE dvwa;

GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa_user'@'localhost' IDENTIFIED BY 'p@ssw0rd';

FLUSH PRIVILEGES;

EXIT;

Enabling DVWA: 

Open a web browser and go to http://localhost/DVWA/setup.php.
Click on “Create/Reset Database”

Installing Nikto:

 sudo apt install nikto -y 
 
Run Nikto to Scan the DVWA for Vulnerabilities: 
Use the following command to scan your web application for possible vulnerabilities and security issues: 

sudo nikto -h http://localhost/DVWA Nikto will run various tests and show any vulnerabilities.


![Picture18](https://github.com/user-attachments/assets/7df34a51-96ad-4b80-b1fc-0bfaedf59b95)

Installing SQLMap: 

SQLMap is an open-source penetration testing tool used to detect and exploit SQL injection vulnerabilities in web applications. 

# Updating Package Repository

sudo apt update

# Installing Required Dependencies

sudo apt install python3 python3-pip git -y

Cloning the SQLMap Repository

Use Git to clone the SQLMap repository from GitHub:
git clone https://github.com/sqlmapproject/sqlmap.git

This will create a directory named sqlmap in your current directory.

Navigating to the SQLMap Directory:

Change to the directory where SQLMap was cloned:

cd sqlmap
Running SQLMap
python3 sqlmap.py -h


# Testing Vulnerabilities

SQL Injection: Identify and exploit injection points using SQLMap.

python3 sqlmap.py -u "http://localhost/DVWA/vulnerabilities/sqli/?id=5&Submit=Submit#" --batch --cookie="PHPSESSID=your_session_id; security=low"

XSS: Inject and execute malicious JavaScript on DVWA.

<script>alert('You Have Been Hacked')</script>

# Countermeasures

Input Validation: Sanitize and validate user inputs to prevent malicious data entry.
Security Headers: Use headers like Content-Security-Policy (CSP) to restrict resources.
Authentication and Authorization:
Implement Multi-Factor Authentication (MFA).
Use Role-Based Access Control (RBAC).
Frequent Security Audits:
Perform penetration testing.
Use tools like OWASP ZAP to identify vulnerabilities early.
Lessons Learned
Importance of secure coding practices.
The value of ethical hacking in identifying vulnerabilities.
Continuous security monitoring is essential for evolving threats.

# Suggestions for Improvement

Integrate automated security scanning into CI/CD pipelines.
Expand use of advanced tools like Metasploit.
Incorporate real-world case studies to understand practical impacts.

# Conclusion

This project emphasizes the critical need for secure web development practices. By identifying vulnerabilities and applying robust countermeasures, developers and security professionals can strengthen the security posture of web applications.
