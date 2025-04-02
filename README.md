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

  To start off lets log into DC-1 as your admin account and CLient-1 from a random user from our last lab. If your not sure what im refering to please revieww [Active Direvtory Setup](https://github.com/AustinmJoseph/AD-Setup) and [Users-Group Policy-Account-Managment](https://github.com/AustinmJoseph/Users-Group-Policy-Account-Management/blob/main/README.md) tutorial. Now that youve signed into both accounts go into DC-1's C:\ drive, and make 4 folders Read-acces, Write-access, no-acces, and accounting. After youve made the folders right click one go to properties > SHaring > Share > and then type in domain users and click add and give read only read permissins, repeat these steps for the write but put that one as read/write. For no-access put domain admin and give it read write. and leave accounting alone for now. make sure that you configure the folders to read or read/write. Now log into Client one as one of your domain users, go to files and at the top type in \\dc-1 to view the folders. Notice how you can not access no acces, you can only read in read access, and in write you can read and add documents to the folder.


  <h2>Security Groups</h2>

Now that we know how to mess with permissions with files explorer lets try using active directory to give permissions to certain groups. Go back to DC-1 and open ADUC and make a new orgizantional unit, I named my _TEAMS. then right click _TEAMS and click group and name it ACCOUNTANTS. Then go back to the accountants folder we made put in ACCOUNTANTS and give them read/write permissions. Try accessing the accountants folder from your CLient-1 user it shouldnt work sign out and go back to DC-1 and in the accounts Security Group add that user to the ACCOUNTANTS group then sign back into Client-1, you should be able to access it.
  
