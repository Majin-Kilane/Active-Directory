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
- configuring auditing policies to trackuser activities, login attempts, and changes in AD objects.
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

![0](https://github.com/user-attachments/assets/7ea7778f-6e38-4aa7-8652-16d7f973a503)

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

![4SelectIPv4](https://github.com/user-attachments/assets/589764e6-16e6-41c1-bed4-f71fb25e825f)

5. Choose **Use the following IP address** and enter the following details:
   - **IP address**: Choose an IP, e.g., 192.168.1.10.
   - **Subnet mask**: Use 255.255.255.0.
   - Leave **Default gateway** and **DNS server** fields blank (for isolated networks).

![5ChooseIP](https://github.com/user-attachments/assets/d38e6428-2836-4257-b0f6-18e9f22d0144)

6. Click **OK** to save settings.

   - **Change the computer name** (optional).
   - **Enable Remote Desktop** (optional).
7. Reboot if necessary.

### Step 9: Install Active Directory Domain Services (AD DS)
1. In **Server Manager**, click **Add Roles and Features**.
2. Select **Role-based or feature-based installation**, click **Next**.
3. Select the server and click **Next**.
4. In the **Roles** section, select **Active Directory Domain Services** and click **Next**.
5. Click **Install** to install the AD DS role.
6. After installation, click **Promote this server to a domain controller**.
7. In the AD DS configuration wizard, choose **Add a new forest** and enter a **domain name** (e.g., `example.com`).
8. Follow the prompts to complete the domain controller configuration and restart the server.

---

## Installing Windows 10 on VirtualBox

### Step 1: Download Windows 10 ISO
- Visit the [Microsoft Windows 10 Download Page](https://www.microsoft.com/software-download/windows10) and download the ISO.

### Step 2: Create a New Virtual Machine for Windows 10
1. Open **VirtualBox** and click **New**.
2. Name the VM (e.g., **Windows 10**).
3. Set **Type** to **Microsoft Windows** and **Version** to **Windows 10 (64-bit)**.
4. Allocate at least **2048 MB** of RAM (preferably 4096 MB).
5. Create a **Virtual Hard Disk** with at least **50 GB** of storage.
6. Click **Create**.

### Step 3: Mount Windows 10 ISO
1. Select the **Windows 10 VM** in VirtualBox and click **Settings**.
2. Go to **Storage**, click the **Empty** disk under **Controller: IDE**, and select **Choose a disk file**.
3. Browse and select the **Windows 10 ISO** you downloaded.
4. Click **OK**.

### Step 4: Start the VM and Install Windows 10
1. Click **Start** to boot the VM from the ISO.
2. In the **Windows Setup** screen, choose your **language**, **time**, and **keyboard layout**.
3. Click **Install Now**.
4. Enter a **product key** or select **I don’t have a product key** to skip.
5. Choose the Windows 10 edition to install and click **Next**.
6. Accept the license agreement.
7. Select **Custom: Install Windows only**.
8. Choose the virtual hard drive you created and click **Next** to begin the installation.

### Step 5: Configure Windows 10
1. Once the installation completes, set up your **user account**, **region**, and **network settings**.
2. Follow the prompts to complete the Windows 10 setup.

### Step 6: Join Windows 10 to the Active Directory Domain
1. In Windows 10, open **File Explorer**, right-click **This PC**, and choose **Properties**.
2. Click **Change settings** next to the computer name.
3. Click **Change** and under **Member of**, select **Domain**.
4. Enter the **domain name** (e.g., `example.com`).
5. When prompted, enter the **Administrator** username and password of your Windows Server domain.
6. Restart the Windows 10 VM to complete the domain join.

---

## Conclusion
Following this guide, you have successfully:
1. Installed **VirtualBox**.
2. Installed and configured **Windows Server 2022** with Active Directory.
3. Installed **Windows 10** and connected it to the domain.

