# INC-003 — Finance Printer Troubleshooting

**Category:** Hardware / Printing
**Priority:** P2 — High
**User:** Finance Department
**Environment:** Windows 10 Pro

## Issue

The Finance Department reported that the **Finance Printer** was not successfully completing print jobs.

The printer appeared to be installed on the workstation, but print jobs were not producing a physical output.

## Troubleshooting

* Verified that the Finance Printer was installed successfully.
* Checked the print queue for pending documents.
* Verified the printer status.
* Ran the Windows printer troubleshooter.
* Verified that the **Print Spooler** service was running.
* Reviewed the configured printer port.
* Verified the printer driver configuration.
* Sent test print jobs to the printer.
* Reviewed the device status and printer configuration.

## Finding

The printer was configured using a **Local Port named `FinancePrinter`** with the **Generic / Text Only** driver.

Windows successfully accepted the printer configuration and could send print jobs to the queue. However, there was no actual physical or network printer endpoint behind the configured Local Port to receive and produce the print job.

The Windows printer troubleshooter also could not identify a specific problem.

## Resolution

The workstation-side printer configuration was verified, but the lab environment did not contain an actual printer endpoint for the Local Port.

The issue would therefore require validation of the printer's physical or network configuration in a production environment.

The following items should be verified before closing the ticket:

* Printer power and physical connectivity
* Printer IP address or hostname
* TCP/IP port configuration
* Print server configuration
* Correct manufacturer printer driver
* Network connectivity to the printer

## Escalation

If this occurred in a production environment, the ticket would be escalated to **Printer/Network Support** to verify the physical printer, network connectivity, TCP/IP configuration, print server settings, and manufacturer driver.

## Evidence

### Evidence #1 — Printer Successfully Added

<img width="3024" height="2877" alt="image" src="https://github.com/user-attachments/assets/43dbcaed-83aa-4b43-8393-162825959b3b" />


### Evidence #2 — Print Queue

<img width="3024" height="2961" alt="image" src="https://github.com/user-attachments/assets/dd6fd522-a681-4dd6-bd45-34f6b2527c98" />


### Evidence #3 — Printer Status and Troubleshooter

<img width="3024" height="2912" alt="image" src="https://github.com/user-attachments/assets/20bddf83-9f5a-4de4-8f66-3786004c745a" />


### Evidence #4 — Print Spooler Running

<img width="3024" height="3166" alt="image" src="https://github.com/user-attachments/assets/bf08b6dd-b238-4842-ab3a-6dc8da01394c" />


### Evidence #5 — FinancePrinter Local Port

<img width="3024" height="3051" alt="image" src="https://github.com/user-attachments/assets/9bdf7ef5-11ca-4123-a024-74d69a9f2d53" />


### Evidence #6 — Generic Text Only Driver

<img width="3024" height="3163" alt="image" src="https://github.com/user-attachments/assets/b403927a-d591-4e5b-bb87-47dcdba97ead" />


## Skills Demonstrated

`Windows Troubleshooting` `Printer Troubleshooting` `Print Spooler` `Windows Services` `Device Management` `Printer Ports` `Printer Drivers` `Troubleshooting` `Escalation`

