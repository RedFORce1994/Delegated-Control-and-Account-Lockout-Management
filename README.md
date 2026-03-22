# Delegated-Control-and-Account-Lockout-Management

<h2>Overview: Account Lockout Management and Delegate Control</h2>

This repository provides documentation on the setup and configuration of a home lab environment aimed at studying "Delegate Control and Account Lockout Management." The primary goal of this lab is to investigate best practices for managing user permissions and account lockout policies within an Active Directory (AD) environment.

<h1>Objectives</h1>

- **Delegate Control**: This involves implementing and testing the delegation of administrative privileges to various users or groups in an AD environment, ensuring that access is granted with the principle of least privilege in mind.
- **Account Lockout Management**: This entails configuring and testing account lockout policies to protect accounts from brute-force attacks while also ensuring that proper exception handling is in place.

<h1>Walkthrough</h1>

In this home lab, our focus will be on comprehending **Delegation Control** and **Account Lockout**. Delegation refers to the process of granting a user limited access through **Active Directory**. To start, we will create a new user in **Active Directory Users and Computers** on our **Windows Server 2022 VM**.



1. <p align="center">
   <img src="https://i.imgur.com/51OocxW.png" height="80%" width="80%" alt="Delegation Control Steps 1"/>
   <br />
   <br />
</p>

We will establish a user with the name Wesley for both the First and Last Name, and his login username will likewise be Wesley.

2. <p align="center">
   <img src="https://i.imgur.com/rPWRMHB.png" height="80%" width="80%" alt="Delegation Control Steps 2"/>
   <br />
   <br />
</p>

Once the user Wesley has been created, we will proceed to establish a new Organizational Unit (OU). Right-click on the domain RedForce.com, choose New → Organizational Unit, and designate it as Consultants. After that, drag Wesley into the newly formed Consultants OU and click Yes to confirm.


3. <p align="center">
   <img src="https://i.imgur.com/n2PyDyK.png" height="80%" width="80%" alt="Delegation Control Steps 3"/>
   <br />
   <br />
</p>

Next, right-click on the domain RedForce.com and choose "Delegate Control".

4. <p align="center">
   <img src="https://i.imgur.com/HwJXmBU.png" height="80%" width="80%" alt="Delegation Control Steps 4"/>
   <br />
   <br />
</p>

Then add “Wesley”. 

5. <p align="center">
   <img src="https://i.imgur.com/Gj1lw18.png" height="80%" width="80%" alt="Delegation Control Steps 5"/>
   <br />
   <br />
</p>

Only grant Wesley the authority to reset passwords for other users. Check the box for "Reset user passwords and force password change at next logon." After that, click on "Next" and then "Finish."

6. <p align="center">
   <img src="https://i.imgur.com/fnT8V3c.png" height="80%" width="80%" alt="Delegation Control Steps 6"/>
   <br />
   <br />
</p>

With the setup complete, we can now log in as Wesley on our Windows 10 virtual machine. Open Active Directory Users and Computers. To review the actions available to Wesley, locate the user Bob, right-click on his account, and select Properties. Then, go to the Account tab. In the Account options section, you will notice that all options are disabled except for the User must change password at next logon option.


7. <p align="center">
   <img src="https://i.imgur.com/tgkMrwY.png" height="80%" width="80%" alt="Delegation Control Steps 7"/>
   <br />
   <br />
</p>


To confirm further, we should right-click on **Bob** and choose **Reset Password**. This action will prompt us to reset Bob's password.

Next, we will proceed to lock **Wesley's** account. Click the **Input** button at the top of the VM, select **Keyboard** → **Insert Alt + Ctrl + Del**, and then opt for **Lock**. This will deliberately lock **Wesley's** account.

8. <p align="center">
   <img src="https://i.imgur.com/aOzC6e0.png" height="80%" width="80%" alt="Delegation Control Steps 8"/>
   <br />
   <br />
</p>

To examine a user account that has been locked out, we can utilize a tool provided by Microsoft known as the Account Lockout and Management Tools. This tool can be downloaded from Microsoft’s website using the following link. Once downloaded, we will transfer the file into our RedForce Lab folder, which is accessible from our Windows Server 2022 VM.


9. <p align="center">
   <img src="https://i.imgur.com/v6Xq0Pj.png" height="80%" width="80%" alt="Delegation Control Steps 9"/>
   <br />
   <br />
</p>

Next, we need to enable shared folders on our Windows Server 2022 VM. Right-click on the folder icon at the bottom and select Share Folder Settings. For the Folder Path, locate the RedForce Lab folder in our Downloads directory. Check the box for Auto-mount and click OK.


10. <p align="center">
    <img src="https://i.imgur.com/C20SnPI.png" height="80%" width="80%" alt="Delegation Control Steps 10"/>
    <br />
    <br />
</p>

The RedForce Lab folder should now be visible as our Z: drive. Access the Z: drive, then find and open the Account Lockout and Management Tools application. Execute the tool to start the investigation.


11. <p align="center">
    <img src="https://i.imgur.com/BAjl5zq.png" height="80%" width="80%" alt="Delegation Control Steps 11"/>
    <br />
    <br />
</p>

For the extraction location, select Documents and click "OK".


12. <p align="center">
    <img src="https://i.imgur.com/7W7FY8O.png" height="80%" width="80%" alt="Delegation Control Steps 12"/>
    <br />
    <br />
</p>

To begin, access the LockoutStatus application within Documents. This tool is intended for the analysis and management of account lockouts in Active Directory settings. It proves particularly beneficial in extensive or intricate networks where account lockouts can arise from factors like misconfigured applications, issues with password synchronization, or attempts at unauthorized access.


13. <p align="center">
    <img src="https://i.imgur.com/gogszvy.png" height="80%" width="80%" alt="Delegation Control Steps 13"/>
    <br />
    <br />
</p>

Navigate to File in the top-left corner and select Select Target. Enter Wesley as the target user and click OK. This will display the User State, which shows that the account is currently locked due to 4 bad password attempts. It also provides key details, including the time of the last password attempt, the date the password was last set, the domain or origin of the lockout, and the lockout timestamp.


14. <p align="center">
    <img src="https://i.imgur.com/LuSAqEF.png" height="80%" width="80%" alt="Delegation Control Steps 14"/>
    <br />
    <br />
</p>



15. <p align="center">
    <img src="https://i.imgur.com/oOU0Kmv.png" height="80%" width="80%" alt="Delegation Control Steps 15"/>
    <br />
    <br />
</p>

Having confirmed that **Wesley’s** account is locked, we can resolve the issue by following these steps:

1. Launch **Active Directory Users and Computers**.
2. Look for **Wesley** in the **Consultants** organizational unit (OU).
3. Right-click on **Wesley** and choose **Properties**.
4. Navigate to the **Account** tab and tick the box for **Unlock account**.
5. Click **Apply** to unlock the account.

16. <p align="center">
    <img src="https://i.imgur.com/g23FspK.png" height="80%" width="80%" alt="Delegation Control Steps 16"/>
    <br />
    <br />
</p>

At this point, we can have Wesley log back into his account.

17. <p align="center">
    <img src="https://i.imgur.com/osUR45w.png" height="80%" width="80%" alt="Delegation Control Steps 17"/>
    <br />
    <br />
</p>



18. <p align="center">
    <img src="https://i.imgur.com/fpbicRY.png" height="80%" width="80%" alt="Delegation Control Steps 18"/>
    <br />
    <br />
</p>

If we execute the Lockout application once more and look for Wesley, the results will indicate that the account is no longer in a locked state.

19. <p align="center">
    <img src="https://i.imgur.com/WZvtKwY.png" height="80%" width="80%" alt="Delegation Control Steps 19"/>
    <br />
    <br />
</p>



Congratulations! We have successfully finished the home lab, acquiring a comprehensive understanding of Delegation Control and the process of investigating an account lockout using Microsoft’s Account Lockout and Management Tools.
