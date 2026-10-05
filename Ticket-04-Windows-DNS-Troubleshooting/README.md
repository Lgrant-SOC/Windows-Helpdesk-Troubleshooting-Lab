# Ticket 04: Windows DNS Troubleshooting & Network Configuration

## Overview

Simulated a Help Desk ticket involving a Windows workstation that had Internet connectivity but was unable to resolve websites by hostname. Used a structured troubleshooting process to identify the DNS problem, test known-good DNS servers, correct the DNS configuration, and verify the fix.

## Lab Environment

* **Client:** Windows Workstation
* **Virtualization:** VirtualBox
* **Host-only IP:** `192.168.56.110`
* **NAT IP:** `10.0.2.15`
* **Default Gateway:** `10.0.2.2`
* **DNS Servers Tested:** Google Public DNS `8.8.8.8` and Cloudflare `1.1.1.1`

## Help Desk Troubleshooting

### 1. Verify Network Connectivity

Started by testing the default gateway to confirm the workstation had local network connectivity.

The gateway responded successfully with **0% packet loss**.

The workstation was then tested against Google's public IP address, `8.8.8.8`, to verify Internet connectivity.

The test was successful, confirming that Internet connectivity was available.

![Gateway and Internet Connectivity](IMG_DNS_CONNECTIVITY.jpeg)

### 2. Review Network Configuration

Used `ipconfig` to review the workstation's network adapters, IP addresses, and default gateway.

The workstation had separate Host-only and NAT network connections:

* Host-only: `192.168.56.110`
* NAT: `10.0.2.15`
* Default Gateway: `10.0.2.2`

![Network Configuration](IMG_DNS_IPCONFIG.jpeg)

### 3. Test DNS Resolution

Tested hostname resolution with:

```text
nslookup google.com
```

The request timed out while using `192.168.56.106` as the DNS server.

This showed that the workstation had network connectivity, but normal DNS resolution was failing.

![DNS Resolution Failure](IMG_DNS_FAILURE.jpeg)

### 4. Test a Known-Good DNS Server

Queried Google Public DNS directly:

```text
nslookup google.com 8.8.8.8
```

The query successfully returned Google's addresses.

This confirmed that external DNS resolution was working and helped isolate the problem to the workstation's DNS configuration.

![Known-Good DNS Test](IMG_DNS_SUCCESS.jpeg)

### 5. Correct the DNS Configuration

Tested another known-good DNS server and then configured the workstation to use Google Public DNS:

```text
netsh interface ipv4 set dns name="Ethernet" static 8.8.8.8
```

The goal was to correct the DNS configuration without changing the workstation's IP addressing or network connectivity.

![DNS Configuration Change](IMG_DNS_CONFIGURATION.jpeg)

### 6. Verify the Resolution

After correcting the DNS configuration, hostname resolution was successfully verified using:

```text
nslookup google.com 8.8.8.8
```

The workstation successfully resolved `google.com` through Google Public DNS.

The same successful DNS-resolution evidence is used here because it demonstrates the working DNS configuration after the change.

![Successful DNS Resolution](IMG_DNS_SUCCESS.jpeg)

### Final Connectivity Verification

Finally, tested the hostname directly:

```text
ping google.com
```

The hostname resolved successfully to `142.251.16.102`.

The test returned:

* **Packets Sent:** 3
* **Packets Received:** 3
* **Packet Loss:** 0%
* **Average:** 42 ms

![Final Connectivity Verification](IMG_DNS_FINAL_PING.jpeg)

## Troubleshooting Outcome

The issue was isolated to DNS resolution rather than general network connectivity. After correcting the DNS configuration, hostname resolution was restored and verified using `nslookup` and `ping`.

## Help Desk Skills Demonstrated

* DNS troubleshooting
* Windows network configuration
* `ipconfig` and `nslookup`
* Network connectivity testing with `ping`
* Identifying DNS resolution failures
* Testing known-good DNS servers
* Correcting DNS configuration
* Structured troubleshooting and verification
* Documenting technical troubleshooting steps
