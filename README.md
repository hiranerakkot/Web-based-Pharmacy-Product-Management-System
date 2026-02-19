# Product: Web-based-Pharmacy-Product-Management-System

## Product Information
Vendor Homepage: [link](https://www.sourcecodester.com/)

Software Link: [link](https://www.sourcecodester.com/php/17883/web-based-product-alert-system.html)

Affected Version: [<= v1.0]

BUG Author: Hiran

## Title
Broken Session Invalidation After Account Deletion

## Severity
High

## Vulnerability Type
- Broken Session Management
- Broken Access Control

---

## Summary

A deleted admin account can continue accessing authenticated pages using an existing active session (`PHPSESSID`). The application does not invalidate active sessions after account deletion.

---

## Description

When an admin account is deleted by the super admin, any active session associated with that account remains valid.
Even after deletion, the user can continue accessing the Admin Dashboard and other authenticated pages until the session expires.

The system does not re-validate the user's existence or status on each request.
This results in privilege retention after account revocation.

---

## Steps to Reproduce

1. Login as given Super Admin credentials.
2. Navigate to User Management > Add User
3. Create a Admin account
   ```bash
   testadmin
4. Login as `testadmin` in another browser or private window.
5. In Super Admin dashboard, navigate to User Management > Admin Record
6. Delete newly created `testadmin` account.
7. In `testadmin` browser/windows, You can still access and can view updated details.
8. Captured `PHPSESSID` of `testadmin` using Cookie Editor.
9. Using Terminal executed the command:

  ```bash
  curl -i http://TARGET/product_expiry/index.php \
  -H "Cookie: PHPSESSID=SESSION_ID"
```
10. Got 200 OK, Welcome to Admin Dashboard

## Proof of Concept
