# splunk-install-cli
Splunk installation CLI

Step 1: Download Splunk Enterprise

Download the appropriate package from Splunk (example shown for .tgz):

wget -O splunk.tgz https://download.splunk.com/products/splunk/releases/<VERSION>/linux/splunk-<VERSION>-Linux-x86_64.tgz


Or copy the installer to the server via SCP:

scp splunk.tgz user@server:/tmp

Step 2: Extract Splunk (Run as root)
cd /opt
tar -xvzf /tmp/splunk.tgz


Splunk will be installed to:

/opt/splunk

Step 3: Create the Splunk User and Group
groupadd splunk
useradd -m -g splunk splunk

Step 4: Set Ownership and Permissions
chown -R splunk:splunk /opt/splunk


This ensures Splunk does not run as root.

Step 5: Switch to the Splunk User
su - splunk

Step 6: Start Splunk for the First Time
/opt/splunk/bin/splunk start --accept-license


You will be prompted to create an admin username and password.

Step 7: Enable Splunk to Start at Boot (Run as root)

Exit back to root:

exit


Enable boot-start:

/opt/splunk/bin/splunk enable boot-start -user splunk

Step 8: Confirm Splunk Status

Switch back to the Splunk user and verify:

su - splunk
/opt/splunk/bin/splunk status

Step 9: Verify Web Access

Open a browser and navigate to:

http://<server-ip>:8000


Default management port: 8089
Default web port: 8000

Common CLI Commands
splunk start
splunk stop
splunk restart
splunk status
splunk show web-port

Best Practices

Never run Splunk as root

Use a dedicated splunk user and group

Monitor disk usage early ($SPLUNK_HOME/var)

Secure ports and credentials immediately

Version-control configs (props.conf, transforms.conf, etc.)

Notes

$SPLUNK_HOME defaults to /opt/splunk

Firewalls must allow port 8000 for web access

Additional configuration may be required for production environments
