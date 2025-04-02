<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Network Files and Permission </h1>
This tutorial shows how to share resources over the network, including allowing users to Read,Write, or Deny access depending on the gorup and using ACtive Directory to make Security Groups.  


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Active Directory Users and Computers(ADUC)

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

  <h2>Files and Permissions </h2>

### **Step 1: Log into DC-1 and Client-1**

1. **Log into DC-1**: Use your admin account to log into **DC-1** (the Domain Controller).
2. **Log into Client-1**: Log into **Client-1** as a domain user from the previous lab session. If you're unsure about these steps, please review the following tutorials:
   - [Active Directory Setup](https://github.com/AustinmJoseph/AD-Setup)
   - [Users, Group Policy, and Account Management](https://github.com/AustinmJoseph/Users-Group-Policy-Account-Management/blob/main/README.md)

---

### **Step 2: Create Folders on DC-1's C:\ Drive**

1. Open the **C:\** drive on **DC-1**.
2. Create the following four folders:
   - **Read-access**
   - **Write-access**
   - **No-access**
   - **Accounting**

---

### **Step 3: Set Folder Sharing Permissions**

1. **Set Permissions for "Read-access" Folder**:
   - Right-click the **Read-access** folder and select **Properties**.
   - Go to the **Sharing** tab.
   - Click **Share**, then type `domain users` into the "Enter names" field.
   - Click **Add**, and assign **Read** permissions.

2. **Set Permissions for "Write-access" Folder**:
   - Right-click the **Write-access** folder and select **Properties**.
   - Go to the **Sharing** tab.
   - Click **Share**, then type `domain users` again.
   - Click **Add**, and assign **Read/Write** permissions.

3. **Set Permissions for "No-access" Folder**:
   - Right-click the **No-access** folder and select **Properties**.
   - Go to the **Sharing** tab.
   - Click **Share**, and add `domain admins`.
   - Assign **Read/Write** permissions to **domain admins**.

4. **Leave the "Accounting" Folder**:
   - No changes are needed for the **Accounting** folder at this time.

---

### **Step 4: Verify Folder Access from Client-1**

1. Log into **Client-1** using one of your domain user accounts.
2. Open **File Explorer** and enter `\\dc-1` in the address bar to view the shared folders on **DC-1**.
3. Check the following:
   - **No-access** folder: You should not be able to access this folder.
   - **Read-access** folder: You should only be able to **read** files (modifying files is not allowed).
   - **Write-access** folder: You should be able to **read and write** files (adding or editing documents is allowed).

---

### **Conclusion**
- You've successfully set up and tested folder permissions within a domain environment.
- The different access levels (Read, Write, No Access) should now function as expected when accessed from **Client-1**.

---

  <h2>Security Groups</h2>



### **Step 1: Create an Organizational Unit (OU) in Active Directory**

1. **Log into DC-1**: Open **Active Directory Users and Computers (ADUC)** on **DC-1**.
2. **Create a New Organizational Unit (OU)**:
   - Right-click on your domain name, select **New**, and then choose **Organizational Unit**.
   - Name the new OU `_TEAMS`.

---

### **Step 2: Create a New Group for Accountants**

1. **Create a Group**:
   - Right-click on the newly created **_TEAMS** OU, then select **New** and choose **Group**.
   - Name the group **ACCOUNTANTS**.

---

### **Step 3: Set Permissions for the Accountants Folder**

1. **Go to the "Accountants" Folder**: Navigate back to the folder you created earlier for **ACCOUNTANTS** (the one you set permissions for).
2. **Set Permissions**:
   - Right-click the **ACCOUNTANTS** folder and select **Properties**.
   - Go to the **Security** tab.
   - Click **Edit** and add the **ACCOUNTANTS** group.
   - Assign **Read/Write** permissions for the group.

---

### **Step 4: Test Access from Client-1**

1. **Log into Client-1** as a domain user who is not yet part of the **ACCOUNTANTS** group.
2. Open **File Explorer** and navigate to the **ACCOUNTANTS** folder by typing `\\dc-1` in the address bar.
3. **Verify Access**:
   - You should not be able to access the **ACCOUNTANTS** folder, as the user isn’t part of the group yet.

---

### **Step 5: Add the User to the ACCOUNTANTS Group**

1. **Go Back to DC-1**: Log back into **DC-1**.
2. **Add the User to the ACCOUNTANTS Group**:
   - In **Active Directory Users and Computers (ADUC)**, find the **Security Group** for the user you want to add.
   - Right-click on the user and select **Properties**.
   - Go to the **Member Of** tab, click **Add**, and type **ACCOUNTANTS** to add the user to the group.
   - Click **OK** to save the changes.

---

### **Step 6: Test Access Again from Client-1**

1. **Log Back into Client-1**: Sign out and log back into **Client-1** with the same user account.
2. Open **File Explorer** and type `\\dc-1` again to access the **ACCOUNTANTS** folder.
3. **Verify Access**:
   - This time, you should be able to access the **ACCOUNTANTS** folder, as the user is now part of the **ACCOUNTANTS** group with **Read/Write** permissions.

---

### **Conclusion**
- You've successfully used Active Directory to manage folder permissions by creating a group and adding users to it.
- The permissions should now work correctly, allowing group members to access the **ACCOUNTANTS** folder as intended.

---

  
