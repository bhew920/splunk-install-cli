# splunk-install-cli
Splunk installation CLI

---
## 🚀 Splunk Enterprise Installation via CLI (Linux)

This guide walks through installing Splunk Enterprise on a Linux server using the command line, following Splunk best practices for security, permissions, and service management.

---
## 🧰 Prerequisites

Before you begin, make sure you have:

🐧 Linux server (RHEL, CentOS, Ubuntu, Amazon Linux)

🔑 Root or sudo access

🌐 Internet access or Splunk installer locally available

💾 Minimum system requirements met

---
## 📥 Step 1: Download Splunk Enterprise

Download the installer (example using .tgz):

wget -O splunk.tgz https://download.splunk.com/products/splunk/releases/<VERSION>/linux/splunk-<VERSION>-Linux-x86_64.tgz


Or copy it to the server:

scp splunk.tgz user@server:/tmp

---
## 📦 Step 2: Extract Splunk (Run as root)
cd /opt
tar -xvzf /tmp/splunk.tgz


📁 Default install path:

/opt/splunk

---
## 👤 Step 3: Create the Splunk User & Group
groupadd splunk
useradd -m -g splunk splunk


🔐 This ensures Splunk runs as a non-root user.

---
## 🔑 Step 4: Set Ownership & Permissions
chown -R splunk:splunk /opt/splunk

---
## 🔄 Step 5: Switch to the Splunk User
su - splunk

---
## ▶️ Step 6: Start Splunk (First Run)
/opt/splunk/bin/splunk start --accept-license


📝 You’ll be prompted to create an admin username and password.

---
## 🔁 Step 7: Enable Splunk at Boot (Run as root)

Exit back to root:

exit


Enable boot-start:

/opt/splunk/bin/splunk enable boot-start -user splunk

---
## ✅ Step 8: Verify Splunk Status
su - splunk
/opt/splunk/bin/splunk status

---
## 🌐 Step 9: Access the Splunk Web UI

Open your browser and navigate to:

http://<server-ip>:8000


🔌 Common Ports:

Web UI: 8000

Management: 8089

🖥️ Common CLI Commands
splunk start
splunk stop
splunk restart
splunk status
splunk show web-port

⭐ Best Practices

🚫 Never run Splunk as root

👤 Always use a dedicated splunk user

📊 Monitor disk usage ($SPLUNK_HOME/var)

🔒 Secure credentials and open ports early

🗂️ Version-control configs (props.conf, transforms.conf)

📝 Notes

$SPLUNK_HOME defaults to /opt/splunk

Ensure firewall rules allow port 8000

Production deployments may require additional tuning
