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

<img width="3024" height="2920" alt="image" src="https://github.com/user-attachments/assets/df60a10f-8951-4bea-b081-e0e0e97cf6ef" />



### Evidence #2 — Active Directory User and Group

<img width="2351" height="2547" alt="image" src="https://github.com/user-attachments/assets/becba39b-62e5-4394-8b5c-2b3b52e2e8ee" />


### Evidence #3 — NTFS Permissions

<img width="3024" height="3302" alt="image" src="https://github.com/user-attachments/assets/10aecbd6-3602-4284-ac9a-3dfcc4772a92" />


### Evidence #4 — Share Permissions

<img width="3024" height="3375" alt="image" src="https://github.com/user-attachments/assets/f9395dd1-6d69-48b5-8b66-ef1035b43cee" />


### Evidence #5 — Successful File Creation

<img width="3024" height="2517" alt="image" src="https://github.com/user-attachments/assets/bcf449c3-c61b-4c0b-9974-a6503f9a7e29" />


## Skills Demonstrated

`Active Directory` `NTFS Permissions` `SMB/UNC` `Windows Server` `Access Control` `Troubleshooting` `User Account Management` `Escalation`

