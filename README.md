# Linux

<h1>File Commands</h1>

<h3>Create-Files</h3>
	touch .filename.txt
Create a hidden file, put a "." before the file name
<br>

Create multiple files with one command
<br>
+ touch filename{1..10}

Creates 100 files with the name filename1-3 
<br>
+ touch filename {file1,file2,file3} {1..100} {a..z}

Create a file with a dash	
<br>
+ touch -- -filename	

Remove file with a dash    	
<br>
+ rm -rf -- -filename	

Remove all file except file1
<br>
+ rm -rf !(file1)		


<h2> Vi Editor Shortcuts </h2>
[CTRL-C] to exist insert
:wq to write and quit
SHIFT Z Z in vi editor to save and quit, similar to :wq
:view /etc/passwd  to view a file inside the vim editor
:11,15d  delete line from 11~15
:5,15s/current-word/new-word/g new word from line 5~15

yy [to copy the text] 	p [to paste the text you copied
dd [to cut the text]
/ssh to search for the word “ssh”


<h4> Display-Files:</h4>
+ stat  /path/folder/file  
Get detailed information of files and or directories, inlcuding date of creation, inode, ownership, etc..
<br>

+ file  /path/folder/file  
read the  information on file type
cat > filename		 [ > overrides  :Receptors:   >> saves]
Edit a file on the fly	
less filename.txt 
Display the content inside a file NOTE: INTERACTIVE
lsof -i :80 -u faze
-i internet address |  -u user | flags can be used independently

<br>
+ tree / -LaphD 1
Display content in a tree format inside.  | Package must be installed to utilize tree command 

<br>
+ wc --line < file-name.txt
Show the number of lines inside the file.
<br> 		    
+ ls -al filename 2> output.txt
 Displays the all folders and files, including hidden onto the console. 2 redirects the output from the console to the output.txt file

diff -c file1 file2                               sdiff file 1 file2
-c is for context
! Signals the difference of the lines
+ Signals the content was added
- Signals the content was removed 
awk ‘{ if (NR == 10) print “new”; else print $0}’  input_file.txt > output_file.txt

head -n 20 /etc/file.log		tail -n 20 /etc/file.log
View first 20 lines of the file	View last 20 lines of the file


<h4> Copy-Files: </h4>

+ cp -r -a  /src/file /destination/file .
- r recursively.  | - a attribute preserving state.  
<br>

+ scp -rv faze@192.168.244.146:/home/faze/file C:\Users\Faisa\Desktop
Copy from remote machine (linux) to a remote machine (windows) using powershell
<br>

scp -rv C:\Users\Faisa\Desktop\file.txt faze@ip:/home/faze/folder
Copy from local machine (windows) to a remote machine (linux) using powershell, make sure to give file extension.
scp -rv filename faze@192.168.50.240:/home/faze/folder/securecopy/
Copy from linux to linux machine
scp faze@192.168.50.240:/path/from/where/you/want/file
Fetch the file from specified path 

mv -iv filename [new-file-name]
Mv allows us to rename and or mv a file to a different location 
- i interactive | - v verbose

sed 's/current-text/new-text/g' file.txt
s is for search and replace
g is for global search and replace
sed -i  's/current-text/new-text/g' file.txt
-i stands for in-place
Command above will implement the changes






Compress-Files (tar) (gzip):  
What is Tar?  
Tar Bundles all the files like gzip but it does not compress the files like gzip

tar -cf name-of-tar-file current-file-name-to-tar     
Create a tar file. 
TIP: .tar is not required, but is standard practice.
-c flag to create. 
-f flag is to specify that it's a file.

tar -cvfz name_backup.tar.gz current-file-name-to-tar
Create a tar with gzip, referred to as a “tar ball”

tar -tvf etc_backup.tar | wc -l
To view inside the tar file
-t flag for type
-v flag for verbose
-l flag is for listing 

tar -xvf [filename] 
Extract the tar file to original content 
-x flag is for extracting
-f flag is to a file
-z flag is for zip

gzip [file-name]
Zip the file
gunzip [file-name]
Unzip the file

cut -d ' ' -f 1 textfile.txt
-d is the delimiter 
-f is the field 
cut will show user what they specify in the -d (delimiter) -f(field)

uniq -c file.txt
-c counts for each unique occurrence 
removes duplicates when searching for a file.
NOTE: Only removes duplicates that are adjacent to each other
first sort the items then uniq for accurate results.
sort -nr file.txt
-n numerical order Arranges the data in numerical order
-r reverse order  Arranges the data in descending order
cat /root/file | awk ‘{print $1}’ |sort -nr | uniq -c
An Example command which utilizes both sort and uniq

crontab -u  root  -e [edit] -l [list]
File where you set-up cron jobs. cronjobs are scripts
That automates tasks.









User Commands:
USER ESSENTIAL:		Cat /etc/passwd
compgen -u
Display the users on the machine, with minimal information
Id [username]
Display the details of the active user.
last
Display the last login user
who
Display who’s logged into the system
getent group sudo 
Check what group has sudo power

passwd -S [username]
1.) The username
2.) Password status Locked (L), No Password (NP), Password (P)
3.) Date of last password change
4.) Minimum password age
5.) Maximum password age
6.) Warning period  (days given before password expires.)
7.) Inactivity period (days after a password expires before it is locked.)

chage -l [username]    
Check the users password settings, such as,
Last password change
Password expires
Password inactive
Account expires




chage -E 2023-01-30 [username]
Set the expiration date for a user 

chage -M 30 [username]
Password will expire after a maximum of 30 days 
chage -m 7 [username]
Minimum amount of days the user can his/her password
chage -M -1 [username]
Remove the password expiration date

ps -aux |grep [username] 
List the process on a user
pkill -f [proccess-name]
Kill a process with the process name
killall -TERM -u [username]
Kill the process on a user
















UserAdd:
adduser [username] -s /sbin/nologin 
Create a user with a non-interactive shell
adduser [username] -s /bin/bash  
Create a user with the bash shell. the -s flag stands for shell

sudo useradd  -u 1100 [username] 
Create a user with 1100 uuid
sudo useradd  m [username] 
Create a user with a home directory  
sudo useradd  --system [username]
Create a user with a system account, system account does not have a /home directory, usually daemons use system account.

echo -e “john” | passwd --stdin “123456me”
Create a user with the username john and password will be 123456me.


UserDelete:
sudo userdel [username] sudo
Remove the user named username from the group sudo.
userdel -rf [username]
The -f would forcefully remove this user, including the user’s home directory/mail (if any) 




UserMod:
usermod -l [current-name] [new-name] 
Change the username for a user
-l  stands for --login
usermod -L [username]
Lock a user, they will not be able to login, possibly login through ssh-keys if it’s previously setup
usermod -U [username]
Unlock a user
usermod -aG sudo | wheel [username] 
Give root privilege to a user, depending on os, sudo or wheel
usermod -g wheel or sudo [username]
Change the primary group of user 

usermod [username] -s /bin/bash 
Change the users $Shell to /bin/bash
usermod [username] -s /sbin/nologin 
Change the users $Shell to /bin/nologin

chown tsi:tsi [filename]
Change file ownership
chmod 440 [filename]  
Change file permissions,
user   group    others
-r w x      - r w x     - r w x        The first - indicates that it’s a file
 4 2 1   	  4 2 1   	  4 2 1
Each category has 3 read/write/execute permissions 

chmod -R 777 /app/binary/scripts/
The -R is for recursive meaning all.


USER GROUP COMMANDS:     Cat /etc/group
groupadd [name-of-group]
Create a group
groupdel [group-name]
Delete the group
chgrp [group-name]  /folder/or/file.txt
Change the group

NOTE: CAN ONLY HAVE ONE PRIMARY GROUP.
gpasswd -a [username] [group-name]
Add a user into the group
gpasswd -d [username] [group-name]
Remove a user from the group
usermod -g [group-name] [username]
Change the users primary group
usermod -G [group-name] [username]
Change the users secondary group
groupmod -n [new-name] [current-name]
will change the groups name

groups [username]
Check the users group
E.G john: john developers
john is the primary or considered login group
developers is the secondary or supplementary group

	SUID, SGID, and sticky bit

SetUID - 4 	(Set User Identification)
E.G. chmod 4664 filename		(Numerical method)   
E.G. chmod +u  				(Symbolic  method)
SetUID bit in Linux helps to execute a command with owner rights.


SetGID - 2 	(Set Group Identification)
E.G. chmod 2664 filename	  	(Numerical method) 
E.G. chmod +g  				(Symbolic  method)

SetGID in Linux is used to assign the same Group Owner to all the files and sub-directories within a directory

Sticky Bit - 1 
E.G. chmod 1666 				(Numerical method) 
E.G. chmod +s  				(Symbolic  method)
Sticky bit in Linux prevents the deletion of a file from other than its owner i.e., if sticky bit is set on a directory then the files within the directory can be deleted only by the file owner.









Hardware Commands:
free -hm
- h human  | - m memory 
systemd-cgtop
Check for memory / cpu usage with Systemd systems
smem -k -u -p -t
Check swap memory 
top -O +%CPU
Displays: the total CPU usage 
htop
Displays: the total usage 
glances
Similar to top but more enhanced, must be installed,

ps -aux
Check running process  - a all  | - u user | -x executable 
pkill -f [proccess-name]
Kill a process with the process name
killall -TERM -u [username]
Kill the process on a user

uptime
List the systems load 
iostat 
Lists all the Input / output devices 
kmod list
List all the kernel modules on the machine 
env    	
List all the environment variable files on the machine
sar -r 
System Activity Report: Captures check swap memory 

strace -w -c [command] 

fdisk -l
Check the device blocks, disks, partition - l list
df -Th
DiskFree shows the blocks allocated in the entire file system, including inodes and other metadata
- T type  | - h human
du -hs
DiskUsed shows the blocks actually allocated to an individual file.
-  human  | - s size

lsblk
Checks the device's blocks, disk, disk-space, disk-name, etc..
lscpu   
Displays information about cpu
lsusb
Display the usb devices connected 
lspci -nn | grep -i net
Display all the Pci express 
lshw -C [cpu] [network]
List detailed information of configuration - C class  

netstat -a -n -t -p -e -r -l 
Display ports
- a all  | - n network | -t tcp  | - p protocol | -r routing | -l listening 
ip r 
Checks the routing of the network
arp -a 
Displays the specific interface(NIC) a MAC address is connected to, and how long to keep the ARP entry within the table.
route 
Print the routing table, this tells users where traffic exits.

history -c 
Clear all history 

Iwconfig 
iwconfig is similar to ifconfig, but is dedicated to wireless networking interfaces

rcpinfo -p | grep nfs
Remote Procedure call (rpc)

nmap -p 1-100 10.0.0.77 
- p port  | -p- scans all ports 0-65535 

fuser -k -n tcp 22 
- k kill  | - n number port
Will remove the specified, port

nmap -sn -oG output_file_name 192.168.50.2/24

nmap --iflist
The “-iflist” command is used to find out routes and host interface information. 


NMCLI Commands:
Oracle/Redhat/Centos/Fedora 

ip addr show 
Shows the ip address similar to ifconfig / ip -4 a
ethtool [nic-name]
Shows the links

nmtui
The GUI version of nmcli 
curl cheat.sh/nmcli
Display a cheat-sheet for nmcli configuration
nmcli con show [ens160] <----- 
Show the connection information 
nmcli general permissions
Show the connection permissions
nmcli general status
View the status of the state 
nmcli dev
Check the status of the device
nmcli con add con-name “en2” ifname “eth0” type "ethernet"  ipv4.adresses 10.0.0.1/24 ipv4.gateway 10.0.0.1
[con-name] connection name | [Ifname] interface name


nmcli con delete [Name]
Delete the configured settings for the particular connection-name specified
nmcli con up [Name] <----- NETWORK-ADAPTER-NAME
Once the settings have been configured properly, you can bring the network-up to utilize it,

nmcli con mod [Name] +ipv4.addresses 10.0.0.75/24
The option to associate another ip address 
- Remove
+ Add
nmcli con mod [Name] connection.autoconnect yes
Configure the auto-connect capabilities for the given con-name
nmcli con mod “current-name” connection.id “new-name”

ifup nicname 
Will bring the nic (network interface card) up and running
If the error below occurs, 
“ linux unknown error /etc/sysconfig/network-scripts/ “
This means that there is a conflict with the UUID.
ifdown nicname 
Will bring the nic (network interface card) down

uuidgen [NIC-Name]
Will generate a new uuid, which you can input into 
/etc/sysconfig/network-scripts/

NMCLI Config for Ubuntu 
apt install openssh-server
vi /etc/netplan/00-installer-config.yaml
--------------------------------------------------------------------------------
network:
  version: 2
  renderer: networkd
  ethernets:
    ens37:
      addresses:
      - 192.168.0.25/24
      gateway4: 192.168.0.1
      nameservers:
        addresses:
        - 8.8.8.8
        - 1.1.1.1
------------------------------------------------------------------------------------
sudo netplan try 
To try the configuration set above.
sudo netplan apply
To implement the changes, once netplan try is successful. 

systemd-resolved handles nameserver configuration.
Netplan configures systemd-resolved to generate a list of nameservers and domains to put in /etc/resolv.conf, which is a symlink.


/etc/resolv.conf -> ../run/systemd/resolve/stub-resolv.conf

Network-Manager Config for ubuntu 20.0.
 vi /etc/sysconfig/networking/devices/


ERROR: Ethernet device not managed
Soloution:
sudo mv /usr/lib/NetworkManager/conf.d/10-globally-managed-devices.conf /usr/lib/NetworkManager/conf.d/10-globally-managed-devices.conf_org

sudo touch /usr/lib/NetworkManager/conf.d/10-globally-managed-devices.conf

sudo systemctl restart NetworkManager






























Time-Date-Ctl Commands
timedatectl
Check the status of time
timedatectl list-timezones
List all the available time-zones
timedatectl set-timezone “Asia/Kolkata”
Set the time-zone to the preferred zone
timedatectl set-timezone UTC
Set the time-zone to the preferred zone
timedatectl set-timezone 15:50:30 | Hour/Minute/Secnd
Set the time-zone to the preferred time
timedatectl set-ntp true
To have the service enabled

chronyc source
To find the nearest-timezone to your location
dnf install chrony* -y
nano /etc/chrony.conf
server 192.168.50.99 iburst
systemctl restart chronyd.service
firewall-cmd --permanent --add-service=ntp 
chronyc clients
chronyc sources





Systemctl Commands
hostnamectl
Checks the hostname on the machine
systemctl status 
In-depth system status 

systemctl list-unit-files --type=service
List the status of all the services on the server
systemctl is-enabled [service-name] 
List a particular service to check whether it’s enabled or not
systemctl enable --now [service-name]
Enables and starts the service in the same command.
systemctl enable --now cockpit.socket 
Enables the web console
systemctl enable --now named
Enables the dns named configuration
Systemctl start mysqld.service

service --status-all
List all services up and running
sysctl --all
Shows kernel parameter 
sysctl -arn ‘icmp’
-a flag stands for all
-r flag stands for read regular expressions 
-n flag stands for number, will only print the number value
sysctl -w [net.ipv4.icmp_echo_ignore_all=0]
Command above sets the kernel parameter.
-w flag stands for write

YellowDog Updater
YUM-Essentials:
yum update
Update the repos
yum upgrade
Update the yum package manager
yum versionlock list 
Display all services that have version lock.
yum versionlock delete [service-name] 
Delete the version lock on the specified service.

YUM-Search:
yum list installed
Display all the packages that are available to to install
yum history 				
Display history of installs.		
yum history list ID_Number 		
Lists transactions (commands) recorded in yum history database.	
yum history info ID_Number 
Provides detailed information about a specific transaction recorded .
yum repolist  
Display all the repos on the machine.
yum deplist nodejs 
Display all the dependencies associated with nodejs package
yum search nodejs 
Display all the dependencies associated with nodejs package
yum info nodejs 
Display all the information related to nodejs package
yum repoquery -l nodejs
Display a query of information of nodejs package
YUM-Install:
yum install postfix
Mail Transfer Agent (MTA)  /etc/postfix/main.cf
yum install sshd 
secure shell service
yum install cronie
Used to configure automated tasks, also known as cron jobs

yum install httpd -y
Apache web server service
yum install rsyslog  
Used to monitor logs for the system
yum install figlet
figlet allows user to customize their console output

yum install nfs-utils nfs4-acl-tools autofs
Network file system, also installs auto file system mount
yum install cifs-utils
Installs Common Internet file system.
yum install dnf-utils
Contains dnf package manager 
yum install bind bind-utils -y
Installs utility to query DNS
yum install pci-utils
Installs various utilities tools for inspecting, and setting devices connected to the PCI bus

yum install mysql-server
Installs MySQL DataBase 
yum install gcc 
Installs GNU Compiler Collection
yum install gcc-c++
Installs C++ Compiler 

yum install sysstat
is responsible for the regular collection of system performance information. 


YUM-Cache:
yum clean packages
Purge the old package information completely
yum clean metadata
Clean all the cached files from any enabled repository at once
yum clean headers
Clean any cached xml metadata from any enabled repository
yum clean all
Clean all the cached files from any enabled repository 
yum makecache
Download and extract all of the repodata 
Configuration repo-file location: /etc/yum.repos.d










AdvancePackageTool:

APT-Essentials:
apt list --installed
view packages installed on system
apt list --upgradable 
view the packages that can be updated 
apt-get update
Gets the latest information about the packages.
apt-get upgrade
Implement the updates to the system.
apt dist-upgrade
Upgrades the distro

dpgk -i vscode

APT-Services:
apt install ssh 
Installs secure shell service
apt install realtek-rtl88xxau-dkms
Installs the realtek drivers for the alfa adapter  










SSH Commands: 
ssh-keygen -t rsa -b 4096
Will generate a public and a private key
.ssh permissions should be 700
Authorized_keys file permissions 600
-t for Type of authentication.
-b for Byte size.
ssh-copy-id  user@Server-IP
Will copy the ssh-key to the specified server

ssh -p 9876 faze@10.0.0.28
To login using ssh on a specific port.
ssh -i faze@10.0.0.28
To login using ssh with interactive.


ssh -V 
to check the version number 
ssh -v
Verbose
sudo mandb
use this if apropos ssh command says  "nothing appropriate" 
which $SHELL
Command To check what shell is being used








Firewall Commands:

firewall-cmd --list-all   
To list all the firewall.service configuration
firewall-cmd --zone=public --list-all

firewall-cmd --permanent --add-port=82/tcp
To permanently add a port to the firewalld.service
firewall-cmd --permanent --add-service={nfs,httpd,mountd}
To permanently add multiple services in one command
firewall-cmd --get-zone-of-interface=ens256

