## Lab Infrastructure Overview

![Active Directory drawio (4)](https://github.com/user-attachments/assets/a84c2fe8-dcda-413e-a8ab-5cfa97fa7ed3)

*Figure 1: Active Directory Lab Infrastructure Diagram*


# Active-Directory

## Objective
To design, implement, and manage a secure and scalable Active Directory infrastructure that centralizes user authentication, resource management, and security controls, ensuring efficient access control, organizational hierarchy, and policy enforcement within a corporate network environment.

## Skills Learned

- Understanding how to install and configure a Domain Controller, which is central to AD functionality.
- Experience in setting up and managing domains, trees, and forests to support organizational structure.
- Advanced skills in creating, deleting, and managing user accounts, both individually and in bulk.
- Expertise in configuring Group Policy Objects (GPOs) to enforce security settings and manage user environments.
- Organizing users, groups, and computers into OUs for better administrative control and policy application.
- ---------- Configuring security groups and assigning permissions based on roles.
- Configuring security policies that enforce password requirements and account lockoput policies.
- Skills in configuring DNS, which is closely tied to AD, to resolve domains names and ensure properAD functionality.
- Configuring AD and dealing with IP ranges, DHCP, and subnetting.
- Understanding and managing permissions for files, folders, and other network resources.
- Configuring auditing policies to trackuser activities, login attempts, and changes in AD objects.
- Implementing security best practices such as least privilege, user account control, and securing AD.

## Tools Used

- Oracle VirtualBox
- Windows Server 2022 ISO
- Windows 10 ISO

 ## Steps

# Setting Up VirtualBox, Windows Server 2022, and Windows 10

## Table of Contents
1. [Installing VirtualBox](#installing-virtualbox)
2. [Installing and Configuring Windows Server 2022](#installing-and-configuring-windows-server-2022)
3. [Installing Windows 10 on VirtualBox](#installing-windows-10-on-virtualbox)

---

## Installing VirtualBox

### Step 1: Download VirtualBox
- Go to the official [VirtualBox website](https://www.virtualbox.org/).
- Download the installer for your operating system (Windows, macOS, or Linux).

### Step 2: Install VirtualBox
1. Run the downloaded installer.
2. In the setup wizard:
   - Click **Next** on the welcome screen.
   - Choose installation location or leave it as default, and click **Next**.
   - Leave default settings for features and click **Next**.
   - Click **Yes** on the network warning if it appears.
   - Click **Install** to complete the installation.
3. After installation, click **Finish** to launch VirtualBox.

---

## Installing and Configuring Windows Server 2022
### Step 1: Download Windows Server 2022 ISO
- Visit the [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022) and download the Windows Server 2022 ISO.

### Step 2: Create a New Virtual Machine for Windows Server
1. Open **VirtualBox** and click **New**.

![0New](https://github.com/user-attachments/assets/ce5839d8-8203-434d-8e76-1fcf4d850e93)

*Ref 3: Creating New Windows Server VM*
  
2. Name the VM (e.g., **Windows Server 2022**).
3. Set **Type** to **Microsoft Windows** and **Version** to **Windows 2022 (64-bit)**.
   
![1  Creating a New VM for Windows Server](https://github.com/user-attachments/assets/e0085cce-cee4-4648-8bf0-4f125c41408c)

*Ref 3: Naming Windows Server VM*

4. Allocate at least **4096 MB** of RAM.

![2  Allocate at least 4096 MB](https://github.com/user-attachments/assets/ba296dde-891c-4e3e-84bb-b42f325d0141)

*Ref 3: Allocating RAM*
   
6. Create a **Virtual Hard Disk** (dynamically allocated) with at least **50 GB** of storage.

![3  50 GB of storage](https://github.com/user-attachments/assets/ddcf44ca-7562-42e3-b326-8d35d4cecfcd)

*Ref 3: Allocating Storage*

7. Click **Create** to finish VM creation.

### Step 3: Mount Windows Server 2022 ISO
1. Select the **Windows Server 2022 VM** in VirtualBox and click **Settings**.

![1  Mount Server VM](https://github.com/user-attachments/assets/cbfc1387-752f-4f2e-9062-7127e36a7e6b)

*Ref 3: Mounting Windows Server 2022*

2. Go to **Storage**, click the **Empty** disk under **Controller: IDE**, and select **Choose a disk file**.

![2  Select Storage](https://github.com/user-attachments/assets/0070bb60-58d6-48ba-ac9c-545704338beb)

*Ref 3: Select Storage*

3. Browse for the **Windows Server 2022 ISO** you downloaded.

![4  Select Server ISO](https://github.com/user-attachments/assets/50e5c340-b1ad-4df5-b39e-5a0f3cada12d)

*Ref 3: Select Server ISO*
   
4. Click **OK**.

### Step 4: Configure NAT Network for Internet Access
By default, VirtualBox uses NAT for internet access. This allows the DC to access the internet.

1. Select the Windows Server 2022 VM to configure NAT and click Settings.
2. In the Settings **window**, go to the **Network** tab.

![2Config NAT and Int](https://github.com/user-attachments/assets/6c910b45-af98-425c-8c87-9f9b6ee64bc1)
  
4. Under **Adapter 1** (or any available adapter):
   - Ensure **Enable Network Adapter** is checked.
   - In the **Attached to** dropdown, select **NAT**.

![3EnsureNetwork_Adapter](https://github.com/user-attachments/assets/8a60bcf8-2ab9-426a-b93f-672ae88173c5)

5. Click **OK** to apply the changes.
The VM is now configured to access the internet via NAT. The host machine will handle all the routing.


### Step 5: Configure an Internal Network for VM Communication
An **Internal Network** allows multiple virtual machines to communicate with each other on a private network and access the internet using the DC as the gateway.

1. Under **Adapter 2** (or another available adapter):
   - Check **Enable Network Adapter**.
     
![4EnableAdapter2](https://github.com/user-attachments/assets/1306351f-c34d-477c-b015-7a174413f98e)


   - In the **Attached** to dropdown, select **Internal Network**.

![5SelectIntNet](https://github.com/user-attachments/assets/8614b408-5270-4510-a8a6-155fd8a46a60)

   - In the **Name** field, provide a name for your internal network (e.g., InternalNet).

![6NameIntNet](https://github.com/user-attachments/assets/27da9eca-6f57-45d0-ba6d-046e6e4110a1)
    
2. Click **OK** to apply the changes.

### Step 6: Start the VM and Install Windows Server 2022
1. Click **Start** to boot the VM and begin installation.

![1Click Start](https://github.com/user-attachments/assets/4e454546-308c-4bb7-ade5-398e7e205bce)
   
2. In the Windows Setup screen, choose your **language**, **time**, and **keyboard layout**.

![1SelectLanguage](https://github.com/user-attachments/assets/ae12da39-ff14-4595-9852-d1c4d995c139)

3. Click **Next** then **Install Now**.

![2Install](https://github.com/user-attachments/assets/52c54cc2-b466-4fc4-8692-fbc35c139e03)
   
4. Select the version of **Windows Server 2022** you want (choose **Desktop Experience** for GUI) and click **Next**.

![3SelectVersion](https://github.com/user-attachments/assets/3aa2afd7-9ff6-4bf0-af51-b9087ebd3559)

5. Accept the license agreement and click **Next**.

![4ClickIAccept](https://github.com/user-attachments/assets/2ffcf842-dff5-44bc-99f9-5920a581fd09)

6. Choose **Custom: Install Windows only**.

![5ChooseCustom](https://github.com/user-attachments/assets/8807683f-ff25-4fa1-a54d-69944a748c66)

7. Select the virtual hard drive, click **Next**, and the installation will begin.

![6SelectVHD](https://github.com/user-attachments/assets/767a4fe7-6a14-4d2f-87fb-a7af4c2874f5)

8. Wait for Installation to Complete.
   - Windows Server will begin copying files and installing features.
   - This process may take several minutes and will automatically restart the server when finished.

![7WaitForInstallation](https://github.com/user-attachments/assets/7fbb034a-38e3-4268-b4b1-70f3c157eebb)

9. After the installation completes, set a **strong password** for the Administrator account and click **Finish**.

![8CreatePW](https://github.com/user-attachments/assets/421ddd24-bff4-4f9b-a388-540c55b687d0)

### Step 7: Configure Windows Server 2022
1. Press **Ctrl+Delete** on the login screen.
   - Enter the **Administrator password** you set up in the previous step.
   - Click **Enter** to log in.
2. Once the VM is running, go to the **VirtualBox menu** at the top of the VM window.
Select **Devices** > **Insert Guest Additions CD Image**.
   - This will insert the Guest Additions ISO file as a virtual CD drive in the VM.
   - This will provide a better experience, allow for resolution adjustments, and eliminate display lag.

![1InsertGuestAdds](https://github.com/user-attachments/assets/e297c429-282e-492e-a3b2-23c2870121ea)
     
3. Open **File Explorer**.

![2GoToExplorer](https://github.com/user-attachments/assets/7fa37eba-02b9-4591-a52c-dce0ffcd384b)

4. Run the Guest Additions Installer (Windows VM)
Open File Explorer in the VM.
Go to **CD Drive (D:)** and double-click on **VBoxWindowsAdditions-amd64.exe** to start the installer.

![3RunVBGA](https://github.com/user-attachments/assets/1a450cd9-e15f-4793-b093-4153c0f81b7d)

Follow the installation prompts:
   - Click **Next** in the installation wizard.
   - Accept the license agreement.
   - When prompted, click Install to begin the installation. Allow any security prompts to install VirtualBox drivers.  

5. Restart the VM
   - After installation, reboot the VM to activate the Guest Additions features.
   - Click **Reboot Now** and **Finish**.

![4Reboot](https://github.com/user-attachments/assets/43acc9f1-cb98-4ae1-bb6c-80be5ec22973)
   
### Step 8: Set a Static IP Address on Windows Server 2022
1. Once logged in, open **Server Manager** and go to Local Server.
2. In the **Properties** section, click on **Ethernet** (or your network adapter name).
   
![1SetNetAdaptor](https://github.com/user-attachments/assets/7913b9f6-f262-4b85-81a1-63cb010ee5e7)
  
3. In the **Network Connections** window, right-click on your network adapter and select **Properties**.

![3OpenProperties](https://github.com/user-attachments/assets/1918b3f1-3606-4b41-b0cd-1759ee2eafab)

4. Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.

![4SelectIPv4](https://github.com/user-attachments/assets/1afc160d-c7fc-411b-b4e0-55c121cfc8f8)

5. Choose **Use the following IP address** and enter the following details:
   - **IP address**: Choose an IP, e.g., 192.168.1.10.
   - **Subnet mask**: Use 255.255.255.0.
   - Leave **Default gateway** and **DNS server** fields blank (for isolated networks).
   - Set the loopback IP 127.0.0.1 to use this server as the DNS server.

![5ChooseIP](https://github.com/user-attachments/assets/4e26ab15-2523-402b-b5ef-89a4ca4ebf58)

6. Click **OK** to save settings.

   - **Change the computer name** (optional).
   - **Enable Remote Desktop** (optional).
7. Reboot if necessary.
--------------------

## Configuring Security in Windows Server 2022


### Step 9: Update the Server
1. Login  Open **Server Manager**.
2. Go to **Local Server** and click on **Windows Update**.

![1ServerManager](https://github.com/user-attachments/assets/e3bc635c-9a50-4866-82d9-bf0bf72d38e5)

3. Check for updates, download, and install any critical and security updates to ensure the server is protected against known vulnerabilities.

![2InstallUpdates](https://github.com/user-attachments/assets/ad80c583-e8b8-4eab-bb3e-46be8d77215c)

4. Restart.


### Step 10: Configure Windows Firewall
1. Open **Server Manager** and select **Tools** > **Windows Defender Firewall with Advanced Security**.
2. Configure **Inbound** and **Outbound** rules to allow only necessary traffic.
3. Enable **logging** in the firewall settings to monitor suspicious connections.


### Step 11: Enable Windows Defender Antivirus
1. Go to **Start** > **Settings** > **Privacy & Security** > **Windows Security** > **Virus & Threat Protection**.

![WinSecurity](https://github.com/user-attachments/assets/123704a3-f991-4dd6-9332-29783170a676)

2. Ensure **Real-Time Protection** and **App & browser control** are enabled.

![VirusThreat](https://github.com/user-attachments/assets/2031034e-73e1-4492-b38a-b1aa849f56a8)

3. Turn on **Reputation-based protection**.

![EnableAppBrowserControl](https://github.com/user-attachments/assets/bf7fdeec-87c0-4458-a4f2-1c3d4561e2ec)
 
4. Schedule regular scans to detect and prevent malware.

![Enabled](https://github.com/user-attachments/assets/3c1f9d64-d2cc-4e66-8dd8-99bc79e4e62c)


### Step 12: Disable Unnecessary Services
1. Open **Server Manager** and go to **Tools** > **Services**.
2. Identify services that are not essential for your server’s purpose and set them to **Manual** or **Disabled**.

![services](https://github.com/user-attachments/assets/a0dc3538-4285-4230-97f6-eb5c111f4f38)

3. Examples of services to review: **Remote Registry**, **Print Spooler** (if not needed), and **Windows Remote Management** (if not required).


### Step 13: Configure Default Domain Policy
1. Go to **Tools** > **Group Policy Management**.
2. In **Group Policy Management**, expand **Forest** > Domains and select your domain (e.g., mydomain.com).
Right-click on Default Domain Policy and choose Edit.
   - Note: Since this policy is domain-wide, changes here will apply to all users and computers in the domain.

![EditGPO](https://github.com/user-attachments/assets/373bfdff-288b-477e-a488-1b6788549d25)


### Step 14: Configure Password Policies
1. In the **Default Domain Policy**, go to **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Account Policies** > **Password Policy**.
2. Define password policies, such as:
   - **Enforce Password History** (e.g., 24 passwords).
   - **Maximum Password Age** (e.g., 60 days).
   - **Minimum Password Length** (e.g., 12-16 characters).
   - **Password Complexity Requirements** (ensure it includes uppercase, lowercase, numbers, and symbols).
  
![2PWPol](https://github.com/user-attachments/assets/dbefe350-3340-4679-b917-9ea7ae0a69ce)


### Step 15: Configure Account Lockout Policy
1. Open **Server Manager**.
2. Go to **Tools** and select **Group Policy Management**.
3. In the **Group Policy Managemen**t window, expand **Forest** > **Domains**.
4. Select your domain name (e.g., mydomain.local).
5. Right-click on the **Default Domain Policy** and choose **Edit**.
   -Note: It’s best to apply this policy at the domain level to ensure it affects all users across the domain.

![1EditGPO](https://github.com/user-attachments/assets/abfa5cd9-993a-4e8d-869d-ffe9d91df8ae)
   
6. In the Group Policy Management Editor window, go to:
   - **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Account Policies** > **Account Lockout Policy**. 
7.Double-click **Account lockout threshold**.
8. Set the number of failed logon attempts allowed before the account is locked out (e.g., 5).

![AccLOThreshold](https://github.com/user-attachments/assets/bbb2f474-5b4b-40bd-ac8e-55871100466e)

9. Click **OK**.
10. Double-click **Account lockout duration**.
11. Set the amount of time (in minutes) the account remains locked before it automatically unlocks. (15 minutes preferred).
   - Note: If you want an administrator to unlock the account manually, set this to 0.

![AccLDuration](https://github.com/user-attachments/assets/126918fe-cab2-4c04-a287-3f3c71a775a7)

12. Click **OK**.
13. After configuring the settings, close the **Group Policy Management Editor**.
    - Group Policy changes will apply automatically.

![lockoutpol](https://github.com/user-attachments/assets/03c97837-752a-4140-86d2-880ebc9156e2)


### Step 16: Configure Kerberos Policies
1. In the **Group Policy Management Editor**, navigate to:
   - **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Account Policies** > **Kerberos Policy**.
2. Configure the following Kerberos settings:
   - **Enforce user logon restrictions**: Set to Enabled to enforce Kerberos logon restrictions, which adds an extra layer of security by checking each user’s rights before logging on.
   - **Maximum lifetime for service ticket**: Define how long service tickets are valid (e.g., 600 minutes).
   - **Maximum lifetime for user ticket**: Set a time limit for user tickets, typically 10 hours (600 minutes).
   - **Maximum lifetime for user ticket renewal**: Specify how long a ticket can be renewed (e.g., 7 days).
   - **Maximum tolerance for computer clock synchronization**: Set to 5 minutes to prevent issues with Kerberos authentication due to time differences.

![Kerberos](https://github.com/user-attachments/assets/34cdbed4-7d7b-4228-86c7-8427bbfb8714)

### Step 17: Install Active Directory Domain Services (AD DS)
1. In **Server Manager**, click **Add Roles and Features**.

![1AddRoles](https://github.com/user-attachments/assets/c245ca51-424a-4032-9e1c-17e6a3e3ced3)
 
2. Click **Next**.

![2Next](https://github.com/user-attachments/assets/7ca87ca2-20d9-4ccb-b27b-c81650409f22)

3. Select **Role-based or feature-based installation**, click **Next**.

![2SelectRoleBased](https://github.com/user-attachments/assets/c8f67bc2-6428-4067-a858-b7afc554c3c6)

4. Select the server and click **Next**.

![3SelectServer](https://github.com/user-attachments/assets/f33c1889-faa4-447a-b94e-cb8331a79fec)

5. In the **Server Roles** section, select **Active Directory Domain Services** and click **Next**.

![5SelectADDS](https://github.com/user-attachments/assets/dd14748c-e497-4446-9a5e-23277d584e83)

6. Click **Next**.
 
![6Next](https://github.com/user-attachments/assets/a763de86-767f-4eb1-a303-578c75ff611c)

7. Click **Next**.

![7Next](https://github.com/user-attachments/assets/359c8998-f73d-4059-b251-afe1114a6800)
 
8. Click **Install** to install the AD DS role.

![8Install](https://github.com/user-attachments/assets/cea0f971-d581-4248-9cb8-1765e3c35802)

9. After installation, click **Promote this server to a domain controller**.

![10SelectPromoThisServer](https://github.com/user-attachments/assets/d7afc632-5e5a-40bd-98a1-38bfbe9f3e37)

10. Click **Notification** icon.

![9ClickNotificationsIcon](https://github.com/user-attachments/assets/f5f5d01c-ffb7-4f2b-aeab-555c97074a16)
  
11. In the AD DS configuration wizard, choose **Add a new forest** and enter a **domain name** (e.g., `mydomain.com`) and click **Next**.
   - Note: Using |.com| allows integration with email, VPNs, and remote access, as it can be routed    
     through public DNS servers.
   - It’s generally recommended to use a subdomain of a registered .com domain (e.g., ad.yourdomain.com) for Active Directory to avoid conflicts and enable more flexible access. This configuration can simplify DNS management, integrate smoothly with external services, and align with internet standards.

![11AddNewForest DomainName](https://github.com/user-attachments/assets/beaf343c-c532-4039-9963-a5285e7336d7)

12. Create a password.

![12CreatePW](https://github.com/user-attachments/assets/88ebdf9e-8246-4f3c-8000-a1ad72a56e30)

13. Uncheck **Create DNS delegation** and press **Next**.

![12UncheckCreateDNSDel](https://github.com/user-attachments/assets/9b1a2d6d-34cb-44b4-9071-2e543d242456)
   
14. Follow the prompts to complete the domain controller configuration and restart the server.
 
![18DomainAdminLogin_Copy](https://github.com/user-attachments/assets/9db58aba-59c7-4d2f-bb85-c61e4c3560ab)

### Step 18: Install the Routing and Remote Access Role
1. Open **Server Manager**.
2. Click **Manage** > **Add Roles and Features**.

![1OpenServerMan](https://github.com/user-attachments/assets/6cf61bd4-2934-49c8-acbd-cc6625ce74c1)

3. In the **Add Roles and Features Wizard**, click **Next** until you reach **Select Server Roles**.
4. Check **Remote Access** and click **Next**.

![3SelectRemoteAccess](https://github.com/user-attachments/assets/07821ecb-f140-455a-b308-269c873bda86)

5. On the **Features** page, click **Next**.

![2AddRolesFeature](https://github.com/user-attachments/assets/95c6e85a-aeed-48c0-9dc7-cb6f3b02f150)
 
6. On the **Role Services** page, check **Routing**, then click **Next**.

![4SelectRouting](https://github.com/user-attachments/assets/2ef59bd1-4153-444d-a655-0d582078c13b)  

7. Click **Install** and wait for the installation to complete.

![5Install](https://github.com/user-attachments/assets/4b16694e-ed1b-4864-89c0-ec0e07760174)

8. Once installed, go to **Tools** in Server Manager, then select **Routing and Remote Access**.

![1Routing RA](https://github.com/user-attachments/assets/0b01140c-039b-4ee3-9e54-6f1ef623fa8e)

9. In the **Routing and Remote Access** window, right-click on your server name and select **Configure and Enable Routing and Remote Access**.

![2Configure](https://github.com/user-attachments/assets/751bcdfd-9234-49f8-bb0f-9be41fe0c496)

10. In the **Routing and Remote Access Server Setup Wizard**, click **Next**.

![3Next](https://github.com/user-attachments/assets/3a5f82da-3ec3-4411-8339-3536fbc21693)

11. Choose **Network Address Translation (NAT)** and click **Next**.

![4ChooseNAT](https://github.com/user-attachments/assets/7001b880-fc62-4d34-b99a-b42d91877dc4)

12. Select the network adapter connected to the external network (public/internet) and click **Next**.
   - This interface is typically the one with internet access.

![5ChooseInterface](https://github.com/user-attachments/assets/21bd46f2-5ae3-45ea-9cfc-d579ce51339a)

13. Select **Finish** to complete the configuration.

![6finish](https://github.com/user-attachments/assets/8e77b88b-1881-4ba0-9f76-1bbb5c84fcea)

14. In the **Routing and Remote Access** window, expand your server node, then expand **IPv4**.

![2ExpandIPv4](https://github.com/user-attachments/assets/70c9170d-f928-4b08-90a0-ccde1fe99db3)
   
15. Right-click **NAT**.
16. Choose the network adapter connected to the internal network (private network) and click **OK**.

![3SelectInNet](https://github.com/user-attachments/assets/e5e23a14-781f-4a00-8bdf-f7ea00c6b2ae)

17. In the **NAT Interface Properties** window, select **Private interface connected to private network** and check **Enable NAT on this interface** if it is not already selected.

![4EnableNAT](https://github.com/user-attachments/assets/ec22eb52-bb5b-401e-a656-521752f09dfd)

18. Click **Apply**, then **OK** to save the settings.

### Step 19: Setting Up a DHCP Server
1. Log in to **Windows Server 2022** with an account that has administrative privileges.
2. Open **Server Manager**.
3. Click **Add Roles and Features**.
4. In the **Add Roles and Features Wizard**, click **Next** through the introductory screens until you reach the **Server Roles** section.

![1Add](https://github.com/user-attachments/assets/a30e6115-a67a-421d-a61f-ff2ecd715bbd)

5. In **Server Roles**, check **DHCP Server** and click **Next**.

![2DHCP](https://github.com/user-attachments/assets/1f58a41f-b46e-47c3-821b-6d2ff8d8dae1)

6. Continue through the wizard, leaving the default settings, and click **Install** on the confirmation screen.

![3Install](https://github.com/user-attachments/assets/990f1658-032e-4bb6-8f4e-8af179b7808d)

7. Wait for the installation to complete, then click **Close**.
8. After installation, go back to **Server Manager**.
9. At the top, you should see a notification flag; click it and select **Complete DHCP Configuration**.

![4YellowFlag](https://github.com/user-attachments/assets/129fcf8b-06a3-4999-88dd-399fbc6b43d0)

10. In the **DHCP Post-Install Configuration Wizard**, click **Next**.
11. Choose to **Use the following user account** (usually the default network service account) and click **Next**.
12. Click **Commit** to apply the configuration.

![5Commit](https://github.com/user-attachments/assets/82c826d8-943b-4809-aadf-56f190491341)

13. Click **Close**.

![6Close](https://github.com/user-attachments/assets/c80c2b7a-57c4-48ce-b4c7-d7546cd5cd86)
   
14. In **Server Manager**, go to **Tools** and select **DHCP** to open the DHCP management console.

![7Tools](https://github.com/user-attachments/assets/4a1a257f-9825-4f8b-bb51-ebcc96c07fd0)

15. In the DHCP console, expand your **Server Name** and right-click on **IPv4**.
16. Select **New Scope** to launch the **New Scope Wizard**.

![8NewScope](https://github.com/user-attachments/assets/2362bd6b-0ed5-44ae-a552-277365454f41)

17. In the **New Scope Wizard**, click **Next**.
18. Enter a **Name** and optional **Description** for the scope (e.g., "Home Network").

![9AddName](https://github.com/user-attachments/assets/69e3d57c-93f7-4665-9076-965869c93164)

19. Specify the **IP Address Range**:
   - **Start IP Address**: The first IP in the range (e.g., 192.168.1.100).
   - **End IP Address**: The last IP in the range (e.g., 192.168.1.200).
   - **Subnet Mask**: Based on your network (e.g., 255.255.255.0).
  
![10SpecifyIP](https://github.com/user-attachments/assets/2dd61190-5032-4689-bae9-49353fc4139d)

20. Click **Next**.

21. Specify the **Lease Duration**, which is how long a device can keep an IP address before it’s reassigned (default is 8 days).

![11Lease](https://github.com/user-attachments/assets/e4d4cdaa-c4e6-48f4-bcf5-864e4b791dc3)

22. Click **Next**.

23. You can now configure **DHCP options** (gateway, DNS servers, etc.):
   - **Router (Default Gateway)**: Enter the IP address of your network's default gateway.
  
![12AddDefaultGateway](https://github.com/user-attachments/assets/c55ef7fa-909e-4130-b233-8076cfe6f742)

   - **DNS Servers**: Specify the IP address of DNS servers to use (e.g., your internal DNS server).

![13AddDNS](https://github.com/user-attachments/assets/321716af-7f17-4014-805e-b4cc2aaadf4e)

   - Click **Next** after each configuration option.

24. At the **Activate Scope** step, select **Yes, I want to activate this scope now** and click **Next**.

![14ActivateScope](https://github.com/user-attachments/assets/8f6a7255-85e0-4fe0-9cf7-09e8048fee0b)

25. Click **Finish** to complete the setup.
26. **Restart DHCP** services if necessary.
27. Connect a client device to the network and check if it’s receiving an IP address from the DHCP server by running ipconfig on the client.

### Step 20: Enable Auditing and Logging on Windows Server 2022
1. In the Group Policy Management Editor, go to:
**Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Advanced Audit Policy Configuration** > **Audit Policies**.

![1Auditpolicies](https://github.com/user-attachments/assets/59bb0a7b-a447-487f-abe1-1d9bba48204a)


2. Go to **Account Logon** and enable **Audit Credential Validation**.
   - This logs successful and failed login attempts.
  
![2EnableAccLO](https://github.com/user-attachments/assets/11d2f8f5-ba8c-45d1-a007-67cba1171f13)

3. In **Account Management**, enable **Audit User Account Management** and Audit **Security Group Management**.
   - These settings track changes to user accounts and security groups.
  
![EnUser Sec](https://github.com/user-attachments/assets/49f09b2e-776d-4229-bbd0-b5d777cf5a45)

4. In **Logon/Logoff**, enable **Audit Logon** and **Audit Logoff**.
   - This logs successful and failed logon attempts for tracking user access times.
  
![5EnLogonLogoff](https://github.com/user-attachments/assets/f7c76707-1410-4752-94c4-34c3fc2ced55)

5. Enable **Audit File System** and **Audit Registry** under Object Access.
   - This setting logs access to files and registry entries, helpful for tracking data access and modifications.
  
![ObjectAccess](https://github.com/user-attachments/assets/a83ecae1-0701-42fe-b735-4191641f7c1e)

6. **Enable Audit Audit Policy Change** and **Audit Authentication Policy Change**.
   - This logs any changes to audit policies and authentication settings.
  
![PolicyChange](https://github.com/user-attachments/assets/3c85bc48-af4e-46d5-8e49-56fc8d8c9f9d)

7. Enable **Audit Sensitive Privilege Use** to log events where high-level permissions are used (e.g., backup, restore).

![PrivilegeUse](https://github.com/user-attachments/assets/cc1951d5-69d4-4990-b7aa-955c04e9de16)
   
9. Go to **Security Settings** > **Local Policies** > **Audit Policy**.
   - Enable **Audit account logon events**, **Audit account management**, and **Audit policy change** for both **Success** and **Failure** to capture a comprehensive log.
  
![AuditCmplt](https://github.com/user-attachments/assets/91a75c72-6965-4134-8a31-9332c5190bfc)

10. Close the **Group Policy Management Editor**.
11. The policy will immediately.

11. Open **Event Viewer** to confirm that logs are being recorded.

![OpenEV](https://github.com/user-attachments/assets/a6073c59-4a6d-41d1-8b4b-50ab3ffb14cb)

12. Navigate to **Windows Logs** > **Security** to view audit logs.

![ViewLogs](https://github.com/user-attachments/assets/e7d4cfc3-5922-4bad-9e49-053296055e30)

13. Check the **Event IDs** to monitor specific events:
   - **4624**: Successful logon.
   - **4625**: Failed logon attempt.
   - **4720**: User account creation.
   - **4722**: User account enabled.
   - **4725**: User account disabled.


### Step 21: Configure WSUS on Windows Server
1. **Prepare Storage for WSUS (Optional but Recommended)**
   - **Partitioning**: Create a new partition or attach a separate drive for storing WSUS updates (e.g., D:\WSUS). This helps isolate the storage load from the system partition.
   - **Create a Folder**: On the new partition, create a dedicated folder for WSUS, such as D:\WSUS\Updates.
2. **Open Server Manager**: Select **Add roles and features**.

![AddRoles](https://github.com/user-attachments/assets/1ec1319d-e16b-407c-8d53-2cf0484a9903)

3. **Role-Based Installation**: Choose **Role-based or feature-based installation** and select the server where you want to install WSUS.
4. **Select WSUS**: In the roles list, select **Windows Server Update Services**, then click **Next**.

![1WSUS](https://github.com/user-attachments/assets/8d667161-bbb1-406c-ba8e-d560ac1169b2)

5. **Select Required Features**: Leave the default features selected, and click **Next**.
6. **Content Location**: You’ll be prompted to specify a **content location** for storing updates.
   -  Create New Folder and rename it (e.g., "WSUS_Update_Storage").
     
  ![CreateFolder](https://github.com/user-attachments/assets/55a70353-7cee-48c7-9673-cdd6192b7525)

   -  Copy Path.
     
![CopyPath](https://github.com/user-attachments/assets/98383dad-109b-4786-a6c5-b4a8751ddc66)

   -  Enter the path to your dedicated folder (e.g., D:\WSUS\Updates).

![PastePath](https://github.com/user-attachments/assets/84722d6d-21f8-4395-9590-90a9db3b94a2)

7. **SQL Server** (Optional): If you have an external SQL Server for the WSUS database, connect to it here. Otherwise, WSUS will use Windows Internal Database by default.
8. Click **Next** to install WSUS.
9. After the WSUS role is installed, click **Launch Post-Installation Tasks** to complete setup.

![LaunchPostInst](https://github.com/user-attachments/assets/e686ea7e-903e-46bc-b5e5-e801debf70ef)

10. Wait for the post-installation tasks to complete, which initializes the WSUS database.

![InstSucceedd](https://github.com/user-attachments/assets/ab5fe8af-504a-4169-89ed-14ca23440660)

11. **Open WSUS Console**: Go to **Tools** > **Windows Server Update Services** in Server Manager.

![OpenWSUS](https://github.com/user-attachments/assets/96fa1259-d9df-402e-b22c-6c5f2771c8b8)

12. **Specify Proxy Server** (if applicable).
13. **Synchronize with Microsoft Update**: In the **WSUS Console**, click **Options** > **WSUS Server Configuration Wizard** to set up synchronization with Microsoft’s update servers.

![WSUSSConfigWiz](https://github.com/user-attachments/assets/d72e3a48-4bc5-49b8-b3c0-275f0a08d11e)

14. Click **Next** until you reach the **Connect to Upstream Server** tab and click **Start Connecting**.
    - Wait for Synchronization to finish then click **Next**. 

![StartConn](https://github.com/user-attachments/assets/3f117ed7-030e-448f-953b-9fe60d26e9a8)

15. Click **Download updates only in these languages** then select **English**.

![SelctLang](https://github.com/user-attachments/assets/4560ac55-9e62-4a04-b342-78913f17a317)

16. Select any products you want to update, then click **Next**.

![ChooseProducts](https://github.com/user-attachments/assets/0c7e49c8-8e3d-49fe-ba4b-4faca619c0fc)
  
17. Select classification types, then click **Next**. 

![ChooseClassifx](https://github.com/user-attachments/assets/09942c02-9f13-4266-9ab6-a21ad5b7d055)

18. Select **Synchronize Manually** then click **Next**.
19. Select **Begin initial synchronization**, then click **Next**, and then **Finish**.

![SelectBeginIntSync](https://github.com/user-attachments/assets/6ea04362-2078-42a4-aeec-6e329b022e51)

20. **Approve Updates**: After synchronization, approve the updates you want to deploy to the networked clients.
21. **Configure Group Policy for Client Updates**
   - **Open Group Policy Management**: Go to **Group Policy Management** on your domain controller.
   - **Create or Edit a Group Policy**: Right-click your domain or specific OU and select **Create a GPO** (or edit an existing GPO).

![_GPO](https://github.com/user-attachments/assets/b1b0a230-af8b-4abc-aea5-79104d8e7411)
  
22. **Configure WSUS Settings**:
   - Right-click the newly created GPO and then click **Edit**.
   - Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Update**.
   - Set **Specify Intranet Microsoft Update Service Location** to the WSUS server URL (e.g., http://WIN-EUI59HSFCD4.mydomain.com:8530).

![_PasteClickApply](https://github.com/user-attachments/assets/cb738f26-def8-4309-b6c1-75e12185f7d0)
   
   - Enable **Configure Automatic Updates** and configure the update schedule.

![_EnableAutoUpdate](https://github.com/user-attachments/assets/0ce0fe2f-70af-48f3-982a-9b13f09a7589)

- Enable **Automatic Updates detection frequency**.  

![__EnableAutoDetecFreq](https://github.com/user-attachments/assets/d3354067-a134-4059-8621-e1aaaec06f57)

______________________________________________________________________________
## Installing Windows 10 on VirtualBox

### Step 1: Download Windows 10 ISO
- Visit the [Microsoft Windows 10 Download Page](https://www.microsoft.com/software-download/windows10) and download the ISO.

### Step 2: Create a New Virtual Machine for Windows 10
1. Open **VirtualBox** and click **New**.

![0New](https://github.com/user-attachments/assets/0de0b4d9-2a91-44fb-be14-b24e6e0c44bc)

2. Name the VM (e.g., **Windows 10**).
3. Set **Type** to **Microsoft Windows** and **Version** to **Windows 10 (64-bit)**.

![3Name](https://github.com/user-attachments/assets/8fc25266-d5b3-49c7-a052-997b7888a033)

5. Allocate at least **2048 MB** of RAM (preferably 4096 MB).

![4Mem](https://github.com/user-attachments/assets/4355785e-569d-469f-ae8e-12629c10df6d)

5. Create a **Virtual Hard Disk** with at least **50 GB** of storage.

![5VHD](https://github.com/user-attachments/assets/0d6d3faa-e2ee-42ca-99ee-7c6eccb18f0c)

6. Click **Finish**.

### Step 3: Mount Windows 10 ISO
1. Go to **Storage**, click the **Empty** disk under **Controller: IDE**, and select **Choose a disk file**.
2. Browse and select the **Windows 10 ISO** you downloaded.

![6ChooseDisk](https://github.com/user-attachments/assets/f4dc82cb-8d21-4cbd-a5c1-a24e31e4c901)

3. Click **OK**.

### Step 4: Configure Network for Internet Access
This allows the Windows 10 client to access the internet using the Domain Controller as the Gateway.

1. Select the Windows 10 VM to configure NAT and click Settings.
2. Under **Adapter 1** (or any available adapter):
   - Ensure **Enable Network Adapter** is checked.
   - In the **Attached to** dropdown, select **Internal Network**.

![SelectIntNetwork](https://github.com/user-attachments/assets/2f17f690-9d8a-4377-b96c-28a5747193bb)

### Step 5: Start the VM and Install Windows 10
1. Click **Start** to boot the VM from the ISO.

![1Start](https://github.com/user-attachments/assets/ac185362-a17a-445d-9ef2-e2dbf1b0be92)
   
2. In the **Windows Setup** screen, choose your **language**, **time**, and **keyboard layout**.

![2ChooseLang](https://github.com/user-attachments/assets/1742c03e-2b8f-4baa-b9c4-dfce6c36098f)

3. Click **Install Now**.

----Insert Image----

4. Enter a **product key** or select **I don’t have a product key** to skip.

![3Product](https://github.com/user-attachments/assets/ee22cfcf-a00d-47bb-829b-5dc54567e244)

5. Choose the Windows 10 Home to install and click **Next**.

![4windows10](https://github.com/user-attachments/assets/451126da-802d-4284-a3c4-e7516557141f)

6. Accept the license agreement.

![5Accept](https://github.com/user-attachments/assets/474d60e4-671a-443b-83b2-85559ddf5cdb)

7. Select **Custom: Install Windows only**.

![6Custom](https://github.com/user-attachments/assets/af1c1b76-48d3-4614-9e8f-b693f709da50)

8. Choose the virtual hard drive you created and click **Next** to begin the installation.

![7ChooseVHD](https://github.com/user-attachments/assets/dbec21c7-ffcf-4eb7-b274-fda257eb9b9a)

### Step 6: Configure Windows 10
1. Once the installation completes, set up your **user account**, **region**, and **network settings**.
2. Follow the prompts to complete the Windows 10 setup.

### Step 7: Verify that the Windows 10 client is domain-joined and has been allocated an IP address from the DHCP server
1. The **Windows 10 client** is joined to the domain. Note **mydomain.com** in the Network tab.
2. Press **Yes**.

![1DJGW](https://github.com/user-attachments/assets/3ee452ee-2356-47ad-b172-7ab9e4fc6ce8)

3. Go to the **Search bar** then type **Powershell** and click **Open**.

![RunPowershell](https://github.com/user-attachments/assets/da8a530a-8481-4795-b449-211419462123)

4. Type **ipconfig** to verify network settings.
5. The **Windows 10 client** has been allocated the IP address 192.168.1.100 and uses the Domain Controller as its default gateway, set to 192.168.1.10.
6. To check if the client can connect to the internet, type the **ping** command followed by www.google.com and verify the connection.

![IpconfigPing](https://github.com/user-attachments/assets/31652418-56f1-4957-9916-a8dc13388ce6)

7. In **Windows Server 2022**, go to **Server Manager** > **Tools** and select **DHCP** to open the DHCP management console.
8.  Click **IPv4** > **Address Leases** to verify that the **Windows 10 client** is joined to the domain.

![2IPaddedInLease](https://github.com/user-attachments/assets/ca08fecb-d90b-41e0-8929-993b92502bc0)

---

## Conclusion
Following this guide, you have successfully:
1. Installed **VirtualBox**.
2. Installed and configured **Windows Server 2022** with Active Directory.
3. Installed **Windows 10** and connected it to the domain.

