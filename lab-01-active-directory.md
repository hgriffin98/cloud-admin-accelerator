# Lab 1: Active Directory Domain Services & Group Policy

**Video Walkthrough:** [[Paste your Loom link here]](https://www.loom.com/share/46027283112a4b6daf93f424bad8bf11)

## Objective
Deploy a Windows Server virtual machine in Microsoft Azure, promote it to an Active Directory Domain Controller, and enforce a Group Policy restriction on a specific Organizational Unit.

## Environment
* **Cloud Provider:** Microsoft Azure
* **Server Name:** `DC-01` (Windows Server)
* **Domain Name:** `corp.local`

## Steps Completed
1. Provisioned `DC-01` in Azure and connected via Remote Desktop (Windows App).
2. Installed the **Active Directory Domain Services (AD DS)** and **DNS** roles via Server Manager.
3. Promoted `DC-01` to a Domain Controller by creating a new forest (`corp.local`).
4. Opened **Active Directory Users and Computers (ADUC)** and created a new Organizational Unit (`IT-Staff`), a standard domain user (`harry`), and a security group (`Helpdesk-Team`).
5. Opened **Group Policy Management**, created a Group Policy Object (`Block-Control-Panel`), linked it to `IT-Staff`, and enabled **Prohibit access to Control Panel and PC settings**.

## Verification
* Confirmed **AD DS** and **DNS** status indicators turned green in Server Manager.
* Ran the **Group Policy Results Wizard** for `CORP\harry` on `DC-01` and verified `Block-Control-Panel` appeared under Applied GPOs.

## Troubleshooting Notes
* **Server Manager Red Indicators:** Confirmed red status on *Local Server* immediately after reboot was caused by delayed auto-start background services rather than an AD failure.
* **Azure Cost Management:** Stopped and deallocated `DC-01` in the Azure Portal immediately upon finishing the lab to preserve subscription credits.
