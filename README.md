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

### Step 4: Start the VM and Install Windows Server 2022
1. Click **Start** to boot the VM and begin installation.
2. In the Windows Setup screen, choose your **language**, **time**, and **keyboard layout**.
3. Click **Install Now**.
4. Select the version of **Windows Server 2022** you want (choose **Desktop Experience** for GUI) and click **Next**.
5. Accept the license agreement and click **Next**.
6. Choose **Custom: Install Windows only**.
7. Select the virtual hard drive, click **Next**, and the installation will begin.

### Step 5: Configure Windows Server 2022
1. After the installation completes, set a **strong password** for the Administrator account.
2. Once logged in, open **Server Manager** for initial configurations:
   - Set a **static IP address**.
   - **Change the computer name** (optional).
   - **Enable Remote Desktop** (optional).
   - **Install Windows Updates**.
3. Reboot if necessary.

### Step 6: Install Active Directory Domain Services (AD DS)
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

