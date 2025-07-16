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
