# Jenkins LTS Installation on Ubuntu/Linux

This setup installs the Jenkins Long-Term Support (LTS) version using the official Jenkins repository.

LTS versions are recommended in enterprise environments because they are:

* Stable
* Secure
* Well-tested
* Production-ready

---

# Prerequisites

Before installing Jenkins, ensure:

* Java 17 or Java 21 is installed
* Internet access is available
* Ubuntu/Debian-based OS is used

Verify Java:

```bash id="ppsrhk"
java -version
```

---

# Step 1 — Create Keyrings Directory

Run:

```bash id="h5m7uw"
sudo mkdir -p /etc/apt/keyrings
```

---

# Why This Step?

APT uses GPG keys to verify package authenticity.

The directory:

```text id="t7tavl"
/etc/apt/keyrings
```

stores trusted repository keys securely.

---

# Step 2 — Download Jenkins Repository GPG Key

Run:

```bash id="0n3mv2"
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
```

---

# What This Does

This command:

* Downloads Jenkins official signing key
* Stores it locally
* Allows Ubuntu to trust Jenkins packages

---

# Command Breakdown

| Part                    | Purpose                        |
| ----------------------- | ------------------------------ |
| `wget`                  | Downloads file from internet   |
| `-O`                    | Saves file with specified name |
| `/etc/apt/keyrings/...` | Key storage location           |

---

# Step 3 — Add Jenkins Repository

Run:

```bash id="8lgf48"
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

# What This Does

This command:

* Adds Jenkins official package repository
* Enables Ubuntu to download Jenkins packages directly

---

# Repository File Created

```text id="qbggfx"
/etc/apt/sources.list.d/jenkins.list
```

---

# Step 4 — Update Package Repository

Run:

```bash id="w8if6n"
sudo apt update
```

---

# Why This Step?

Ubuntu refreshes package metadata and detects:

* Jenkins package
* Latest versions
* Dependencies

Without this step:

* Jenkins package may not be found

---

# Step 5 — Install Jenkins

Run:

```bash id="pf3o8w"
sudo apt install jenkins -y
```

---

# What Happens During Installation

Ubuntu automatically:

* Downloads Jenkins
* Creates Jenkins user
* Installs service files
* Configures systemd service
* Enables Jenkins startup service

---

# Step 6 — Verify Jenkins Service

Run:

```bash id="9jx6th"
sudo systemctl status jenkins
```

Expected:

```text id="zv3rce"
active (running)
```

---

# Step 7 — Enable Jenkins on Boot

Run:

```bash id="6s8q1v"
sudo systemctl enable jenkins
```

---

# Why This Step?

Ensures Jenkins starts automatically after:

* Reboot
* Server restart
* EC2 restart

---

# Step 8 — Start Jenkins Service

Run:

```bash id="x4m1yh"
sudo systemctl start jenkins
```

---

# Step 9 — Check Jenkins Port

Run:

```bash id="j9rm7x"
sudo netstat -tulnp | grep 8080
```

Expected:

```text id="r7ltc4"
8080
```

---

# Step 10 — Open Jenkins in Browser

Access:

```text id="h24x4z"
http://YOUR_SERVER_IP:8080
```

Example:

```text id="l8stlq"
http://13.233.xx.xx:8080
```

---

# IMPORTANT — AWS Security Group

Allow inbound traffic:

| Port | Purpose    |
| ---- | ---------- |
| 8080 | Jenkins UI |
| 22   | SSH        |

---

# Step 11 — Get Initial Jenkins Password

Run:

```bash id="8hdp54"
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy the password.

Paste it into Jenkins UI.

---

# Step 12 — Install Suggested Plugins

Choose:

```text id="7k6gy9"
Install Suggested Plugins
```

Jenkins installs:

* Git plugin
* Pipeline plugin
* Docker plugin
* Maven integration
* SSH plugins

---

# Step 13 — Create Admin User

Set:

* Username
* Password
* Email

---

# Step 14 — Verify Jenkins Home Directory

Run:

```bash id="5tx9is"
ls /var/lib/jenkins
```

This is Jenkins home directory.

---

# Important Jenkins Directories

| Directory                    | Purpose        |
| ---------------------------- | -------------- |
| `/var/lib/jenkins`           | Jenkins Home   |
| `/var/log/jenkins`           | Logs           |
| `/etc/default/jenkins`       | Jenkins config |
| `/var/lib/jenkins/workspace` | Job workspace  |

---

# Useful Jenkins Commands

## Start Jenkins

```bash id="ab9w5y"
sudo systemctl start jenkins
```

## Stop Jenkins

```bash id="3m0tmr"
sudo systemctl stop jenkins
```

## Restart Jenkins

```bash id="mk8m5w"
sudo systemctl restart jenkins
```

## Check Status

```bash id="3mnq5v"
sudo systemctl status jenkins
```

---

# Verify Installed Version

Run:

```bash id="qaxv7v"
jenkins --version
```

OR

```bash id="hns8bn"
dpkg -l | grep jenkins
```

---

# Enterprise Best Practice

In production:

* Use Jenkins LTS only
* Run Jenkins behind NGINX
* Configure HTTPS
* Use Jenkins agents
* Store backups
* Use external database if needed
* Integrate with LDAP/SSO

---

# Jenkins Architecture in Real Projects

```text id="d5mz5h"
Developer
   ↓
GitHub
   ↓
Jenkins Pipeline
   ↓
Maven Build
   ↓
SonarQube Scan
   ↓
Docker Build
   ↓
Kubernetes Deployment
```

---


