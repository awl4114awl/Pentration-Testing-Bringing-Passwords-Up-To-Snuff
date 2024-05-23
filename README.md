<p align="center">
<img src="https://i.imgur.com/ARGlAoP.png" height="50%" width="50%" alt="install kali"/>
</p>
<h1>Pentration Testing: Bringing Passwords Up to Snuff</h1>

    We have reason to believe that some of our employees have weaker than should be acceptable passwords, so we want you to conduct authorized penetration testing against various company assets to determine which employees need to change their passwords.

<h2>Solution</h2>

    Utilize Kali Linux to target Pretty Safe Electronic's Active Directory located at 171.16.30.55.

    - Use Metasploit's Auxiliary module smblookupsid to enumerate authorized users in the directory.
    - Utilize Hydra, leveraging Metasploit's output, to target specific users in the directory.
    - Employ the "rockyou.txt" wordlist to identify weak passwords among users.

    Reset passwords for identified users with weak passwords.

    - Access the domain controller and initiate password resets for users flagged with weak passwords.

<h2>Tools Used</h2>

    Kali Linux
    Metasploit Console
    SMB
    smb_lookupsid Auxiliary in Metasploit
    Hydra command line tool
    Active Directory (Users and Computers)

<h2>Network Map and targets used</h2>

    Our target is the AD-Server located at 172.16.30.55
    We will utilize the Security-Desk workstation located at 172.16.20.55
<img src="https://i.imgur.com/Ms9L7zn.jpeg" height="80%" width="80%" alt="NICE Challenge"/>

<h2>Actions Taken</h2>

    1. Activate the Security-Desk workstation and log in to player one.
    2. Launch Terminal and execute "sudo msfconsole".
    3. Select the smb_lookupsid tool by running "use auxiliary/scanner/smb_lookupsid".
    4. Set the target to Active Directory service with "set RHOSTS 172.16.30.55".
    5. Specify SMB user with "set SMBUser playerone".
    6. Set SMB password using "set SMBPass password123".
    7. Commence exploit with "exploit".
    8. After completion, copy and paste the output into MousePad.
    9. Remove extraneous data, leaving only found users:
        rcortes
        jsmith
        manderson
        skeefe
        nkeefe
        asteele
        jraffin
        jcortes
        tclark
    10. Save the document in the home directory (/home/playerone/(KNOWNUSERS).txt).
    11. Create an empty document for Hydra's output in the home directory (/home/playerone/(OUTPUT).txt).
    12. Exit the Metasploit console.
    13. In Terminal, execute "hydra -L /home/playerone/(KNOWNUSERS).txt -P /usr/share/wordlists/rockyou.txt -o /home/playerone/(OUTPUT).txt -v 172.16.30.55 smb". 
        Hydra identifies two users with weak passwords:
        nkeefe:987654321
        jcortes:iloveme
    14. Shutdown Security-Desk.
    15. Initiate Domain-Controller.
    16. Navigate to Start Menu > Administrative Tools.
    17. Open Active Directory Users and Computers.
    18. Access prettysafeelectronics.io > Users.
    19. Adjust the password policy for Jan Cortes (jcortes) & Naomi O'Keefe (nkeefe):
        - Select the respective user and open properties from the secondary menu.
        - Navigate to the account tab.
        - Uncheck [Password never expires].
        - Check [User must change password at next logon].
        - Apply changes.
    20. Repeat for the second user.

<h2>Report</h2>
<br />
<br />
<img src="https://i.imgur.com/WcwS8N4.png" height="80%" width="80%" alt="NICE Challenge"/>
<br />
<br />
<img src="https://i.imgur.com/LvN5xX3.png" height="80%" width="80%" alt="NICE Challenge"/>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
