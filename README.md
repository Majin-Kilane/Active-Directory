## Active Directory Home Lab Project

## Overview
This project showcases my ability to design, implement, and manage a secure Active Directory (AD) environment. Using VirtualBox, Windows Server 2022, and Windows 10, I configured a simulated network to demonstrate essential IT administration tasks, including:

- Security-focused Group Policy Object (GPO) configurations.
- Active Directory structure with Organizational Units (OUs), users, and groups.
- Advanced security policies like account lockout, Kerberos, and password policies.
- Windows Server Update Services (WSUS) and DHCP management.
- Windows Defender Firewall management.
- Domain-joined client functionality.
_____________________________________________________________________________________

## Objectives
1. Build and secure an AD environment.
2. Implement advanced security policies (e.g., account lockout, Kerberos, password).
3. Create and manage a structured directory with OUs, users, and groups.
4. Configure WSUS and DHCP for network services.
5. Configure Windows Firewall settings via GPOs.
6. Test domain functionality and policy enforcement on a Windows 10 client.
_____________________________________________________________________________________

## Architecture Diagram
![Active Directory_Homelab](https://github.com/user-attachments/assets/79de1019-43d0-4b89-aa60-a871c38992cb)

The lab consists of:

- Router (192.168.1.1): Simulates internet access.
- Domain Controller (192.168.1.10): Hosts AD DS, DNS, WSUS, DHCP, and GPO configurations.
- Windows 10 Client (192.168.1.100): Domain-joined machine for testing policy application.
_____________________________________________________________________________________

## Lab Setup

### Tools Used
- Virtualization Platform: VirtualBox.
- Operating Systems:
   - Windows Server 2022 (Domain Controller).
   - Windows 10 (Client Machine).

## Key Configurations
1. ### Active Directory Setup:

   - Configured the domain controller with a static IP (192.168.1.10).
   - Installed Active Directory Domain Services (AD DS).
   - Created a domain yourdomain.local.
  
2. **Organizational Units (OUs), Users, and Groups**:
 - Designed a structured directory:
   - **OUs**: Created separate OUs for departments (e.g., IT, HR, and Sales).
   - **Users**: Added test users to each OU with specific roles.
   - **Groups**: Configured security groups (e.g., Administrators, Standard Users) for resource access control.

3. **Advanced Security Policies**:
 - **Account Lockout Policy**: Configured lockout thresholds and durations to protect against brute force attacks.
 - **Kerberos Policy**: Set ticket lifetimes and enforcement for secure authentication.
 - **Password Policy**: Enforced complexity requirements, expiration, and history settings for password security.

4. **Routing and Access Role**:
- Installed the Routing and Remote Access service (RRAS).
- Configured the router for VPN access and internal routing, ensuring connectivity between different network segments.

5. **DNS and Active Directory Integration**:
 - Configured DNS on the domain controller to support name resolution for domain-joined devices.
 - Integrated DNS with Active Directory to facilitate domain controller location and service resolution.

6. **Windows Server Update Services (WSUS)**:
 - Configured WSUS to manage Windows updates for all domain-joined devices.
 - Created GPOs to ensure automatic update installation on client machines.

7. **Dynamic Host Configuration Protocol (DHCP)**:
 - Set up DHCP on the domain controller for automatic IP address allocation.
 - Configured DHCP scopes and options to support network clients.

8. **Security Group Policy Objects (GPOs)**:
 - Configured additional GPOs for password requirements, account lockouts, and user restrictions.
 - Applied GPOs to OUs to enforce specific security policies based on department.

9. **Windows Defender Firewall Configuration**:
 - Created a GPO to manage firewall settings for all domain-joined devices.
 - Enabled inbound and outbound rules for specific services (e.g., ICMPv4 for troubleshooting).

10. **Auditing and Logging**:
 - Enabled auditing on critical domain controller events, including logon/logoff and object access.
 - Configured Windows Event Logging to capture and review security events for compliance and troubleshooting.

11. **Client Machine**:
 - Joined Windows 10 to the domain and tested the application of security and firewall policies.


## Key Features

- **Security Policies**:
   - Enforced password complexity, expiration, lockout settings, and Kerberos ticket management.
   - Configured account lockout to mitigate brute force attempts.
- **Routing and Access Configuration**:
   - Set up VPN and internal routing for remote access to the network.
- **DNS and Active Directory Integration**:
   - Ensured proper name resolution and service location for domain-joined machines.
- **WSUS Configuration**:
   - Managed Windows update deployment across domain clients to maintain security and compliance.
- **DHCP Management**:
   - Ensured IP address allocation to all domain-joined clients through a centralized DHCP server.
- **Firewall Management via GPOs**:
   - Enabled automatic startup for Windows Defender Firewall.
   - Applied inbound/outbound rules for enhanced security.
- **Auditing and Logging**:
   - Captured critical events through auditing, ensuring enhanced security monitoring.
     
_(Include screenshots of your GPO settings, OU structure, user/group configurations, DHCP/WSUS setups, and event logs here.)_


## Testing and Results

1. **Domain Functionality**:
   - Successfully joined the Windows 10 client to yourdomain.local.
   - Verified authentication using domain accounts.
2. **Policy Enforcement**:
   - Confirmed that security policies were applied to domain users (e.g., password changes required, account lockout after failed attempts).
   - Verified Kerberos ticket management and password complexity enforcement.
   - Tested automatic Windows updates via WSUS.
   - Verified DHCP functionality for IP address allocation to clients.
   - Verified firewall rules using test commands (e.g., ping for ICMP).
3. **Routing and Access**:
   - Verified VPN connectivity and internal routing using test devices.
4. **DNS Functionality**:
   - Ensured DNS resolved domain names for internal devices and services.
5. **Auditing and Logging**:
   - Verified the auditing configuration by reviewing event logs for critical activities (e.g., successful logons, object access).
6. **Organizational Management**:
   - Ensured users in specific OUs inherited the correct GPOs.
   - Tested group-based access to resources.
     
_(Add images of testing results, such as a successful gpresult /r output, event logs, VPN access logs, and DHCP lease information.)_


## Lessons Learned
- Improved understanding of Group Policy inheritance and troubleshooting conflicts.
- Gained experience with creating structured, scalable directory designs.
- Enhanced skills in configuring and managing Windows Defender Firewall through GPOs.
- Gained expertise in managing critical services like WSUS, DHCP, and Routing/Access.
- Learned the importance of auditing and logging for security and compliance.


## Conclusion
This project highlights my ability to build a secure and organized Active Directory environment, demonstrating skills in directory services, Group Policy management, network security, and server services like WSUS and DHCP. It reflects my readiness to manage enterprise-level IT systems and troubleshoot complex configurations.

