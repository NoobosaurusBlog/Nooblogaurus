---
layout: default
title: SMBMap Cheat Sheet
permalink: /cheat-sheets/smbmap/
---

# SMBMap Cheat Sheet

## **1. Basic Terminology**
- **SMBMap**: A tool to enumerate SMB shares, permissions, and perform file operations across Windows domains.
- **SMB (Server Message Block)**: Protocol for shared access to files, printers, and ports.
- **Share**: A network folder or resource exposed over SMB (e.g., `C$`, `ADMIN$`).
- **Null Session**: Connecting to SMB without credentials (often restricted in modern systems).

---
## **2. Basic Usage**

### General Syntax
```bash
smbmap [options] -H <IP>
```

### Common Flags

<table>
  <thead>
    <tr>
      <th>Flag</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>-H &lt;IP&gt;</code></td><td>Target IP address.</td></tr>
    <tr><td><code>-u &lt;user&gt;</code></td><td>Username (use <code>-u ''</code> for null session).</td></tr>
    <tr><td><code>-p &lt;password&gt;</code></td><td>Password.</td></tr>
    <tr><td><code>-d &lt;domain&gt;</code></td><td>Domain/workgroup (use <code>.</code> for local workgroup).</td></tr>
    <tr><td><code>-s &lt;share&gt;</code></td><td>Specific share to target.</td></tr>
    <tr><td><code>-P &lt;port&gt;</code></td><td>Custom SMB port (default: 445).</td></tr>
    <tr><td><code>-x &lt;command&gt;</code></td><td>Execute a command on the target.</td></tr>
    <tr><td><code>-R</code></td><td>Recursive directory listing (with read permissions).</td></tr>
    <tr><td><code>--download &lt;file&gt;</code></td><td>Download a file from the share.</td></tr>
    <tr><td><code>--upload &lt;src&gt; &lt;dst&gt;</code></td><td>Upload a file to the share.</td></tr>
    <tr><td><code>--users</code></td><td>Enumerate users.</td></tr>
    <tr><td><code>--admin</code></td><td>Check if the user has admin access.</td></tr>
    <tr><td><code>-v</code></td><td>Verbose output.</td></tr>
  </tbody>
</table>

---

## **3. Practical Examples**

### **Authentication**
**Null Session (Guest Access):**
```bash
smbmap -u '' -p '' -d . -H 192.168.1.1
```

**Authenticated Access:**
```bash
smbmap -u admin -p 'Password123!' -d WORKGROUP -H 192.168.1.1
```

---

### **Share Enumeration**
**List All Shares:**
```bash
smbmap -H 192.168.1.1
```

**Check Specific Share:**
```bash
smbmap -H 192.168.1.1 -s 'C$'
```

**Check Shares with Full Permissions:**
```bash
smbmap -H 192.168.1.1 -R
```

---

### **File Operations**
**Download a File:**
```bash
smbmap -u admin -p 'Password123!' -H 192.168.1.1 --download 'C$\secret.txt'
```

**Upload a File:**
```bash
smbmap -u admin -p 'Password123!' -H 192.168.1.1 --upload '/tmp/payload.exe' 'C$\Windows\Temp\payload.exe'
```

**Recursive Directory Listing:**
```bash
smbmap -u guest -p '' -H 192.168.1.1 -R 'Documents'
```

---

### **Command Execution**
**Run a Command (e.g., `whoami`):**
```bash
smbmap -u admin -p 'Password123!' -H 192.168.1.1 -x 'whoami'
```

**Execute a PowerShell Script:**
```bash
smbmap -u admin -p 'Password123!' -H 192.168.1.1 -x 'powershell -c "Get-Process"'
```

---

### **User & Permission Checks**
**Enumerate Users:**
```bash
smbmap -H 192.168.1.1 --users
```

**Check Admin Access:**
```bash
smbmap -u admin -p 'Password123!' -H 192.168.1.1 --admin
```

---

## **4. Advanced Techniques**

### **Port Redirection**
Target non-standard SMB port (e.g., 8445):
```bash
smbmap -H 192.168.1.1 -P 8445
```

### **Read-Only Checks**
Check if shares are writable:
```bash
smbmap -u guest -p '' -H 192.168.1.1 --no-write-check
```

### **Brute-Force Share Names**
Combine with `enum4linux` or `nmap` scripts for share discovery.

---

## **5. Useful Tips**
- Use `-v` for debugging connection issues.
- Combine with `crackmapexec` for lateral movement.
- For interactive sessions, use `smbclient` (e.g., `smbclient //192.168.1.1/C$ -U admin`).
- Always check permissions (`--admin`, `-R`) before attempting writes.

---

## **6. References**
- [SMBMap GitHub](https://github.com/ShawnDEvans/smbmap)
