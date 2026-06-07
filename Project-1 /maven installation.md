# Maven Installation & Configuration on Ubuntu/Linux

This setup installs Apache Maven manually under `/opt/maven` and configures environment variables globally.

---

# Step 1 — Switch to Root User

```bash
sudo su -
```

---

# Step 2 — Create Maven Directory

```bash
mkdir -p /opt/maven
cd /opt/maven
```

---

# Step 3 — Install Required Package

Maven package is downloaded as a ZIP file, so install `unzip`.

```bash
apt update
apt install unzip -y
```

---

# Step 4 — Download Apache Maven

Download Maven 3.9.16:

```bash
wget https://dlcdn.apache.org/maven/maven-3/3.9.16/binaries/apache-maven-3.9.16-bin.zip
```

---

# Step 5 — Extract Maven

```bash
unzip apache-maven-3.9.16-bin.zip
```

After extraction, Maven will be available at:

```text
/opt/maven/apache-maven-3.9.16
```

---

# Step 6 — Verify Maven Installation Directory

Run:

```bash
find / -name "apache-maven*" 2>/dev/null
```

Expected output:

```text
/opt/maven/apache-maven-3.9.16
```

---

# Step 7 — Configure Maven Environment Variables

Open the bash profile:

```bash
vi ~/.bash_profile
```

Press:

```text
i
```

to enter INSERT mode.

---

# Step 8 — Add Maven Environment Variables

Add the following lines at the bottom of the file:

```bash
export M2_HOME=/opt/maven/apache-maven-3.9.16
export M2=$M2_HOME/bin
export PATH=$PATH:$M2
```

---

# Step 9 — Save the File

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

# Step 10 — Reload Profile

Apply changes immediately:

```bash
source ~/.bash_profile
```

---

# Step 11 — Verify Maven Installation

Run:

```bash
mvn -version
```

Expected output:

```text
Apache Maven 3.9.16
Maven home: /opt/maven/apache-maven-3.9.16
Java version: 17
```

---

# Environment Variables Explanation

| Variable  | Purpose                              |
| --------- | ------------------------------------ |
| `M2_HOME` | Maven installation directory         |
| `M2`      | Maven binary path                    |
| `PATH`    | Allows `mvn` command to run globally |

---

# Additional Verification Commands

Check Maven path:

```bash
echo $M2_HOME
```

Check executable location:

```bash
which mvn
```

Check PATH variable:

```bash
echo $PATH
```

---

# Final Installed Maven Path

```text
/opt/maven/apache-maven-3.9.16
```

---

# Production Best Practice

In enterprise environments, environment variables are usually configured system-wide using:

```bash
/etc/profile.d/maven.sh
```

Example:

```bash
vi /etc/profile.d/maven.sh
```

Add:

```bash
export M2_HOME=/opt/maven/apache-maven-3.9.16
export PATH=$PATH:$M2_HOME/bin
```

Apply:

```bash
source /etc/profile.d/maven.sh
```

This makes Maven available for all users on the server.
