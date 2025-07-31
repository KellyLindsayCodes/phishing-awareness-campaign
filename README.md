# Phishing Campaign Simulation (GoPhish + MailHog)

## Live Pages

## 🎯Project Overview 
This project is a phishing simulation training exercise. A controlled phishing email is sent to employees of a fictional company, SecureNet Systems. If recipients fall for the simulated attack, they are required to complete a phishing awareness training module.

## 📚 Table of Contents
- Requirements
- Environment Setup
- Creating Your Campaign
- Email & Landing Pages
- User Group & Launch
- Tracking Engagement

## 🧰 Requirements
- Kali Linux VM
- GoPhish downloaded from: https://github.com/gophish/gophish/releases/v0.12.1
- MailHog downloaded from: https://github.com/mailhog/MailHog/releases/v1.0.0


## ⚙️ Environment Setup
1. Open the terminal in your Kali Linux VM
2.Start GoPhish
```
cd /path/to/gophish
chmod +x gophish
sudo ./gophish
```
2. Start MailHog
```
cd /path/to/MailHog
chmod +x MailHog
./MailHog
```
3. Access Dashboards
```
GoPhish: https://127.0.0.1:3333 (default: admin/gophish)

MailHog: http://127.0.0.1:8025
```
4. Find Your VM's IP Address
```
ip addr show
#or
ifconfig
```

### Setting up a Sending Profile
1. In the GoPhish admin panel, navigate to Sending Profiles
2. Click + New Profile
3. Configure the profile with these settings:
- Name: SecureNet Systems Security Alerts
- From: security-alerts@securenetsystems.com
- Host: localhost:1025 (MailHog's default SMTP port)
- Interface Type: SMTP
- Ignore Certificate Errors: Checked
- Leave username/password blank for MailHog testing
4. Click Send Test Email to verify the connection works
5. Check the MailHog interface to confirm receipt
6. Save the profile

### Creating an Email Template
1. Go to Email Templates in GoPhish
2. Click + New Template
3. Configure the template:
- Name: SecureNet Systems - Account Verification
- Subject: Your Account Requires Immediate Attention
- HTML: Copy and paste the HTML from the email-template.html file in this repository
- Attachments: None needed for this simulation
- Ensure {{.URL}} placeholder exists in your HTML where the phishing link should go
4. Click Save Template

### Building a Landing Page 
1. Go to Landing Pages in GoPhish
2. Click + New Page
3. Configure the page:
- Name: SecureNet Systems Login Page
- HTML: Copy and paste the HTML from landing-page.html in this repository
- Capture Submitted Data: Checked
- Redirect URL: 
4. Click Save Page

### Creating a User Group
1. Go to Users & Groups in GoPhish
2. Click + New Group
3. Name the group (e.g., "Phishing Test")
4. Add test users:
- You can import from CSV or add manually
- For testing, add your own email address or create test accounts
5. Click Save Group

### Launching Your Campaign
1. Go to Campaigns in GoPhish
2. Click + New Campaign
3. Configure the campaign:
- Name: SecureNet Systems Security Test
- Email Template: Select your "Security Alert - Account Verification" template
- Landing Page: Select your "SecureNet Systems Login Page"
- URL: Enter http://YOUR-VM-IP-ADDRESS (use the IP address you found earlier)
- Launch Date: Schedule or launch immediately
- Sending Profile: Select "SecureNet Systems Security Alerts"
- Groups: Select your test user group
4. Click Launch Campaign

## Tracking Results
Once campaign is launched, progress can be monitored by:
1. Go to the Campaigns dashboard in GoPhish
2. Click on your active campaign
3. View statistics on:
- Emails sent/opened
- Links clicked
- Credentials submitted
- Users who visited the educational page
4. Click on individual results to see detailed information about each target's interaction with the campaign

## Screenshots 
### Phishing Email Template sent to recipients
![alt text](/images/image.png)
### Index page recipients are taken to if data submitted
![alt text](/images/image-1.png)
### Phishing training module for recipients to learn from
![alt text](/images/image-2.png)
### GoPhish Dashboard and recipient data
![alt text](/images/image-3.png)
### MailHog Shows Evidence of Email Sent
![alt text](/images/image-4.png)

## Acknowledgements
Some training module questions were adapted from the original github https://github.com/NoisyPlatypus/itsolutions.
This project was developed as part of a group assessment for a cybersecurity course. 
