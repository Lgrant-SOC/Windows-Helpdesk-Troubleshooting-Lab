# INC-001 — Marketing Network Share Access Denied

**Category:** Access / File Share
**Priority:** P3 — Medium
**User:** Alex Rivera
**Environment:** Windows 10 Pro + Windows Server 2022 / Active Directory

## Issue

Alex Rivera reported that he could access the **Marketing network share** but could not create or modify files.

## Troubleshooting

* Tested access to the Marketing share using the server hostname and IP address.
* Verified the user's account in **Active Directory Users and Computers**.
* Reviewed the user's account settings.
* Verified `GG-Marketing-Dept` membership and NTFS permissions.
* Reviewed the **Share Permissions** on the Marketing folder.
* Retested access after correcting the permissions.

## Finding

The user had **Modify** permissions through `GG-Marketing-Dept` at the NTFS level, but the **Share Permission** was restricting access.

The user's Active Directory account also had **"User must change password at next logon"** enabled, which contributed to the initial authentication issue.

## Resolution

* Cleared **"User must change password at next logon"** for `arivera`.
* Updated the Marketing share permissions to allow **Read + Change** while leaving **Full Control** disabled.
* Retested the share.
* Successfully created `Alex_Rivera_Access_Test.txt`.

## Escalation

If access remained unsuccessful after verifying the user's account and permissions, the issue would be escalated to the **Windows/AD or File Services team** to verify server-side access controls and share configuration.

## Evidence

### Evidence #1 — Marketing Department Share

<img width="3024" height="2920" alt="image" src="https://github.com/user-attachments/assets/ce0dc903-6fee-4e66-8916-5ec3a0543c6c" />


### Evidence #2 — Active Directory User and Group

<img width="2850" height="3087" alt="image" src="https://github.com/user-attachments/assets/b20b8bd7-f356-4a73-af3a-7d9c517631ed" />


### Evidence #3 — NTFS Permissions

<img width="3024" height="3302" alt="image" src="https://github.com/user-attachments/assets/ef00aefb-bc1e-4def-bd1b-770c9bd9f7e3" />


### Evidence #4 — Share Permissions

<img width="3024" height="3375" alt="image" src="https://github.com/user-attachments/assets/3d347d71-4bd1-42cf-be41-6f04247a9430" />


### Evidence #5 — Successful File Creation

<img width="3024" height="2517" alt="image" src="https://github.com/user-attachments/assets/4b9d0c14-92d8-45a8-af7a-e11a188d45fe" />


### Supporting Evidence #6 — Active Directory Account Settings

<img width="3024" height="2357" alt="image" src="https://github.com/user-attachments/assets/05a7e05e-f449-45c9-9e7e-9595937a4988" />



## Skills Demonstrated

`Active Directory` `NTFS Permissions` `SMB/UNC` `Windows Server` `Access Control` `Troubleshooting` `User Account Management` `Escalation`

