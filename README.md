# HackForTroops - Capture the Flag Repository
---
## Summary
This repository contains the challenges and information required to run the VM challenges. Note: only the challenges are stored in this repository. The webserver is stored on a seperate repository [here](https://github.com/t4t-github/CTFd).

## Finding IP addresses on any virtual machine
To retrieve the IP address for any virtual machine, log into it and run `sudo ipconfig`.

## Webserver
The virtual machine containing the webserver is: **(to be updated later)**. Once the virtual machine is started up the webserver will be run automatically. By default the webserver runs at http://127.0.0.1:8080.

Access to the administrative panel uses these credentials:
 - developer : d3ve13per<>


### Troubleshooting the webserver
In the event the webserver needs to be restarted it can be found at /home/developer/CTFd. The following commands will navigate to the proper directory, terminate the webserver, and relaunch the webserver:
``cd /home/developer/CTFd`
 - `killall -9 python3`
 - `python3 serve.py`

### Installing the webserver on a new machine
The webserver is platform independent and is based on Python3. Git and Python3 must be installed before the webserver can be properly installed. Git must also be configured with a working SSH key before `git clone` may be executed.

 - `git clone https://github.com/t4t-github/CTFd`
 - `cd CTFd`
 - `pip3 install -r requirements.txt`

# Challenges

## Virtual machines

### Samba Share
**Credentials:** developer : d3ve13per<>
**Description:** This VM is running Debian 10 on a 4GB partition. The samba share runs automatically at boot time and serves files located at /share/samba.
**Challenge information:** The competitor will need to log into the fileshare using a guest account (with no password) then search for the the flag prefix "H4T" to discover the password.
**Example commands:**
- Enumerate shares on remote machine: `smbutil view //GUEST@192.168.56.108`
- Create local mount directory: `sudo /mnt/samba`
- Mount remote share: `sudo mount -t smbfs //GUEST@192.168.56.108/samba /mnt/samba`
- Change directory `cd /mnt/samba`
- Search for "H4T" flag: ```grep -r "H4T" .```

## Web Challenges
### Web hosting details :
The following challenges are hosted on the WebChallenge virtual machine. When the virtual machine is booted up Apache webserver automatically starts and the challenges may be played.
**Credentials:**
 - root : t4Tc0mp1@ZX
 - developer : d3ve13per<>

**File locations:**
 - /var/www/html/webchal1
 - /var/www/html/webchal2

#### Web challenge 1:
**Description:** This challenge tests the competitors ability to bruteforce login prompts.
**Challenge information:** The competitor accesses the /webchal1 directory and is presented with a login screen. The default username presented in the login promp is admin. The competitor then uses a bruteforcing program such as BurpSuite or similar to discover the password.
**Flag:** H4T{THERES_A_FLAG_IN_SITE}

#### Web challenge 2:
**Description:** This challenge tests the competitors ability to manipulate cookies to bypass a login authentication mechanism.
**Challenge information:** The competitor accesses the /webchal2 directory and is presented with a login screen. The competitor views the cookie that is saved on the local machine and is shown a field for "isloggedin". The competitor then edits that cookie so that its value is "true". Editing cookies can be quickly done by using third-party browser extensions (such as EditThisCookie) or through BurpSuite.
**Flag:** H4T{OATMEAL_AND_RAISINS}
