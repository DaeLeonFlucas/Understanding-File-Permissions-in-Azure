<h1>Understanding File Permissions</h1>
In this lab, we focus on managing file permissions and shares in the context of an Active Directory domain. Proper file permissions and shares are vital in a business setting to grant users the appropriate access to the files they require. This builds upon a prior lab where I have a client connected to the domain ernestotest.com. I am logged in as Jane Doe (administrator) on the domain controller VM and as a regular user on the client VM <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>File Permissions Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/bUjobDC.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/lz1DMos.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
To set permissions on folders and files, we first need to create the folders to share. While logged into the domain controller VM as an administrator, I created four appropriately named folders on the C:\ drive. To share a folder and assign permissions, open the folder’s Properties and navigate to the Sharing tab, then click on Share. From here, you can specify which users on the network can access the folder and assign the appropriate permissions. The following permissions were set for the folders (the accounting folder will be adjusted later):

Domain Users are granted Read access to the read-access folder and Read/Write permissions on the write-access folder. Domain Admins, on the other hand, have Read/Write access to the no-access folder.
</p>
<br />

<p>
<img src="https://i.imgur.com/kWrpLFE.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
When accessing shared folders on the client VM, you can find them by navigating to \dc-1 in File Explorer. Some folders will only let you view the files, while others won’t grant access at all. This occurs because folder permissions are tied to the user's Security Group and the specific permissions set for that group.
</p>
<br />

<p>
<img src="https://i.imgur.com/NgM0CcI.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/I4k9T2J.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
The next step involves creating a Security Group and granting it the proper permissions for the accounting folder. In the Active Directory Users and Computers panel on the domain controller, create a group called ACCOUNTANTS. Afterward, assign Read/Write permissions to the accounting folder for the new ACCOUNTANTS group.
</p>
<br />

<p>
<img src="https://i.imgur.com/xev1Svv.png" height="80%" width="80%" alt="Permissions Steps"/>
<img src="https://i.imgur.com/SHotVB2.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
Access to the accounting folder is denied for the user since they are not part of the ACCOUNTANTS Security Group. To correct this, log off from the client to allow the permissions to take effect when the client logs back in. On the domain controller, open the ACCOUNTANTS group in Active Directory Users and Computers. In the Members tab, add bon.rovej to the group. After logging back in, bon.rovej will now have access to the accounting folder.
<br />

<h2>Lessons Learned </h2>

In a professional scenario, it's important to configure permissions carefully, ensuring that users only have access to the files they need to perform their tasks. Granting more permissions than necessary is not recommended.
