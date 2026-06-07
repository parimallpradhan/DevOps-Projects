# Java Installation & Configuration on Ubuntu/Linux

This setup installs Java Runtime Environment (JRE) required for:

* Jenkins
* Maven
* SonarQube
* Java applications
* Spring Boot projects

In enterprise DevOps environments, Java is mandatory because Jenkins and Maven run on Java.

---

# Step 1 — Update Package Repository

Run:

```bash
sudo apt update
```

---

# Why We Run This

Ubuntu maintains a local package index.

`apt update` refreshes the package repository information so the system knows:

* latest package versions
* security updates
* dependency updates

Without this step, old package versions may get installed.

---

# Step 2 — Install Java

Run:

```bash
sudo apt install fontconfig openjdk-21-jre -y
```

---

# Explanation of Packages

| Package          | Purpose                                          |
| ---------------- | ------------------------------------------------ |
| `openjdk-21-jre` | Installs Java Runtime Environment version 21     |
| `fontconfig`     | Required by Java applications for font rendering |
| `-y`             | Automatically answers YES during installation    |

---

# What is JRE?

JRE = Java Runtime Environment

It is used to:

* Run Java applications
* Run Jenkins
* Run Spring Boot JAR files
* Execute Maven builds

---

# Difference Between JDK and JRE

| Component | Purpose                           |
| --------- | --------------------------------- |
| JRE       | Only runs Java applications       |
| JDK       | Runs + develops Java applications |

---

# Which One Should You Install?

| Use Case                | Install         |
| ----------------------- | --------------- |
| Jenkins Server          | JRE is enough   |
| Java Development        | JDK required    |
| Maven Build Server      | JDK recommended |
| Spring Boot Development | JDK required    |

---

# Recommended for DevOps

Instead of only JRE, install JDK because:

* Maven compilation requires JDK
* Jenkins pipelines often compile code
* SonarQube scanners use Java compiler tools

Recommended command:

```bash
sudo apt install openjdk-21-jdk -y
```

---

# Step 3 — Verify Java Installation

Run:

```bash
java -version
```

Expected output:

```text
openjdk version "21"
```

Example:

```text
openjdk version "21.0.2" 2026-01-16
OpenJDK Runtime Environment
OpenJDK 64-Bit Server VM
```

---

# Step 4 — Verify Java Binary Location

Run:

```bash
which java
```

Example output:

```text
/usr/bin/java
```

---

# Step 5 — Verify Installed Java Packages

Run:

```bash
dpkg -l | grep openjdk
```

This shows all installed Java-related packages.

---

# Step 6 — Check JAVA_HOME (Optional)

Run:

```bash
echo $JAVA_HOME
```

If blank, configure it manually.

---

# Step 7 — Configure JAVA_HOME (Recommended)

Find Java installation path:

```bash
readlink -f $(which java)
```

Example output:

```text
/usr/lib/jvm/java-21-openjdk-amd64/bin/java
```

Java Home becomes:

```text
/usr/lib/jvm/java-21-openjdk-amd64
```

---

# Step 8 — Open bash_profile

```bash
vi ~/.bash_profile
```

Press:

```text
i
```

to enter INSERT mode.

---

# Step 9 — Add Java Environment Variables

Add:

```bash
export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
export PATH=$PATH:$JAVA_HOME/bin
```

---

# Step 10 — Save File

Press:

```text
ESC
```

Then type:

```text
:wq
```

Press Enter.

---

# Step 11 — Reload Profile

Run:

```bash
source ~/.bash_profile
```

---

# Step 12 — Verify JAVA_HOME

Run:

```bash
echo $JAVA_HOME
```

Expected:

```text
/usr/lib/jvm/java-21-openjdk-amd64
```

---

# Step 13 — Verify Java Compiler

If JDK installed:

```bash
javac -version
```

Expected:

```text
javac 21
```

---

# Final Verification Commands

## Java Version

```bash
java -version
```

## Java Compiler

```bash
javac -version
```

## Java Home

```bash
echo $JAVA_HOME
```

## Java Binary Path

```bash
which java
```

---

# Real Enterprise Best Practice

In enterprise Linux servers, Java variables are usually configured globally:

Create:

```bash
sudo vi /etc/profile.d/java.sh
```

Add:

```bash
export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
export PATH=$PATH:$JAVA_HOME/bin
```

Apply:

```bash
source /etc/profile.d/java.sh
```

This makes Java available for:

* Jenkins
* All users
* Automation scripts
* CI/CD pipelines

---

# Why Java is Important in Your DevOps Stack

| Tool        | Java Required? |
| ----------- | -------------- |
| Jenkins     | Yes            |
| Maven       | Yes            |
| SonarQube   | Yes            |
| Spring Boot | Yes            |
| Tomcat      | Yes            |
| Gradle      | Yes            |

---

# Recommended Version for DevOps

| Tool            | Recommended Java |
| --------------- | ---------------- |
| Jenkins         | Java 17 or 21    |
| SonarQube       | Java 17          |
| Spring Boot 3.x | Java 17+         |

Java 21 is currently a strong enterprise choice for modern DevOps environments.
