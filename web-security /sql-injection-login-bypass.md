# SQL Injection – Login Bypass

## 🧩 Lab Description

This lab contains a SQL injection vulnerability in the login functionality.

---

## 💥 Vulnerability

SQL Injection allows bypassing authentication.

---

## 🛠️ Tools Used

* Burp Suite

---

## ⚡ Payload Used

' OR 1=1--

---

## 🔍 Steps

1. Intercept login request using Burp Suite
2. Modify the username parameter
3. Insert payload: ' OR 1=1--
4. Forward the request

---

## ✅ Result

Successfully logged in without valid credentials.

---

## 🚨 Impact

Attackers can bypass authentication and gain unauthorized access.

---
