


# RHCSA_Full_Content (RHEL9)

**Find all files that are larger than 5MB in the /etc directory and copy them to /tmp/5mfile**

```BASH
 find /etc -size +5M -exec cd {} /tmp/5mfile/\;
```


-----------------------------------------------------------------
# SCP SYNTAX : 

**scp -r username@ip:path [windows path]**

```SHELL
scp -r root@192.168.0.100:/etc/ansible/Playbooks/shellscript.yaml D:\AnsiblePlaybooks
```


**Linux:**
```SHELL
scp -rp text.txt root@@vmc1015:/tmp
```

------------------------------------------------------------------------------
# User & Group Creation:

**We can create users & group with 2 methods. one is there are some files where we can go and edit it or using commands we can create it**

**Below are file path of users group & password

```SHELL
vi etc/passwd       # Stores user account information, including usernames and user IDs
vi /etc/group       # Contains group account information, such as group names and group IDs
vi /etc/shadow      # Stores encrypted password information and account expiry details for user accounts.
vi /etc/login.defs  # Defines default login configuration settings for user accounts.
vi /etc/gshadow     # Securely stores group password information (rarely used in modern systems).
vi /etc/login.defs  # 1. Repeated entry; defines default login configuration settings for user accounts.
```

# Creating users group passwords using Commands:

## User Creation:

```SHELL
useradd cena  # will create a user cena
passwd cena  # This will create a pasword for the new user cena 
```
## Group Creation:

```SHELL
groupadd devgroup #This will create a new group in your system
```
## User Modification:

```SHELL
usermod -G devgroup cena  # -G is secondary group now cena is part of secondary group devgroup.

usermod -s /sbin/nologin cena #Here cena don't hvae access to the shell so he can't login to his account.

sudo usermod -c "This is test user" test_user # To add comment to user

sudo usermod -d /home/manav test_user # To change the home directory of a user

sudo usermod -e 2020-05-29 test_user # To change the expiry date of a user

sudo usermod -l test_account test_user # To change user login name

sudo usermod -L test_user # To lock a user

sudo usermod -U test_user #To unlock a user

sudo usermod -s /bin/sh test_user # To create a shell user.

sudo usermod -u 1234 test_user # To change the user id of a user
```

## Removing Users Groups and Passwords:

``` SHELL
sudo userdel username    # Remove the User 
sudo userdel -r username # Remove the User & its folder which will present in /usr
sudo groupdel groupname  # Remove the Group
sudo passwd -d username  # Remove the Password
passwd -uf root #root unlock
passwd -l root # for lock root
```

---
# Zipping and Unzip in RHEL:

## **Create a Tar Archive**:
**tar = to combine multiple files in OneFile**            
**gzip = to compress the file size we use gzip**
**c = create , v =verbose , f= forcefully , x= extract**
**tar -cvf  testtar (outputname) file1 (file which you need to compress)

```SHELL
sudo tar -cvf archive.tar directory_or_file #Which you are going to zip it

```
## **Extract a Tar Archive**:

```SHELL
sudo tar -xvf archive.tar
```

## **Compress (gzip) a Tar Archive**:

```SHELL
sudo tar -czvf archive.tar.gz directory_or_file
```

## Extract a Compressed Tar Archive (gzip):

```shell
sudo tar -xzvf archive.tar.gz
```
## **Compress (bzip2) a Tar Archive**:

```shell
sudo tar -cjvf archive.tar.bz2 directory_or_file
```

**Extract a Compressed Tar Archive (bzip2)**:

```shell
sudo tar -xjvf archive.tar.bz2
```

---

# Linux Permissions:

**chmod = used to change the access mode of a file**
**chown = change the owner of file** 
**chgrp = change the group**

**If we do ls -l we can able see like below. Here D is teh beginning then it is a dirctory**
> d| rwx | r_x | r-- -| 1 root root 6 junly01 04:10 chiru 

**If you see like below " -" the you can confirm that as a file
> - | rwx | r_x | r-- -| 1 root root 6 junly01 04:10 chiru 

| Permission  | Owner User/Group  | Description            | File Size (Bytes) |
|-------------|--------------------|------------------------|-------------------|
| rwx         | root               | Owner or root user     | 6                 |
| r_x         | root               | Group                  |                   |
| r--         | Other user         | Others (created user)  |                   |
| 1           |                    | Symbolic link          |                   |

| Permission  | Numeric Value | Description     |
|-------------|---------------|-----------------|
| r           | 4             | Read (display)  |
| w           | 2             | Write (modify)  |
| x           | 1             | Execute (run)   |

**This table summarizes the meanings of the permissions 'r', 'w', and 'x' along with their corresponding numeric values, which are commonly used in Unix and Linux systems to define file permissions.** 

---

# How to take SSH without Password:

**Assume that you have 2 servers naming Ser1, Ser2. So if you want take access of serv2 from ser1 we need to use ssh.**

**While taking SSH everytime it will ask's are password how to avoid it ?

```SHELL
#In Ser1:
 sudo ssh-keygen     # Step:1 Create a Cert file deafault give enter enter cert will be created

sudo ssh-copy-id root@Ser2  # Step:2 Here we are transferring the cert file to Ser2 so that from next time it will not ask's password 

```

**In Few cases HOST VERIFICATION FIALED error will be appread then use below command. 

```SHELL
sudo ssh-keygen -R servername
```

---- 
# Port scanning:

**Here we can use 2 options one is using netcat command and the other is Nmap command.

## NetCat:

```SHELL
nc -zv 192.168.1.200 22

```

## Nmap:

```SHELL
sudo nmap vmc6001 -p 10443
```

# To Check all open ports in your system:

### Netstat:

```SHELL
sudo netstat -tuln
```

### Nmap:

```SHELL
nmap -p- 192.168.1.100
```

---
# **View Running Processes (List):**

```SHELL
sudo ps aux
```

### **Find a Specific Process by Name:**

```shell
sudo pgrep nginx
```

### **Kill a Process by PID:**

```shell
sudo kill 1234
sudo kill -9 1234 # use `kill -9` to forcefully kill a process if it doesn't respond to a regular
sudo kill myprocess # Kill Processes by Name
```

---

# Firewall Configurations:

```SHELL
firewall-cmd --list-all # to see list of all ports & services 
firewall-cmd --add-port=400/tcp --permanent # To add port in firewall
firewall-cmd --reload # reload
firewall-cmd --get-services # To check all services
firewall-cmd --add-service=http --permanent # To add service in firewall
firewall-cmd --remove-port=400/tcp --permanent # To remove a port
firewall-cmd --remove-service=http --permanent # To remove a service
```

**Note: If you are adding anything or removing anything try to reload it or else added configuration will not be applied.**

----

# ACCESS CONTROL LISTS (ACL)

**Example:**

```SHELL
ls
rw-r--r-- student student demo 
```

**I have demo file and i need chiru user to write on demo assuming chiru is not part of student group. here chiru is not owner and also (group chiru) is other and for others we have only read permission.**
**one way is we can change permission for other like below:**

```SHELL
rw-r--rw- student student demo
```

**But here the problem is chiru can write but also the other users in server also can edit the file**
**So now how we can do it ? we can do it using ACL. We have two command getfacl, setfaclACL Permissions**

```shell
sudo getacl demo # get acl info
sudo setfacl demo  # apply new acl
```

### How we can get info whether ACL is applied on the file or not?

```SHELL
ll
-rw-r--r--+ 1 root root 10 mar 5 10:13 data1  
```

**Here from the above command we can able to see "+" from here we can confirm that ACL is applied on that data1 file. if you see "+" blindly we can see ACL is applied on that file.

## How to apply ACL on a file for user:

```shell
sudo setfacl -m "u:chiru:rw-" data1   # here -m is modify
```

## How to apply ACL on a file for group:

```SHELL
setfacl -m "g:manager:rw-" data 
```

## How to apply ACL on a file for others:

```SHELL
setfacl -m "o:rw-" data 
```

## Removing ACL:

```SHELL
sudo setfacl -b data1  # b =back to normal 

# To remove a particular ACL then use below command -x
setfacl -x "g:manager" data1
setfacl -x "u:chiru" data1
```














PARTITIONS COMMANDS:


#lsblk 
#fdisk -l
#fdisk /dev/sdb
i have mounted 3 GB i need 1Gb FOR 1 PARTITON AND 2 GB FOR ANOTHER PARTITION.IN LAST SECTOR WE CAN GIVE LIKE +1GB.

#partprobe /dev/sdb  ------we need to do reboot but instead of reboot we can use this command
#fdisk -l
#lsblk
#mkfs.xfs  /dev/sdb1
#mkfs.ext4  /dev/sdb2
#lsblk
#df -h
TO CHANGE LABLE NAME INSEAD OF UUID: need to done before mount if mouned we can add lable 
xfs_admin -L testlable /dev/sdb1

MOuting HDD TO MOVIES &SOFTWARES
#mkdir /movies /software
#mount /dev/sdb1 /movies
#mount /dev/sdb2 /software/
#mount
#lsblk
#df -h
NOW ITS HAS MOUNTED BUT AFTER RESTART IT WILL BE GONE SO TO KEEP THIS WE NEED TO ADD OUR UUID IN ETC/FSTAB
#Vi /etc/fstab 
#blkid
------------------------------------------------------------------------------
FIREWALL PORTOPENING:

TO SEE LIST OF PORTS:
firewall-cmd --list-all
To add port:
firewall-cmd --add-port=400/tcp --permanent
firewall-cmd --reload
TO check service:
firewall-cmd --get-services
To add service:
firewall-cmd --add-service=http --permanent

To remove all:
firewall-cmd --remove-port=400/tcp --permanent
firewall-cmd --remove-service=http --permanent
firewall-cmd --reload
------------------------------------------------------------------------------
SELINUX:
cat /etc/selinux/config  = configuration file 
getenforce = to change the mode to enforcing
setenforce 0 = it is in permissive means selinux will run but shows warning
setenforce 1 = it means enforcing  means it will block all the new thing 

we have changed the ssh port 400 and we reload sshd service it will not load 
due to we have not informed to selinux to inform we need to run the command.

TO RUN SEMANAGE YOU NEED TO INSTALL A PACKAGE yum provides /usr/sbin/semanage
semanage port -l | grep ssh (here u will get a name like prot_ssh_l) we need to add that thing.

semanage port -a -t port_ssh_l -p tcp 400

to check it is added or not:
semanage port -l | grep ssh

even now also it ssh will not work due to firewall add 400 port in firewall too.
-----------------------------------------------------------------------------
CHANGE THE RULES FOR A FOLDER 

WE ARE HOSTING A WEBSITE DEFAULT LOCATION IS /VAR/WWW/HTML/INDEX.HTML

BUT I NEED A SEPARATE FOLDER TO HOST IT SO TO DO IT.

CREATE A DIR IN / (mkdir /mysite)
now create a index.html inside of mysite 

now type ll -Z we can see default for mysite dir beacuse selinux don't know 

now ll -Z /var/www/ we can able to for html folde will add some httpd copy that

now we need to modify our mysite dir
semanage fcontext -a -t httpd_ "/mysite(/.*)?"
restorecon -rv /mysite
even now also we will get error due to we need to allow permission for other also 
chmod 777 mysite
chmod 777 index.html
now we can able to see you website to load from our dir but not from /var/www/html.
---------------------------------------------------------------------
dmidecode  | less
----------------------------------------------------------------------
NFS SERVER:
MKDIR /DATA
CP /USR/BIN/* /DATA
dnf install -y nfs-utils
vi /etc/exports
/data *(rw,no_root_squash)
:wq!
systemctl start nfs-server
firewall-cmd --add-service=nfs --permanent
firewall-cmd --add-service=rpc-bind --permanent
firewall-cmd --add-service =mountd --permanent
firewall-cmd --reload
firewall-cmd --list-all
NFS CLIENT:
yum install -y nfs-utils

showmount -e ip of the server

mount 192.168.10.100:/data /mnt


--------------------------------------------------------------------------
 AUTONFS:
 dnf install nfs-utils
 systemctl enable --now nfs-server
mkdir /data
cp /usr/bin/* /data
inside data create dir 
mkdir u1 u2 u3 u4 u44 u50
cp a* u1
cp b* u2
cp c* u3
cp d* u4
cp e* u44
cp f* u50

vi /etc/exports

/data *(rw,no_root_squash)
systemctl restart nfs-server.service
firewall-cmd --add-service=nfs --permanent
firewall-cmd --add-service=rpc-bind --permanent
firewall-cmd --add-service =mountd --permanent
firewall-cmd --reload
firewall-cmd --list-all
clien side:
dnf install dnf-utils
showmount -e server ip 
mount serverip:/data /mnt
df -h
umount /mnt

mount server ip:/data/u36 /mnt we dont know in nfs u36 is there or not here
we use automount.

dnf install autofs -y
systemctl enable --now autofs
vi /etc/auto.master.d/xxxx("dir" we are using).autofs
/mnt /etc/auto.dir  :wq!
vi /etc/auto.dir
xyz -rw,sync,fstype=nfs4 serverip:/data
systemctl restart autofs

cd /mnt/xyz (we can able go into xyz dir )
df -h

wildcard autofs
open the same file again
vi /etc/auto.dir
* -rw,sync,fstype=nfs4 serverip:/data/&
-------------------------------------------------------------------------
--------------------------------------------------------------------------
SPECIAL PERMISSIONS:

IT GIVEN NEW FUNCTINALITY FOR EXAMPLE

when we run passwd command via chiru user
/etc/shadow(password storing file) -> it will be modified
can chiru user edit the shadow file?
 login as root l s-l /etc/shadow
 ---------. 1 root root 1580 feb 25 10:50 /etc/shadow
how can edhit only root user can edit anyone because ther is no permission applied.
 login to chiru try to change th password we can change how we can change using special permissions
in chiru ls -l we can see
-rwsr-xr-x 1 root root 1580 feb 25 10:50 /etc/shadow
here we can able to see "s" kind of special permissions s= get userid

her for this file we have set user id in root so we will acting as root for this particular file we can also check usingg 

login to chiru type passwd chiru it will ask for type new password take new tabe and type ps -ef | grep passwd we can able to see root

2) sticky :

ls -ld /tmp 
drwxrwxrwt. 20 root root 4096 mar 5 10:29 /tmp  we can see t= sticky
if we are able to understand the permisson we can also use stat /tmp
 we can see tmp has all permission anyone can use anyone can edit anyone can remove the file but to avoid we can use sticky only the owner of file can remove edit the files.

user1 has created  the mail in tmp and user2 can remove or edit the file due to 777 but the moment we add sticky user2 can do anything for user1 created files. this is the feature of sticky bit

3) G+S( SET GROUP ID )

assume we have dir in /project 3 dev are creating mobile app. when they are creating app mutiple files are created so all the dev need to have access edit remove  for all the files like u2 can modify the files of u1 &u3 and viceversa
 in this case special permission are applied on project directory that is called set group ip 
 
 3dec ->devs group u1 u2 u3 belons to group devs
 mkdir /project
 rw-rw-r-- root devs /project
  now u1 login in went to cd /project creats a file touch prog.js
  ls -l prog.js
  rw-rw-r-- u1 u1 prog.js 
  now u2 also logs in an create a file by the name data.css
  ls -l data.css
  rw-rw-r-- u2 u2 data.css
  
  now can user1 can modify data.css file ? 
rw-rw-r-- u1 u1 prog.js
rw-rw-r-- u2 u2 data.css
we will stay frpm permissions 

u2 we have rw for owner ok rw for group  r for other u1 will falls under others

answer is no u1 can't able to modify how it can be possible ??

it is possible when group is belongs to dev group
rw-rw-r-- u1 devs prog.js
rw-rw-r-- u2 devs data.css
which need to be applied automatically. if we user special permission to project whenever any user creats the file group will be taken as devs.
--------------------------------------------------------------------------
DAY 2: SPECIAL PERMISSIONS:
 LS -L /USR/BIN/PASSWD
 
-rwsr-xr-x. 1 root root 346 au10 2021 /usr/bin/passwd  s = suid
if colour is hightlite in red means it has having suid
if it is apply on dir there will be n effects
see the table in pdf you will get the 
APPLY SPECIAL PERMISSIONS:

2 WAYS
SYMBOLIC
 SUID = U+S - chmod u+s filename
 SGID = G+S - chmod g+s filename
 STICKY = O+T - chmod o+t filename
NUMERIC:
suid = 4 - chmod 4775 filename (exu file)
sgid =2 - chmod 2755 dir name   
sticky =1 - chmod 1755 dirname

stat /tmp

SUID - SET USER ID
create a command and apply suid
SGID - SET GROUP ID
5 user part of staff group need to work on comman exam paper
STICKY -
create a public writeable dir and protect with sticky

cd /usr/bin

vi welcome  #!/bin/bash echo "hellow file"
ls -l welcome
-rw-r--r--. 1 root root 31 mar aa welcome
we need to run this welcome file 
chmod 4775 welcome
ls -l welcome
-rwsrwxr-x.1 root root 31 mar welcome3
to understand more we will edit the weclome file
#!/bin/bash
read name
echo "hello $name"
wq!
now run the welcome it wil wait for user info nwo in another console use
ps -ef | grep i welcome here we can able to see it is running as root 
now login to student user and run the weclome command come to anothe console and try to check ps -ef | grep -i welcome even here we can also able to see the root but we are trying as student user.

SGID - SET GROUP ID
5 user part of staff group need to work on comman exam paper
need to do :/exam root:staff -rwxrwxr-x 
mkdir /exam
ls -ld /exam
drwxr-xr-x. 2 root root 5 mar /exam
chmod 775 /exam
groupadd staff
chown student:staff /exam   dont make root as owner it will trows error
ls -ld /exam

now we need to add members to staff group (adding chiru cena)
vi /etc/group 
staff: chiru,cena
wq!
id chiru id cena 
now try to login as chiru & cena try to create a file inside of /exam
 chiru login : touch chiru_file1
 cena login : touch cena_file1
 
ls -l
-rw-rw-r--. chiru chiru 0 mar chiru_file1
-rw-rw-r--. cena cena 0 mar cena_file1

now here chiru user can work on cena_file1 no because chiru is other of cena_file1.

manually way:
chiru login : chgrp staff chiru_file1
cena login : chgrp staff cena_file1   ls -l
 what if we have more that 1000 files so we will be using user group id 
chmod g+s  /exam  (remember exam has group staff )
stat /exam
now if we create a file group will be default staff 
 touch rock_file3
 ls -l
 studen staff mar 11 rock_file3
 
 sticky:
 mkdir /test 
 chmod 777 /etst
 ls -d  (anyone can come edit remov ethe files)
chmod 0+t /test
ls -ld 
we can see "t" nwo who will create files in test they can only remove but not all.
------------------------------------------------------------------------------
UMAKS
WE CAN ABLE TO SEE WHEN WE CREATE ANY FILE OR DIR IT WILL HAS PERMISSION AUTOMATICALLY DUE TO UMAKS EXAMPLE

touch demo 
ls -ld demo
we will see -rw-r--r--.1 root root 10:55 demo 
also now login as differnt user and create a file and check permisson it may be different.

To check what is umask on root user also check for student user also
umask command it will show 0022

root 0022
normal file(not exe file):666
dir:777
non root:0002

so now we need to sunstract the file + root like below

022      777
666      022
---      ---
644      755   --> this is umask which will applied by default when we create a file or dir 

we will be having only 1 admin user which is root remaining are all non root user even if we add them to wghell group 
Now same applied for noroot user also
002      777
666      002
---      ---
664      775  -> umask for non root users

Umask can set in 2 ways 1 is globally 2 is per user based

procedure to setup default umaks:
vi /etc/profile
vi /etc/bashrc
vi~/.bash_profile
vi~/.bashrc
grep -rn umask /etc
-----------------------------------------------------------------------------
DNF:
DNF INSTALL FIREFOX 
NOW IT WILL READ ONE XXX.REPO FILE >> WIIL HAVE URL>> PACKAGES DOWNLOAD.

TO USE URL WE NEED TO PAID TO RED HAT FO UPDATES 

subscription-manager register ---username DCr@gmail.com --auto-attach
password : email password

dnf clean all
dnf repolist
we can see base os and app stream

 -------------------------------------------------------------------------
 CRON JOB:
 
 EVERYDAT AT 9AM RUN DF -H > /RMP/DATA.TXT
 
 cat /etc/crobtab
 1.min
 2.hours
 3.day of te month)1-31)
 4.month (1-12)
 5.day of the week (sun, man.tue...)
 1 2 3 4 5 user-name command tobe executed
 
 0 12  * * 1-5
 
 crontab -e  
 0 9  * * * df -h > /tmp/data.txt
 
 25 15 * * * /bin/echo hiyya
 
 2. 21:30 15th of everymonth need to update DB.
 
 30 21 15 * * updatedb
crontab -l = to list the jobs
crontab -e -u chiru == it will configured for user chiru
crontab -l -u chiru
crontab -r -u chiru = r is used to remove all entries

-------------------------------------------------------------------
GUI LOGIN LOGOUT
For stopping the currently running GUI session:

# init 3

To get back into the GUI mode temporarily, type the following in the terminal.

# init 5

------------------------------------------------------------------------------                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
Container file:
FROM ubi9
RUN dnf install -y httpd
ENTRYPOINT ["httpd","-D","FOREGROUND"]
----------------------------------------------------------------------------------------
NOTE: WHEN WE ARE RUNNING A CONTAINER LOGIN A NONROOT USER ITSELF DONT USE SU CHIRU THIS IS THE PROBLEM IN CONTAINERS

 

 

which podman

 

dnf install container-tools

 

 

podman pull httpd  ==> use docker.io

 

podman ps ==> to check container running
podman search httpd ==>search for container

 

podman ps  -a ==> it you stop any container and it will store in ram using -a we can see all the stopped containers

 

podman rmi [image id ]  ==> to remove images

 

podman images ==> show container where it got downloaded

 

podman run -d httpd ==> it will start container  -d is run in backend dont show login terminal

 

now if we run with ip in google i will get can't able to reach the site beacuse we need to do some port mapping to access the httpd

 

podman ps
podman stop [name of the container]
podman ps  -a

 

podman rm [name of the container]

 

podman run -d --name web1  -p 8080:80 httpd  =>8080 server port will redirect to the port 80 of the httpd container

 

if its not working add 8080 in firewall

 

podman exec -it web1 /bin/bash ==> we enter into shell
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
day-2

 

now we have website and we need to run in container

 

i have website.zip

 

mkdir /data

 

cp website.zip  /data

 

cd  /data
ls
we can see zip file of website

 

change the owner ship and permissions:

 

chmod 776 /data

 

chown -R student:student /data   here -R  is recorversve means in /data if we create it will have ownership of student

 

uzip website.zip

 

rm -rf website.zip

 

cd startbotsstrps

 

here we will see all the website files .html,.css...

 

now move all the files to /data

 

mv *  /data

 

rm -rf  startbotsstrps

 

 

podman run -d --name web1 -p 8080:80  -v /usr/local/apache2/htdocs :Z   [here z is used for selinux how to understand? now follow below steps before running this command run]

 

ls -ldZ /data

 

as per selinux we have dafaults_t    which means only user can enter but not application so we will use Z in last now run the command

 

podman run -d --name web1 -p 8080:80  -v /usr/local/apache2/htdocs :Z  httpd

 

podman ps

 

ls -ldZ /data
now we can see container_file_t

 

open chrom and use ip:8080 it will run we can see our website.
-----------------------------------------------------------------------------------------------------------------------
RUNNING CONTAINER AS A SERVICE:

 

to run the container as a service we need to go to home directory and we need to run the command as below

 

[student@june~] mkdir -p  .config/systemd/user
ls -ld .config

 

cd .config/

 

ls

 

cd  systemd/

 

ls

 

cd user/
ls

 

her in this path we need to run the below command

 

podman generate systemd --name web1 --files   ==> now her in user dir a service file has ben genereated
ls

 

now to user systemctl enable or disable or start or stop we will use a feature  which is called linger

 

sudo loginctl enabled-linger student

 

systemctl --user daemon-reload  ==> it will reload our files

 

 

systemctl --user status container-web1.service

 

we can see it is not loaded  lets do we will stop container and we will start as a service

 

podman ps

 

podman stop web1

 

systemctl --user start container-web1.service

 

systemctl --user status container-web1.service

 

systemctl --user enable  container-web1.service

 

 

now no need to run podman start we can use systemctl

 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

BUILDING A CONTAINER FILE:

 

 

LETS CREAT HTTPD CONTAINER FILE
vi Dockerfile
FROM ubi9
RUN dnf install -y httpd
ENTERYPOINT ["httpd"," -D", "FOREGROUND"]

 

podman built -t httpd:amit /home/student/  or buildah build -f Dockerfile -t watch

 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

que:

 

make in root
wget https:// container file

 

buildah build -f Dockerfile -t watch

 

cd /opt ; mkdir in out

 

 

chmod 777 in; chmod 777 out

 

chown neith:neith in,chown neith:neith out
sudo loginctl enabled-linger neith

 

now login as neit user

 

podman run -d --name ascii2pdf -v /opt/in:/opt/incoming:Z -v /opt/out:/opt/outgoing:Z /localhost/watch

 

podman ps

 

 

now we need to run as service

 

mkdir -p  .config/systemd/user; cd ~/.config.systemd/user

 

podman generate systemd --name ascii2pdf  --files
systemctl --user daemon-reload

 

systemctl --user status container-ascii2pdf.service
systemctl --user enable  container-ascii2pdf.service --now

 

 

 

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

test:

 

root@rhel2 server

 

wget container file

 

buildah build -f Dockerfile -t watch

 

sudo loginctl enabled-linger neit

 

 

cd /opt; mkdir in out

 

chmod 777 in ; chmod 777 out

 

chown neith:neith in ; chown neith:neith out

 

 

now login as neith user

 

 

podman run  -d --name ascii2pdf -v /opt/in:/opt/incoming:Z  -v /opt/out:/opt/outgoing:Z  /localhost/watch

 

 

mkdir -p .config/systemd/user;cd ~/.config/systemd/user

 

podman generate --name  ascii2pdf --files**

 
 


















































































