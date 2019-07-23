# LFCS
Preparation for Linux Foundation Certified System Administrator

- [Module 1: Essential Commands](#module-1-essential-commands)
- [Lesson 1: Installing Linux](#lesson-1-installing-linux)
- [Lesson 2: Learning Objectives](#lesson-2-learning-objectives)
- [Lesson 3: Using Essential File Management Tools](#lesson-3-using-essential-file-management-tools)

## Module 1: Essential Commands

### Lesson 1: Installing Linux
We will use several distributions:
* CentOs
* Ubuntu
* SUSE - OpenSUSE

### Lesson 2: Learning objectives

###### Common linux commands 

* ``` logout ``` or ``` exit ``` - to log off from your current session. 
* ``` whoami ``` - name of logged in user
* ``` hostname ``` - full hostname
* ``` date ``` - current date and time
* ``` uname ``` - information about system
* ``` passwd ``` - change your password 
* ``` touch ``` - creating an empty file 
* ``` last ``` - shows logged users to the system

- Working with ``` man ``` command. 
By using ``` man ``` we will work with following sections:
1. User commands (1)
4. Devices (4)
5. Configuration files (5)
8. Sysadmin commands (8)

Examples:
- ``` man 8 useradd ``` - show information about command from section 8 
- ``` man -a passwd ``` - show information about command from all sections
- ``` man -k ``` - using manual with keyword, when you don't know which command to use 
- ``` appropos user ``` - same results as for ``` man -k ``` command 
- ``` man -k | grep 8 ``` - search for section 8
- ``` sudo mandb ``` - create or update the manual page index caches
- ``` su - ``` - switch for root user

###### Common bash features

- stdin or '<' redirect standard input
- stdout - your console, or redirect output to a file use '>' or '>>' to append
- stderr or 2> - for redirect error
- piping
    * ``` ls | less ``` input of ``` ls ``` filtered by ``` less ```
    * ``` ps aux | grep httpd ```
- ``` find /proc -name "cpu*" 2> /dev/null ``` - find cpu in /proc directory and send error output to the null device
- ``` history ``` - command line history, to use command from history simple write commands number from history ``` !28 ```
    * history stored in *.bash_history*, you can find this file by typing ``` ls -a ``` - where *-a* means to show hidden files. 

###### Using bash shell scripts
* ``` echo who > myscript ``` - create and add line to the file
* ``` echo ls >> myscript ``` - append to the file
* ``` chmod +x myscript ``` - make your script executable
* ``` ./myscript ``` - run your script 

###### Lab answers 
* ``` uname -r ``` - get kernel version
* ``` hostnamectl set-hostname ``` - change hostname 
* ``` nmtui-hostname ``` - change hostname from gui on CentOS
* ``` lvcreate --help ``` - all options in [] brackets are optional, all options in {} brackets are mandatory, must be used 

### Lesson 3: Using Essential File Management Tools
###### 3.1 Understanding the Linux File System Hierarchy

Hierarchy:
* / - root directory
    * /boot - files need to start your computer's OS
    * /home - loc of user home directories
    * /usr - operating system files 
    * /var - diverse information (log, cache)

* mount - connection between directory and device
    * ``` /dev/sdb1 ``` - 
        * /dev is device directory, 
        * sd - scsi disk
        * b - second scsi disk 
        * 1 - number of partition.

By using command ``` mount ``` we can mount different disks to the different directories.
Directories in linux defined by *FHS* - Filesystem Hierarchy Standards 

![img](https://github.com/Bes0n/LFCS/blob/master/images/img1.JPG)

###### 3.2 Listing files with ls command
- ``` ls -l ``` - long list of items
- ``` ls -a ``` - shows hidden items
- ``` ls -lrt ``` - list items by last time modified
- ``` ls -l /etc ``` - get content of /etc directory
- ``` ls -R ``` - list entire directory structure (recursive)
- ``` ls -ld /etc ``` - get information of /etc directory directly

###### 3.3 Using Shell Wildcards
Three types of globbing:
- '*' - ``` ls a* ``` - will list all files starting with 'a' character. With any length
- ? - ``` ls ca? ``` - will list files which have 'ca' in the beginning and with last character, for instance 'cat' or 'car'
- [a-b] - ``` ls ca[bt] ``` or ``` ls ca[b-t] ``` - first will list with 'ca' and 'b' or 't', second will list 'ca' and starting from 'b' to 't'
Example: ``` ls [a-d]??* ``` - list word starting with 'a' to 'd', have '??' at least two characters and '*' any amount of characters in the end

###### 3.4 Copying files with cp
- ``` cp /etc/hosts . ``` - copy hosts files in home directory
- ``` cp -R /tmp . ``` - copy entire subdirectoy structure in home directory
- ``` cp /etc/hosts ~/data/ ``` - copy hosts file in home/data directory. Don't forget to put slash behind the directory

###### 3.5 Working with Directories
- ``` cd /tmp ``` - change directory
- ``` pwd ``` - print working directory
- ``` mkdir data ``` - create subdirectory data
- ``` mkdir -p files/pete ``` - create directory files with pete directory entire using '-p' - path option
- ``` rmdir videos/ ``` - remove empty directory
- ``` rm -rf ``` - remove directory forcely. Even if directory has a files in it. 

###### 3.6 Using Absolute and Relative Paths
Absolute path can be:
- ``` /tmp/data/files/pete ```
Relative path can be:
- ``` /files/photos/2017 ``` - no need to change directory from 'tmp' 
- ``` cd .. ``` - go to previous directory
- ``` cd ../.. ``` - go to two levels up on directory

We can copy items by using relative path: 
![img](https://github.com/Bes0n/LFCS/blob/master/images/img2.JPG)

- ``` tree /tmp/data ``` - get structure of the directory
- ``` cp hosts /tmp/data/photos/2016/ ``` - copy hosts to '2016' directory using **absolute** path
- ``` cp hosts ../../photos/2017/newfiles ``` - copy hosts to '2017' directory using **relative** path