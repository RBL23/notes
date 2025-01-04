# Linux notes

# **Week 1 (10 September)**

Introducing the class and the class ends by the success of downloading VMware or other virtual machine that can be use.


# **Week 3 (24 September)**

**Making client-server and copy files & directories**

Introducing about different AI models like gemini, openAi and also their billing system, how to use those openai in a doc format and showing the billing of it.

- **Setting up SSH server on a Linux machine.**
    
    An **SSH server** is like a **doorway** to your computer that lets you control it from far away, securely.
  
    ```bash
    sudo apt install openssh-server
    ```
    
- **Find and List Software Packages**
    
    dpkg -l part lists **all the software packages installed** on your Linux system that were installed using the Debian package manager (`dpkg`) and then **`grep`** is like a **search tool** that filters the output.**`grep ssh`** looks for lines containing the word **ssh** in the list of installed packages.

    ```bash
    dpkg -l | grep ssh
    ```
    
- Systemctl commands in Linux
    
    ### 1. **Check if the Service is Running:**
    
    ```bash
    systemctl is-active sshd
    ```
    
    - Returns whether the service is active (`active`) or not (`inactive`).
    
    ---
    
    ### 2. **Enable the Service at Boot:**
    
    ```bash
    sudo systemctl enable sshd
    ```
    
    - Configures the service to start automatically every time the system boots.
    
    ---
    
    ### 3. **Disable the Service at Boot:**
    
    ```bash
    sudo systemctl disable sshd
    ```
    
    - Prevents the service from starting automatically at boot.
    
    ---
    
    ### 4. **Start the Service:**
    
    ```bash
    sudo systemctl start sshd
    ```
    
    - Manually starts the SSH server if it’s not running.
    
    ---
    
    ### 5. **Stop the Service:**
    
    ```bash
    sudo systemctl stop sshd
    ```
    
    - Stops the SSH server if it’s running.
    
    ---
    
    ### 6. **Restart the Service:**
    
    ```bash
    sudo systemctl restart ssh
    ```
    
    - Stops and then starts the SSH server. Use this if you’ve made changes to the SSH configuration file (`/etc/ssh/sshd_config`).
    
    ---
    
    ### 7. **Reload the Service:**
    
    ```bash
    sudo systemctl reload sshd
    ```
    
    - Reloads the service configuration **without stopping** the service.
    - Use this after making changes to `sshd_config` to apply them.
    
    ---
    
    ### 8. **View Logs of the Service:**
    
    ```bash
    journalctl -u sshd
    ```
    
    - Shows the logs for the `sshd` service, which can help you troubleshoot issues.
    
    ---
    
    ### 9. **Check if the Service is Enabled at Boot:**
    
    ```bash
    systemctl is-enabled sshd
    ```
    
    - Tells you if the service is set to start at boot (`enabled` or `disabled`).
    
    ---
    
    ### 10. **View All Services:**
    
    ```bash
    systemctl list-units --type=service
    ```
    
    - Lists all active services running on your system.
    
    ---
    
    ### 11. **Mask the Service:**
    
    ```bash
    sudo systemctl mask sshd
    ```
    
    - Prevents the service from being started (even manually). It’s like "disabling" but more restrictive.
    
    ---
    
    ### 12. **Unmask the Service:**
    
    ```bash
    sudo systemctl unmask sshd
    ```
    
    - Reverses the effect of masking and allows the service to be started again.
        
    - Display Network connections
    
    <aside>
    
    netstat -tunlp | grep ssh
    
    </aside>
    
    ### **What is `netstat`?**
    
    - **`netstat`** (short for **network statistics**) is a command-line tool that shows network connections, routing tables, and listening ports.
    - It's useful for diagnosing network issues or checking which applications are using the network.
    
    ### **`-tunlp`:**
    
    1. **`t`:**
        - Displays **TCP** connections (Transmission Control Protocol).
        - TCP is used for things like web browsing and SSH connections.
    2. **`u`:**
        - Displays **UDP** connections (User Datagram Protocol).
        - UDP is used for things like DNS and streaming.
    3. **`n`:**
        - Displays addresses and port numbers **numerically** (e.g., IP addresses like `192.168.1.1` instead of hostnames like `example.com`).
    4. **`l`:**
        - Shows **listening ports**, i.e., ports that are waiting for incoming connections.
    5. **`p`:**
        - Shows the **process name and ID (PID)** of the program using each port.
                        
    - Still runs as normal but hide the output
      
        ```bash
        netstat -tunlp | grep ssh < /dev/null
        ```
        
    - Display the **exit status** of the last command that was run.
        
        <aside>
        
        **`echo $?`**
        
        </aside>
        
        - **`0`**: Success
            - The command ran successfully without any errors.
        - **Non-zero values (e.g., `1`, `2`, `127`)**: Failure
    - if you ever forgot pass
    
    <aside>
    
    mount -o remount,rw / passwd ricky
    
    </aside>
    
    in the terminal sudo passwd root
    
    - Ensure your user is in the group:
    
    ```bash
    usermod -aG sudo ricky2
    ```
    
    - SEE your IP
    
    ```bash
    ifconfig
    ```
    
    - edit sshd config
    
    sudo nano /etc/ssh/sshd_config
    

### Client Server

- normal login : Using ssh ricky@10.0.2.15 and then enter login pass
- w/out password login : ssh-keygen

- see the public and private key

if theres error in ssh-copy-id user@…. or in ssh user@.. use this…. ssh-keygen -f "/home/ricky/.ssh/known_hosts" -R "10.0.2.15"

- w/out password login to root

sudo nano /etc/ssh/sshd_config and then make PermitRootLogin yes

systemctl restart sshd

if you cant find the ip root name then just sudo nano /etc/hosts and then add 10.0.2.15    ubuntu2 and finally you can do ssh root@ubuntu2

- Copy file
    
    create file using touch and then copy it with these things below
    
if you delete the file using rm, and do this( dont forget the dot on the right!)

it will copy the file back to the server 

- copy directories

use scp -r 

delete and copy it back

### **1. `scp` Without a Dot (`.`)**

This copies **from your local machine to the remote server**.

### **2. `scp` With a Dot (`.`)**

This copies **from the remote server back to your local machine**.

# **Week 4 (1 October)**

## USB ##
- The `lsusb` command lists all USB devices connected to your system. This is helpful for identifying USB peripherals like keyboards, mice, flash drives, external hard drives, webcams, etc.
- The `lsblk` command lists information about block devices. Block devices include storage devices such as hard drives, SSDs, USB drives, and their partitions.
- The `umount` command in Linux is used to **unmount a mounted filesystem or storage device**.

### Mounting a USB ###

Steps:
- Use lsblk to identify the device name (e.g., /dev/sdb)
  ```bash
  lsblk
  ```
-Become a superuser using su -
```bash
su -
```
-Create a directory for the USB mount point:
```bash
mkdir -p /myusb
```
-Mount the USB drive to the directory:
```bash
mount /dev/sdb1 /myusb
```
-Verify the contents using:
```bash
ls /myusb
```
### Adding a New Hard Disk ###
You added a new virtual hard disk to a Linux virtual machine and made it usable.

1. Verify the new disk:
- After adding the disk, check the available disks with lsblk.
```bash
lsblk
```
Example:
If /dev/sdb (10GB) appears alongside the main disk /dev/sda (20GB), the new disk was successfully added.

2. Partitioning the new disk:
Use fdisk to create a partition on the new disk:
```bash
fdisk /dev/sdb
```
Steps in fdisk:
- Type n to create a new partition.
- Follow the prompts to define the size and type of the partition.
- Type w to write changes to the disk.

3. Formatting the partition:
- Format the new partition with the ext4 filesystem:
```bash
mkfs -t ext4 /dev/sdb1
```

4. Mounting the partition:

- Create a mount point:
```bash
mkdir -p /mydisk
```
- Mount the new partition:
```bash
mount /dev/sdb1 /mydisk
```
- Verify by navigating to /mydisk and creating a test file:
```bash
cd /mydisk
touch testfile
ls
```

5. Making the mount permanent:
- Find the UUID of the partition:
```bash
blkid
```
- Open the fstab file to configure automatic mounting:
```bash
sudo nano /etc/fstab
```
- Add an entry using the partition's UUID, like this:
```bash
UUID=0779fc59-8323-4206-a8b4-0ea85feba2bd /mydisk ext4 defaults 0 1
```
- Save the file and verify with:
```bash
df -h
```
This process ensures that the new disk is mounted automatically after a reboot and is ready for use.

# **Week 5 (8 October)) Symbolic Links and Hard Links** #
1. Create a File
```bash
touch source
```
- This creates an empty file named source.
2. Create a Symbolic Link
```bash
ln -s source source-slink
```
- Creates a symbolic link (source-slink) pointing to source.
- Symbolic links reference the file path, not the actual data.
3. Create a Hard Link
```bash
ln source source-hlink
```
- Creates a hard link (source-hlink) to source.
- Hard links reference the same inode as the original file.
4. Inspect the Inodes
```bash
ls -ali
```
Lists all files with their inodes:
- source and source-hlink share the same inode (e.g., 123456).
- source-slink has a different inode because it’s a symbolic link.
5. Modify the Content of source
```bash
echo "Hello, World!" > source
cat source
```
- Writes Hello, World! to the file source.
- Since source and source-hlink share the same inode, their content will now show Hello, World!.
- source-slink also displays this content because it points to source.
6. Delete the Original File
```bash
rm source
```
- Deletes the original file source.
Effects:
- Symbolic Link (source-slink): Becomes broken, as it points to a non-existent file.
- Hard Link (source-hlink): Still works, as it references the same inode.
7. Test the Links
Test the Symbolic Link:
```bash
cat source-slink
```
- This will fail because source-slink points to a deleted file.
Test the Hard Link:
```bash
cat source-hlink
```
- This will succeed, showing Hello, World!, as the data is still accessible via the hard link.
8. Attempt to Create Another Hard Link
```bash
ln source source-hlink
```
- This will fail, as the original file (source) no longer exists.

### Expected Output ###
1. Before Deleting source
```bash
ls -ali
123456 -rw-r--r-- 2 user user  13 Jan  4 10:00 source
123456 -rw-r--r-- 2 user user  13 Jan  4 10:00 source-hlink
123457 lrwxrwxrwx 1 user user   6 Jan  4 10:00 source-slink -> source
```
2. After Deleting source
```bash
ls -ali
123456 -rw-r--r-- 1 user user  13 Jan  4 10:00 source-hlink
123457 lrwxrwxrwx 1 user user   6 Jan  4 10:00 source-slink -> source
```
3. When Trying to Use cat
```bash
cat source-hlink
Hello, World!

cat source-slink
cat: source-slink: No such file or directory
```
4. When Trying to Create Another Hard Link
```bash
ln source source-hlink
ln: failed to create hard link 'source-hlink': No such file or directory
```

# **Week 6 (15 October))** 
## C Program Workflow
1. Create the C file and write the program
```bash
sudo nano test.c
```
Inside test.c
```c
#include <stdio.h>
int main() {
    printf("hello! \n");
    return 0;
}
```
2. Compile the program
```bash
gcc -o test test.c
```
- gcc is the GNU Compiler Collection.
- o test specifies the output file name as test.

3. Run the compiled program
```bash
./test
```
- Output: hello!

## Bash Script Workflow
1. Create the Bash script
```bash
sudo nano a.sh
```
Inside a.sh
```bash
#!/bin/bash
echo "hello world"
```
2. Run the script without execution permissions
```bash
bash a.sh
```
Output: hello world
3. Add execution permissions to the script
```bash
chmod +x a.sh
```
4. Run the script with execution permissions
```bash
./a.sh
```
- Output: hello world

## Python Script Workflow
1. Create the Python script
```bash
sudo nano test.py
```
Inside test.py
```python
#!/usr/bin/python3

print("hellowww")
```
2. Run the script using Python 3 directly
```bash
python3 test.py
```
- Output: hellowww
3. Make the script executable
```bash
chmod +x test.py
```
4. Run the script directly as an executable
```bash
./test.py
```
- Output: hellowww
Summary
C Program: Use a compiler like gcc to build and execute.
Bash Script: Can be run directly with bash or made executable with chmod +x.
Python Script: Run with python3 or directly after adding execution permissions.

# **Week 7 (22 Octorber) Ngrok**

## Making Local Server Public with Ngrok
1. Start Apache Server
```bash
sudo su
systemctl start apache2
```
Get the IP Address
```bash
ifconfig
```
- Use the IP address to verify the Apache server is running by visiting it in your browser.
3. Install Curl
```bash
sudo apt install curl
```
4. Set up Ngrok
- Go to Ngrok Dashboard and log in.
- Add the repository and its key
```bash
curl -sSL https://ngrok-agent.s3.amazonaws.com/ngrok.asc | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null
echo "deb https://ngrok-agent.s3.amazonaws.com buster main" | sudo tee /etc/apt/sources.list.d/ngrok.list
sudo apt update
```
- Install Ngrok
```bash
sudo apt install ngrok
```
- Add your authentication token
```bash
ngrok config add-authtoken <your_auth_token>
```
5. Expose Your Local Server
```bash
ngrok http http://localhost:80
```
- Use port 80 to ensure the default Apache port is exposed.
6. Verify the Public Page
- Navigate to the Ngrok-provided public URL.
7. Create a Simple HTML File
```bash
cd /var/www/html
echo "hello everybody" > kel.htm
```
- Access the page via the URL: <ngrok_public_url>/kel.htm.

## Password Authentication Using Apache
1. Install Apache Utilities:
```bash
sudo apt install apache2-utils
```
2. Create User Credentials
```bash
sudo htpasswd -c /etc/apache2/.htpasswd kel
sudo htpasswd /etc/apache2/.htpasswd lily
```
- Use -c only for the first user to create the file; for subsequent users, omit it.
3. Verify Users
```bash
ls -al /etc/apache2
cat /etc/apache2/.htpasswd
```
4. Create a Secure Directory
```bash
cd /var/www/html
mkdir sec
cd sec
echo "this is a private webpage" > index.htm
```
5. Update Apache Configuration
```bash
sudo nano /etc/apache2/sites-enabled/000-default.conf
```
Add the following before </VirtualHost>
```apache
<Directory "/var/www/html/sec">
    AuthType Basic
    AuthName "You need to login"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
```
6. Restart Apache
```bash
systemctl restart apache2
```
7. Access Secure Page
- Go to <ip_address>/sec and log in with the credentials (kel or lily).

## User and Password Management
1. Add a New User
```bash
useradd -m Bryan -s /bin/bash
```
2. Set Password for the User
```bash
passwd Bryan
```
3. Verify User Information
```bash
cat /etc/passwd
cat /etc/shadow
```

## Cracking Passwords with John the Ripper
1. Install John the Ripper
```bash
sudo apt install snapd
sudo snap install john-the-ripper
sudo apt install john
```
2. Prepare Wordlist
```bash
sudo nano wordlists
```
Add common passwords like qwerty.
3. Combine /etc/passwd and /etc/shadow
```bash
unshadow /etc/passwd /etc/shadow > mypasswd.txt
```
4. Run John the Ripper
```bash
john --wordlist=./wordlists --format="crypt" mypasswd.txt
```
- Output: Found password is qwerty.

## Group and User Management
1. Add a Group
```bash
groupadd rd
```
2. Assign User to Group
```bash
useradd -g rd Bryan
```
3. Verify User Group
```bash
id Bryan
```
4. Switch User
```bash
su Natalia
```

# **Week 8 (29 October) UserDir Module and Virtual Hosts Setup in Apache**

## UserDir Module
The UserDir module in Apache allows users to host web pages from their home directories. Here's how to set it up:
1. Enable the UserDir Module
```bash
sudo a2enmod userdir
```
2. Edit the UserDir Configuration
```bash
sudo nano /etc/apache2/mods-enabled/userdir.conf
```
Replace the existing configuration with
```apache
<IfModule mod_userdir.c>
    UserDir public_html
    UserDir disabled root
    <Directory /home/*/public_html>
        AllowOverride All
        Options MultiViews Indexes SymLinksIfOwnerMatch
        <Limit GET POST OPTIONS>
            Require all granted
        </Limit>
        <LimitExcept GET POST OPTIONS>
            Require all denied
        </LimitExcept>
    </Directory>
</IfModule>
```
3. Restart Apache
```bash
sudo systemctl restart apache2
```
4. Create Public HTML Directory for User
- Exit the root user
```bash
exit
```
- Navigate to your home directory and create the public_html folder
```bash
mkdir ~/public_html
echo "hi, this is user" > ~/public_html/index.html
```
5. Set Permissions
- Check permissions
```bash
ls -ald ~/public_html
```
- Update permissions to 755
```bash
chmod 755 ~/public_html
```
6. Access the Web Page
- Open the browser and navigate to: http://<server_ip>/~<username>/.

## User Creation with UserDir
1. Add a New User
```bash
sudo useradd -m Bryan -s /bin/bash
```
2. Switch to the New User
```bash
su - Bryan
```
3. Create a Public HTML Directory
```bash
mkdir ~/public_html
echo "hi, this is Natalia using userdir" > ~/public_html/index.html
```
4. Set Permissions
```bash
chmod 755 ~/public_html
```
5. Access the Web Page
- Navigate to: http://<server_ip>/~natalia/.

## Virtual Hosts in Apache
Apache Virtual Hosts allow you to host multiple websites on a single server.
1. Create Directories for Each Website
```bash
sudo mkdir /var/www/www-a-com
sudo mkdir /var/www/www-b-com
```
- Add an index.html for each site
```bash
echo "www.a.com" > /var/www/www-a-com/index.html
echo "www.b.com" > /var/www/www-b-com/index.html
```
2. Create Virtual Host Configurations
- For www-a-com
```bash
sudo nano /etc/apache2/sites-available/www-a-com.conf
```
Add
```apache
<VirtualHost *:80>
    ServerAdmin admin@www.a.com
    ServerName a.com
    ServerAlias www.a.com
    DocumentRoot /var/www/www-a-com
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
- For www-b-com
```bash
sudo nano /etc/apache2/sites-available/www-b-com.conf
```
Add
```apache
<VirtualHost *:80>
    ServerAdmin admin@www.b.com
    ServerName b.com
    ServerAlias www.b.com
    DocumentRoot /var/www/www-b-com
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
3. Enable the Virtual Hosts
```bash
sudo a2ensite www-a-com.conf
sudo a2ensite www-b-com.conf
sudo systemctl reload apache2
```
4. Update Local Hosts File:
- On your local machine (e.g., Windows), edit the hosts file
```plaintext
<server_ip> www.a.com
<server_ip> www.b.com
```
- Save and restart your browser.
5. Verify the Websites
- Open http://www.a.com and http://www.b.com in your browser to verify.

## Key Commands Summary
- UserDir Setup
```bash
sudo a2enmod userdir
sudo nano /etc/apache2/mods-enabled/userdir.conf
sudo systemctl restart apache2
mkdir ~/public_html
chmod 755 ~/public_html
```
Virtual Host Setup
```bash
sudo mkdir /var/www/www-a-com
echo "www.a.com" > /var/www/www-a-com/index.html
sudo nano /etc/apache2/sites-available/www-a-com.conf
sudo a2ensite www-a-com.conf
sudo systemctl reload apache2
```

# **Week 10 (12 November) Samba and NFS Configuration Guide**
## Samba: Sharing Files Between Linux and Windows
Samba enables seamless file sharing between Linux and Windows systems.

## Steps to Set Up Samba
### Step 1: Install Samba
Update the package manager and install Samba
```bash
sudo apt update
sudo apt install samba samba-common
```
### Step 2: Create Shared Directories
1. Create directories for shared access
```bash
sudo mkdir /sharea
sudo mkdir /shareb
```
2. Set permissions for full access
```bash
sudo chmod 777 /sharea
sudo chmod 777 /shareb
```
### Step 3: Create and Add Users
1. Add system users
```bash
sudo useradd -m usera
sudo useradd -m userb
```
2. Set passwords for the system users
```bash
sudo passwd usera
sudo passwd userb
```
3. Add the users to Samba and set their Samba passwords
```bash
sudo smbpasswd -a usera
sudo smbpasswd -a userb
```
### Step 4: Configure Samba
1. Open the Samba configuration file
```bash
sudo nano /etc/samba/smb.conf
```
2. Add the following configuration at the bottom of the file
```apache
[sharea]
path = /sharea
comment = Guest access folder
writable = yes
browseable = yes
guest ok = yes

[shareb]
path = /shareb
comment = Authenticated access folder
writable = yes
browseable = yes
valid users = usera, userb
write list = usera, userb
```
- sharea: Guest access (guest ok = yes) allows anonymous users.
- shareb: Requires authentication for usera and userb (valid users).
3. Save and exit
- Press Ctrl + O, then Enter to save.
- Press Ctrl + X to exit.
### Step 5: Restart Samba
Restart Samba to apply changes
```bash
sudo systemctl restart smbd
```
Check the status
```bash
sudo systemctl status smbd
```
### Step 6: Verify Sharing
1. Create a file in the sharea folder
```bash
echo "Hello from sharea!" > /sharea/a.txt
```
2. Verify file sharing
- Access from Windows: Use the \\<server_ip>\sharea in File Explorer.
- From Linux, use cat /sharea/a.txt.
## Using smbclient
Install smbclient
```bash
sudo apt install smbclient
```
List Available Shares
```bash
smbclient --list=<server_ip> --user=usera
```
Connect to a Share
```bash
smbclient --user=usera //<server_ip>/shareb
```
Within the Session
- List files
```bash
smb: \> ls
```
- Download a file
```bash
smb: \> get a.txt
```
- Exit the session
```bash
smb: \> exit
```
### Upload Files to the Share:
1. Create a file locally
```bash
echo "Hello, Samba!" > hi.txt
```
2. Upload the file to the share
```bash
smbclient --user=usera //<server_ip>/shareb
smb: \> put hi.txt
smb: \> ls
smb: \> exit
```
### NFS: Sharing Files Between Linux and Unix
NFS facilitates sharing files between Unix-like systems. Here's a quick setup guide
1. Install NFS Server
```bash
sudo apt update
sudo apt install nfs-kernel-server
```
Create Shared Directories
```bash
sudo mkdir /nfsshare
sudo chmod 777 /nfsshare
```
3. Configure Exports: Add the directory to the /etc/exports file
```plaintext
/nfsshare <client_ip>(rw,sync,no_subtree_check)
```
4. Restart NFS Server
```bash
sudo systemctl restart nfs-kernel-server
```
5. Access from a Client: On the client system, install nfs-common and mount the share
```bash
sudo apt install nfs-common
sudo mount <server_ip>:/nfsshare /mnt
```

# **Week 11 (19November) Networking Concepts and Tools**

## NGROK User Authentication
Objective: Set up NGROK with basic authentication
1. Start NGROK
```bash
ngrok http 80
```
2. Verify Apache2 Status
```bash
systemctl status apache2
ifconfig
```
3. Set Up Authentication
```bash
ngrok http 80 --basic-auth "username1:password1" --basic-auth "username2:password2"
```
4. Access NGROK Web Interface
- Open the NGROK URL in a browser.
- Enter username1 and password1 (or any specified credentials).
## Network and Routing
Setting Up LAN Segments in Virtual Machines
- Ubuntu1: Add two network adapters (LAN10 and LAN20).
- Ubuntu2: Change the single adapter to LAN10.
- Ubuntu3: Change the single adapter to LAN20.
## Static IP and Routing Configuration
Ubuntu2 Configuration
```bash
su -
ifconfig
ip addr add 192.168.10.1/24 dev ens33
ip addr show ens33
ip route add default via 192.168.10.254
ip route show
```
Ubuntu3 Configuration
```bash
su -
hostnamectl set-hostname ubuntuwork3
bash
ifconfig
ip addr add 192.168.20.1/24 dev ens33
ip route add default via 192.168.20.254
```
Ubuntu1 Configuration
1. Assign IP addresses to network interfaces
```bash
sudo su
ip addr add 192.168.10.254/24 dev ens35
ip addr add 192.168.20.254/24 dev ens36
ifconfig
```
2. Enable packet forwarding
```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
sudo nano /etc/sysctl.conf
```
- Uncomment or add net.ipv4.ip_forward=1.
- Save and reload
```bash
sudo sysctl -p /etc/sysctl.conf
```
## Configuring Static and Dynamic IPs with Netplan
Ubuntu1 Netplan Configuration
1. Edit the Netplan YAML file
```bash
sudo nano /etc/netplan/01-network-manager-all.yml
```
2. Add the following configuration
```yaml
network:
    renderer: NetworkManager
    ethernets:
        ens33:
            dhcp4: true
        ens37:
            addresses:
               - 192.168.10.254/24
        ens38:
            addresses:
               - 192.168.20.254/24
    version: 2
```
3. Apply the changes
```bash
netplan try
netplan apply
```
Ubuntu2 Netplan Configuration
```yaml
network:
    renderer: NetworkManager
    ethernets:
        ens33:
            addresses:
               - 192.168.10.1/24
            routes:
               - to: default
                 via: 192.168.10.254
    version: 2
```
Commands
```bash
netplan try
netplan apply
ping 192.168.10.254
ping 192.168.20.1
ping 192.168.20.254
```
Ubuntu3 Netplan Configuration
```yaml
network:
    renderer: NetworkManager
    ethernets:
        ens33:
            addresses:
               - 192.168.20.1/24
            routes:
               - to: default
                 via: 192.168.20.254
    version: 2
```
Commands
```bash
netplan try
netplan apply
ping 192.168.20.254
ping 192.168.10.1
ping 192.168.10.254
```
## Wireshark
Wireshark is a network protocol analyzer to monitor and inspect network traffic.
1. Install Wireshark
```bash
sudo apt install wireshark
```
2. Start Wireshark
```bash
wireshark
```
3. Usage
- Select the network interface to monitor.
- Analyze incoming/outgoing packets in real-time.

Summary of Commands
- NGROK:
```bash
ngrok http 80 --basic-auth "username:password"
```
- Static Routing
```bash
ip addr add <IP>/<Subnet> dev <Interface>
ip route add default via <Gateway>
```
Netplan
```bash
sudo nano /etc/netplan/<file>.yaml
netplan try
netplan apply
```
- Wireshark
```bash
sudo apt install wireshark
wireshark
```

# **Week 12(26 November)DHCP and NAT Configuration**
## DHCP Configuration
Setting Up DHCP in Ubuntu1
1. Install ISC DHCP Server
```bash
sudo apt install isc-dhcp-server -y
```
2. Backup Configuration File
```bash
sudo cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.backup
```
3. Edit DHCP Configuration File
```bash
sudo nano /etc/dhcp/dhcpd.conf
```
Add these configurations
```plaintext
subnet 192.168.10.0 netmask 255.255.255.0 {
  range 192.168.10.100 192.168.10.200;
  option subnet-mask 255.255.255.0;
  option routers 192.168.10.254;
  option broadcast-address 192.168.10.255;
  default-lease-time 600;
  max-lease-time 7200;
}

subnet 192.168.20.0 netmask 255.255.255.0 {
  range 192.168.20.100 192.168.20.200;
  option subnet-mask 255.255.255.0;
  option routers 192.168.20.254;
  option broadcast-address 192.168.20.255;
  default-lease-time 600;
  max-lease-time 7200;
}

subnet 10.0.0.0 netmask 255.255.255.0 {
  range 10.0.0.100 10.0.0.200;
  option subnet-mask 255.255.255.0;
  option routers 10.0.0.1;
  option broadcast-address 10.0.0.255;
  default-lease-time 600;
  max-lease-time 7200;
}
```
Restart DHCP Service
```bash
sudo systemctl restart isc-dhcp-server
sudo systemctl status isc-dhcp-server
```
## Testing DHCP on Ubuntu2 and Ubuntu3
1. Check Network Configuration
- Go to Settings > Network.
- Set IPv4 to Automatic (DHCP).
- Turn off and turn on the connection.
2. Validate IP Assignment
```bash
ifconfig
```
You should see IPs assigned from the DHCP ranges (e.g., 192.168.10.100 or 192.168.20.200).
3. Update Netplan (if needed)
- Edit /etc/netplan/50-cloud-init.yaml
```yaml
network:
    version: 2
    renderer: NetworkManager
    ethernets:
        ens33:
            dhcp4: true
```
- Apply the configuration
```bash
netplan try
netplan apply
```
4. Ping Tests
- On Ubuntu3
```bash
ping 192.168.10.100
```
## NAT Configuration
Setting NAT in Ubuntu1
1. Change IPv4 Address of Ethernet Interface (ens36)
- Go to Settings > Network.
- Set the IPv4 address to 10.0.0.1.
- Turn off and turn on the connection.
2. Verify New IP
```bash
ifconfig
```
3. Configure NAT Using iptables
```bash
iptables -t nat -A POSTROUTING -s 192.168.10.0/24 -o ens36 -j MASQUERADE
```
4. Check iptables Rules
```bash
iptables -t nat -L
```
## Wireshark Usage
1. Install Wireshark
```bash
sudo apt install wireshark-*
```
2. Run Wireshark (if issues occur)
```bash
sudo wireshark
```
3. Monitor Traffic
- Select the interface for Ubuntu2 or Ubuntu3 (e.g., ens36).
- Observe the traffic while performing actions like ping.
4. Ping Test from Ubuntu2
```bash
ping 10.0.0.100
```
- Verify traffic movement in Wireshark.
## Troubleshooting
- If DHCP does not assign IPs
1. Restart the DHCP server
```bash
sudo systemctl restart isc-dhcp-server
```
2. Restart the network on Ubuntu2 or Ubuntu3
- Disable and re-enable the connection.
- Run
```bash
ifconfig
```
- If Wireshark doesn't launch properly
```bash
sudo apt remove --purge wireshark
sudo apt install wireshark
```
Summary of Key Commands
DHCP
```bash
sudo apt install isc-dhcp-server -y
sudo nano /etc/dhcp/dhcpd.conf
sudo systemctl restart isc-dhcp-server
```
NAT
```bash
iptables -t nat -A POSTROUTING -s <source_subnet> -o <interface> -j MASQUERADE
iptables -t nat -L
```
Wireshark
```bash
sudo apt install wireshark-*
sudo wireshark
```
