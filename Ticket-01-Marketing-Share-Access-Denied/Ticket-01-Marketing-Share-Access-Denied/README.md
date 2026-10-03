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

![Marketing Department Share](evidence/01-marketing-share.png)

### Evidence #2 — Active Directory User and Group

![Active Directory User and Group](evidence/02-active-directory-user-group.png)

### Evidence #3 — NTFS Permissions

![NTFS Permissions](evidence/03-ntfs-permissions.png)

### Evidence #4 — Share Permissions

![Share Permissions](evidence/04-share-permissions.png)

### Evidence #5 — Successful File Creation

![Successful File Creation](evidence/05-successful-file-creation.png)

## Skills Demonstrated

`Active Directory` `NTFS Permissions` `SMB/UNC` `Windows Server` `Access Control` `Troubleshooting` `User Account Management` `Escalation`

