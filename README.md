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


## Summary

A deleted admin account can continue accessing authenticated pages using an existing active session (`PHPSESSID`). The application does not invalidate active sessions after account deletion.


## Description

When an admin account is deleted by the super admin, any active session associated with that account remains valid.
Even after deletion, the user can continue accessing the Admin Dashboard and other authenticated pages until the session expires.

The system does not re-validate the user's existence or status on each request.
This results in privilege retention after account revocation.


## Steps to Reproduce

1. Login as given Super Admin credentials.
2. Navigate to User Management > Add User
3. Create a Admin account
```bash
   testadmin
```
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

<img width="1920" height="1080" alt="Windows 10 x64-2026-02-19-16-01-27" src="https://github.com/user-attachments/assets/53559ed5-adf6-4aed-bb5e-b052b5f17b4b" />
<img width="1718" height="878" alt="kali-linux-2025 4-vmware-amd64-2026-02-19-16-02-32" src="https://github.com/user-attachments/assets/2bc57575-5400-4507-b94a-5be1a858ab72" />
<img width="1920" height="1080" alt="Windows 10 x64-2026-02-19-16-24-54" src="https://github.com/user-attachments/assets/2bc5e044-afbd-4470-886a-4300e1ea320c" />
<img width="1718" height="878" alt="kali-linux-2025 4-vmware-amd64-2026-02-19-16-03-44" src="https://github.com/user-attachments/assets/10c76796-c67f-44b6-9c87-c34eafad8830" />
<img width="1920" height="1080" alt="Windows 10 x64-2026-02-19-16-04-12" src="https://github.com/user-attachments/assets/59fbf876-0b2c-4537-8b20-425084c455c9" />
<img width="1718" height="878" alt="kali-linux-2025 4-vmware-amd64-2026-02-19-16-04-29" src="https://github.com/user-attachments/assets/f52de838-fc51-417b-b22f-d323b4679bc8" />
<img width="1718" height="878" alt="kali-linux-2025 4-vmware-amd64-2026-02-19-16-03-02" src="https://github.com/user-attachments/assets/ca52f797-04a1-44f9-b393-5d99635ae400" />
<img width="1718" height="878" alt="kali-linux-2025 4-vmware-amd64-2026-02-19-16-06-17" src="https://github.com/user-attachments/assets/b4944950-bc57-4620-b439-cda392b6a346" />

