# INC-002 — Internal Server DNS/Network Connectivity Failure

**Category:** Network / Connectivity
**Priority:** P2 — High
**User:** Alex Rivera
**Environment:** Windows 10 Pro + Windows Server 2022 / Active Directory
**Affected Resource:** `\\192.168.56.106\Marketing`

## Issue

Alex Rivera reported being unable to access an internal server resource from the Windows 10 workstation.

The user could access external websites, but the internal Marketing network share was not initially accessible.

## Initial Symptoms

The first attempt to access the internal server using the server's fully qualified domain name returned:

> The network name cannot be found.

A subsequent `net view` attempt returned:

> System error 5 has occurred.
> Access is denied.

These results indicated that additional troubleshooting was required to determine whether the problem involved network connectivity, DNS resolution, or authentication.

## Troubleshooting Performed

### 1. Verified Server Connectivity

Tested direct IPv4 connectivity to the Windows Server:

```text
ping 192.168.56.106
```

The server responded successfully with **0% packet loss**, confirming that the workstation could reach the server over the network.

### 2. Verified DNS Resolution

Used `nslookup` to verify that the server's fully qualified domain name resolved:

```text
nslookup WIN-E1SKA42GQ7G.lab.local
```

The hostname resolved to the server's internal address:

```text
192.168.56.106
```

### 3. Reviewed Client Network Configuration

Used:

```text
ipconfig /all
```

The Windows 10 workstation was configured with:

* IPv4 Address: `192.168.56.110`
* Subnet Mask: `255.255.255.0`
* Default Gateway: `192.168.56.100`
* DNS Server: `192.168.56.106`

The configuration confirmed that the workstation was connected to the internal network and using the Windows Server as its DNS server.

### 4. Tested Authentication and Share Access

The workstation was using a local Windows account, so the domain credentials were explicitly provided when connecting to the server share:

```text
net use \\192.168.56.106\Marketing /user:LAB\arivera
```

The connection completed successfully.

### 5. Verified Successful Access

After authentication, the Marketing share was accessible through File Explorer.

The share contained:

* `Alex_Rivera_Access_Test.txt`
* `Ticket2_Access_Test.txt`

This confirmed successful access to the internal server resource.

## Finding

The workstation had network connectivity to the server and could successfully resolve the server's hostname through DNS.

The initial access failure was related to the user's authentication/session context rather than a complete network outage.

The workstation was logged into a **local Windows account** rather than the `LAB` domain account. Providing the appropriate domain credentials allowed the workstation to establish the connection to the Marketing share.

## Resolution

* Verified IPv4 connectivity to the Windows Server.
* Verified DNS resolution for the internal server.
* Reviewed the Windows workstation's network configuration.
* Authenticated to the server using the `LAB\arivera` domain account.
* Successfully connected to the Marketing network share.
* Verified that files were accessible from the share.

## Escalation

If the issue had continued after verifying connectivity, DNS, and authentication, the ticket would be escalated to the **Network/Windows Infrastructure team** to investigate server availability, DNS configuration, SMB connectivity, domain authentication, or access-control policies.

## Evidence

### Evidence #1 — Server IP Connectivity

<img width="3024" height="2970" alt="image" src="https://github.com/user-attachments/assets/2a81fb8b-84c5-4f55-a01c-cccea397955c" />


### Evidence #2 — DNS Resolution

<img width="3024" height="3168" alt="image" src="https://github.com/user-attachments/assets/81df52e6-4db1-4820-9233-0815fc0c82f5" />


### Evidence #3 — Client Network Configuration

<img width="3024" height="3092" alt="image" src="https://github.com/user-attachments/assets/e441dfb7-8a61-4639-9249-b89b706b0b42" />


### Evidence #4 — Successful Server Share Connection

<img width="3024" height="3198" alt="image" src="https://github.com/user-attachments/assets/e74b84be-ea6a-456f-9f44-fc45d0872565" />


### Evidence #5 — Successful Share Access

<img width="3024" height="3433" alt="image" src="https://github.com/user-attachments/assets/2ee7907f-37bb-4438-a092-1af8f4a58232" />


## Skills Demonstrated

`Windows Troubleshooting` `DNS` `TCP/IP` `IPv4` `Active Directory` `Domain Authentication` `SMB/UNC` `Network Shares` `ipconfig` `ping` `nslookup` `net use` `File Explorer` `Troubleshooting` `Escalation`

