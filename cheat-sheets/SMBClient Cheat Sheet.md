---
layout: default
title: SMBClient Cheat Sheet
permalink: /cheat-sheets/smbclient/
---

# smbclient Cheat Sheet

## **1. Basic Terminology**
- **SMB (Server Message Block)**: Protocol for file sharing, printers, and network communication.
- **smbclient**: Command-line tool to interact with SMB shares (similar to FTP).
- **Share**: A network folder or resource exposed via SMB (e.g., `C$`, `Documents`).
- **Workgroup/Domain**: Network group for shared resources (default: `WORKGROUP`).

---

## 2. Basic Usage**

### General Syntax
```bash
smbclient [options] //<server>/<share>
```
Replace `server` with the name or IP address of the server hosting the file share, and `share` with the name of the file share.

You will be prompted for your username and password for the file share. Once authenticated, you will be presented with a command prompt where you can enter various commands to interact with the file share.

### Common Options

<table>
  <thead>
    <tr>
      <th>Option</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>-U &lt;user&gt;[%pass]</code></td><td>Username and password (e.g., <code>-U admin%Password123</code>).</td></tr>
    <tr><td><code>-W &lt;domain&gt;</code></td><td>Workgroup/domain name (default: <code>WORKGROUP</code>).</td></tr>
    <tr><td><code>-I &lt;IP&gt;</code></td><td>Server IP address (bypasses DNS).</td></tr>
    <tr><td><code>-p &lt;port&gt;</code></td><td>Custom port (default: 445 for SMB over TCP/IP).</td></tr>
    <tr><td><code>-N</code></td><td>No password prompt (use with empty or guest access).</td></tr>
    <tr><td><code>-E</code></td><td>Hide password prompt output.</td></tr>
    <tr><td><code>-c &lt;command&gt;</code></td><td>Execute a command non-interactively (e.g., <code>-c 'ls'</code>).</td></tr>
    <tr><td><code>-A &lt;creds-file&gt;</code></td><td>Load credentials from a file.</td></tr>
    <tr><td><code>-m &lt;max-protocol&gt;</code></td><td>Set max SMB protocol (e.g., <code>-m SMB3</code>).</td></tr>
    <tr><td><code>-d &lt;debug-level&gt;</code></td><td>Debug verbosity (0-10).</td></tr>
  </tbody>
</table>

---

## **3. Interactive Commands**

Once connected, use these commands:

<table>
  <thead>
    <tr>
      <th>Command</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>ls</code></td><td>List files/directories.</td></tr>
    <tr><td><code>cd &lt;dir&gt;</code></td><td>Change directory.</td></tr>
    <tr><td><code>get &lt;file&gt;</code></td><td>Download a file.</td></tr>
    <tr><td><code>put &lt;file&gt;</code></td><td>Upload a file.</td></tr>
    <tr><td><code>mget &lt;pattern&gt;</code></td><td>Download multiple files (e.g., <code>mget *.txt</code>).</td></tr>
    <tr><td><code>mput &lt;pattern&gt;</code></td><td>Upload multiple files.</td></tr>
    <tr><td><code>rm &lt;file&gt;</code></td><td>Delete a file.</td></tr>
    <tr><td><code>mkdir &lt;dir&gt;</code></td><td>Create a directory.</td></tr>
    <tr><td><code>rmdir &lt;dir&gt;</code></td><td>Delete a directory.</td></tr>
    <tr><td><code>pwd</code></td><td>Print current directory.</td></tr>
    <tr><td><code>recurse</code></td><td>Toggle recursive mode for <code>mget</code>/<code>mput</code>.</td></tr>
    <tr><td><code>mask &lt;filter&gt;</code></td><td>Set a file filter (e.g., <code>mask *.docx</code>).</td></tr>
    <tr><td><code>tar</code></td><td>Create/extract tar backups (e.g., <code>tar c backup.tar *</code>).</td></tr>
    <tr><td><code>exit</code></td><td>Quit smbclient.</td></tr>
  </tbody>
</table>

---

## **4. Practical Examples**

### **Connection**
**Anonymous/Guest Access:**
```bash
smbclient //192.168.1.10/public -N
```

**Authenticated Access:**
```bash
smbclient //192.168.1.10/C$ -U admin%Password123
```

**Specify Domain/Workgroup:**
```bash
smbclient //SERVER/Share -W CORP -U user%pass
```

---

### **File Operations**
**Download a File:**
```bash
smbclient //192.168.1.10/Data -U user%pass -c "get report.docx"
```

**Upload All TXT Files:**
```bash
smbclient //192.168.1.10/Data -U user%pass -c "mask *.txt; recurse; mput *.txt"
```

**Delete a File:**
```bash
smbclient //192.168.1.10/Data -U user%pass -c "rm oldfile.zip"
```

---

### **Directory Management**
**Create a Directory:**
```bash
smbclient //192.168.1.10/Data -U user%pass -c "mkdir Projects"
```

**Recursive Download:**
```bash
smbclient //192.168.1.10/Data -U user%pass -c "recurse; prompt; mget *"
```

---

### **Non-Interactive Mode**
**List Shares via Script:**
```bash
smbclient -L 192.168.1.10 -U admin%Password123 -N -I 192.168.1.10
```

**Backup Directory to Tar:**
```bash
smbclient //192.168.1.10/Backup -U user%pass -c "tar c backup.tar Documents"
```

---

## **5. Advanced Techniques**

### **Mounting Shares**
Use `mount.cifs` (Linux) or `net use` (Windows) for persistent access:
```bash
sudo mount -t cifs //192.168.1.10/Data /mnt/share -o user=admin,pass=Password123
```

### **Brute-Force Share Names**
Combine with tools like `nmap` or `enum4linux`:
```bash
enum4linux -S 192.168.1.10
```

### **Using a Credentials File**
Create `creds.txt`:
```ini
username = admin
password = Password123
domain = CORP
```
Then:
```bash
smbclient //192.168.1.10/C$ -A creds.txt
```

---

## **6. Troubleshooting**

- **Connection Refused**: Check firewall rules, SMB port (445/139), and service status.
- **Access Denied**: Verify credentials, share permissions, and user privileges.
- **Protocol Errors**: Use `-m SMB2` or `-m SMB3` to enforce protocol version.

---

## **7. References**
- [smbclient Man Page](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html)
