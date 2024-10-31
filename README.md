## Lab Infrastructure Overview

![Infrastructure Diagram](infrastructure-diagram.png)

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
- Configuring security groups and assigning permissions based on roles.
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
*Ref 1: Network Diagram* 



1. Run the downloaded installer.
2. In the setup wizard:
   - Click **Next** on the welcome screen.
   - Choose installation location or leave it as default, and click **Next**.
   - Leave default settings for features and click **Next**.
   - Click **Yes** on the network warning if it appears.
   - Click **Install** to complete the installation.
3. After installation, click **Finish** to launch VirtualBox.

*Ref 2: Virtualbox Installation Complete Diagram* 



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
   
![image alt](https://github.com/user-attachments/assets/5a3d32ff-354d-499b-b1a6-ecd6ce20ec43)

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
  

-----**ADD LOGIN PAGE**------
   
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

![3OpenProperties](https://github.com/user-attachments/assets/af9f303b-7b40-4253-8aa5-64951bc39944)

4. Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.

![4SelectIPv4](https://github.com/user-attachments/assets/4a485deb-9583-416a-a746-6cb188396aad)

5. Choose **Use the following IP address** and enter the following details:
   - **IP address**: Choose an IP, e.g., 192.168.1.10.
   - **Subnet mask**: Use 255.255.255.0.
   - Leave **Default gateway** and **DNS server** fields blank (for isolated networks).
   - Set the loopback IP 127.0.0.1 to use this server as the DNS server.

![5ChooseIP](https://github.com/user-attachments/assets/d38e6428-2836-4257-b0f6-18e9f22d0144)

6. Click **OK** to save settings.

   - **Change the computer name** (optional).
   - **Enable Remote Desktop** (optional).
7. Reboot if necessary.

### Step 9: Install Active Directory Domain Services (AD DS)
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

![11AddNewForest DomainName](https://github.com/user-attachments/assets/beaf343c-c532-4039-9963-a5285e7336d7)

12. Create a password.

![12CreatePW](https://github.com/user-attachments/assets/88ebdf9e-8246-4f3c-8000-a1ad72a56e30)

13. Uncheck **Create DNS delegation** and press **Next**.

![12UncheckCreateDNSDel](https://github.com/user-attachments/assets/9b1a2d6d-34cb-44b4-9071-2e543d242456)
   
14. Follow the prompts to complete the domain controller configuration and restart the server.
 
![18DomainAdminLogin_Copy](https://github.com/user-attachments/assets/9db58aba-59c7-4d2f-bb85-c61e4c3560ab)

15. Click **Start** and select **Administrative Tools**.

![19Start](https://github.com/user-attachments/assets/384b9000-95e5-450a-9d65-e23851e4edd3)

16. Select **Active Directory Users and Computers**.

![20ADUser Comp](https://github.com/user-attachments/assets/6bcab368-5607-4a5b-86ff-070156b11dbf)


## Create Users (Manually and in Bulk)
### Step 1: Create a New Administrator User Account
1. Click **Start** > **Windows Administrative Tools** > **Active directory Users and Computers**.

![1Start](https://github.com/user-attachments/assets/6d9648a2-521c-414b-8b69-e0e5d8c530a4)

2. Open **Administrators**, right-click and select **New** > **Users**.

![2CreateAdminUser](https://github.com/user-attachments/assets/ee488336-1f72-43ff-90ca-891d6a2a310f)

3. In the New User window, enter the following details:
   - Username: The name you want to assign to the new admin account.
   - Full Name: The full name of the user.

![3EnterDetails](https://github.com/user-attachments/assets/b161030d-aac3-4466-af90-abc3b692f83e)

   - Description: Add a description (optional).
   - Password: Set a strong password for the account.
4. Uncheck User must change password at next logon if you do not want this prompt.
5. Check Password never expires if you want the password to be static (optional).
6. Click **Finish** to complete the user creation.

![4Finish](https://github.com/user-attachments/assets/64f68f06-2223-49a5-aeb9-54dbbcb4f2cc)

7. Navigate to the **Administrator** OU/ folder to verify if the user was created.

![5UserCreated](https://github.com/user-attachments/assets/d8393915-d4ac-47e5-b7cb-a38a49948504)


### Step 2: Create Bulk users
1: Open 

## Configuring NAT on Windows Server 2022

### Step 1: Open Server Manager and Install the Routing and Remote Access Role
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

### Step 2: Configure Routing and Remote Access
1. Once installed, go to **Tools** in Server Manager, then select **Routing and Remote Access**.

![1Routing RA](https://github.com/user-attachments/assets/0b01140c-039b-4ee3-9e54-6f1ef623fa8e)

2. In the **Routing and Remote Access** window, right-click on your server name and select **Configure and Enable Routing and Remote Access**.

![2Configure](https://github.com/user-attachments/assets/751bcdfd-9234-49f8-bb0f-9be41fe0c496)

3. In the **Routing and Remote Access Server Setup Wizard**, click **Next**.

![3Next](https://github.com/user-attachments/assets/3a5f82da-3ec3-4411-8339-3536fbc21693)

4. Choose **Network Address Translation (NAT)** and click **Next**.

![4ChooseNAT](https://github.com/user-attachments/assets/7001b880-fc62-4d34-b99a-b42d91877dc4)

5. Select the network adapter connected to the external network (public/internet) and click **Next**.
   - This interface is typically the one with internet access.

![5ChooseInterface](https://github.com/user-attachments/assets/21bd46f2-5ae3-45ea-9cfc-d579ce51339a)

6. Select **Finish** to complete the configuration.

![6finish](https://github.com/user-attachments/assets/8e77b88b-1881-4ba0-9f76-1bbb5c84fcea)

### Step 2: Configure Internal Network Interface
1. In the **Routing and Remote Access** window, expand your server node, then expand **IPv4**.

![2ExpandIPv4](https://github.com/user-attachments/assets/70c9170d-f928-4b08-90a0-ccde1fe99db3)
   
2. Right-click **NAT**.
3. Choose the network adapter connected to the internal network (private network) and click **OK**.

![3SelectInNet](https://github.com/user-attachments/assets/e5e23a14-781f-4a00-8bdf-f7ea00c6b2ae)

4. In the **NAT Interface Properties** window, select **Private interface connected to private network** and check **Enable NAT on this interface** if it is not already selected.

![4EnableNAT](https://github.com/user-attachments/assets/ec22eb52-bb5b-401e-a656-521752f09dfd)

5. Click **Apply**, then **OK** to save the settings.

## Setting Up a DHCP Server on Windows Server 2022
### Step 1: Open Server Manager and Add Roles and Features
1. Log in to **Windows Server 2022** with an account that has administrative privileges.
2. Open **Server Manager**.
3. Click **Add Roles and Features**.
4. In the **Add Roles and Features Wizard**, click **Next** through the introductory screens until you reach the **Server Roles** section.

![1Add](https://github.com/user-attachments/assets/a30e6115-a67a-421d-a61f-ff2ecd715bbd)

### Step 2: Install the DHCP Server Role
1. In **Server Roles**, check **DHCP Server** and click **Next**.

![2DHCP](https://github.com/user-attachments/assets/1f58a41f-b46e-47c3-821b-6d2ff8d8dae1)

2. Continue through the wizard, leaving the default settings, and click **Install** on the confirmation screen.

![3Install](https://github.com/user-attachments/assets/990f1658-032e-4bb6-8f4e-8af179b7808d)

3. Wait for the installation to complete, then click **Close**.

### Step 3: Complete DHCP Configuration
1. After installation, go back to **Server Manager**.
2. At the top, you should see a notification flag; click it and select **Complete DHCP Configuration**.

![4YellowFlag](https://github.com/user-attachments/assets/129fcf8b-06a3-4999-88dd-399fbc6b43d0)

4. In the **DHCP Post-Install Configuration Wizard**, click **Next**.
5. Choose to **Use the following user account** (usually the default network service account) and click **Next**.
6. Click **Commit** to apply the configuration.

![5Commit](https://github.com/user-attachments/assets/82c826d8-943b-4809-aadf-56f190491341)

7. Click **Close**.

![6Close](https://github.com/user-attachments/assets/c80c2b7a-57c4-48ce-b4c7-d7546cd5cd86)
   
### Step 4: Open DHCP Management Console and Create a New Scope
1. In **Server Manager**, go to **Tools** and select **DHCP** to open the DHCP management console.

![7Tools](https://github.com/user-attachments/assets/4a1a257f-9825-4f8b-bb51-ebcc96c07fd0)

2. In the DHCP console, expand your **Server Name** and right-click on **IPv4**.
3. Select **New Scope** to launch the **New Scope Wizard**.

![8NewScope](https://github.com/user-attachments/assets/2362bd6b-0ed5-44ae-a552-277365454f41)

### Step 5: Configure the DHCP Scope
1. In the **New Scope Wizard**, click **Next**.
2. Enter a **Name** and optional **Description** for the scope (e.g., "Office Network").

![9AddName](https://github.com/user-attachments/assets/69e3d57c-93f7-4665-9076-965869c93164)

3. Specify the **IP Address Range**:
   - **Start IP Address**: The first IP in the range (e.g., 192.168.1.100).
   - **End IP Address**: The last IP in the range (e.g., 192.168.1.200).
   - **Subnet Mask**: Based on your network (e.g., 255.255.255.0).
  
![10SpecifyIP](https://github.com/user-attachments/assets/2dd61190-5032-4689-bae9-49353fc4139d)

4. Click **Next**.

### Step 6: Set Lease Duration
1. Specify the **Lease Duration**, which is how long a device can keep an IP address before it’s reassigned (default is 8 days).

![11Lease](https://github.com/user-attachments/assets/e4d4cdaa-c4e6-48f4-bcf5-864e4b791dc3)

2. Click **Next**.

### Step 7: Configure DHCP Options
1. You can now configure **DHCP options** (gateway, DNS servers, etc.):
   - **Router (Default Gateway)**: Enter the IP address of your network's default gateway.
  
![12AddDefaultGateway](https://github.com/user-attachments/assets/c55ef7fa-909e-4130-b233-8076cfe6f742)

   - **DNS Servers**: Specify the IP address of DNS servers to use (e.g., your internal DNS server).

![13AddDNS](https://github.com/user-attachments/assets/321716af-7f17-4014-805e-b4cc2aaadf4e)

   - Click **Next** after each configuration option.

### Step 8: Activate the DHCP Scope
1. At the **Activate Scope** step, select **Yes, I want to activate this scope now** and click **Next**.

![14ActivateScope](https://github.com/user-attachments/assets/8f6a7255-85e0-4fe0-9cf7-09e8048fee0b)

2. Click **Finish** to complete the setup.

### Step 9: Verify DHCP Configuration
1. **Restart DHCP** services if necessary.
2. Connect a client device to the network and check if it’s receiving an IP address from the DHCP server by running ipconfig on the client.



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

