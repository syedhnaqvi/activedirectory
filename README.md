# Active Directory Lab

## Objective
The purpose of utilizing the active directiry funcitinaly and attack vectors for detectiona & analysis .

### Skills Learned

- Active direcotry installtion.
- Setting up Windows & Linux VM's.
- Setting up Splunk Server .
- Create detection & log analysis.


### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis Wazuh
- Kali Linux for attcking windows based victom machine 
- WIndows & Lunux VM's.
- Darw.io for digramatic flow 

## Steps
- Create 4 VM's For setting up these VM's watch Video-2 In Links & references section
- Windows 10 Machine , Kali Linux machine , Ubuntu 20.04 LTS for Splunk deployment , Active Directory
- Setup & Configuee VM's based on network diagram based on your system vailable resources (RAM)

  ## Links & References
- <a href="https://youtu.be/mWqYyl89QaY">Lab-1 Video</a>
- <a href="https://youtu.be/2cEj3bS5C0Q">Lab-2 Video</a>
- <a href="https://youtu.be/uXRxoPKX65Q">Lab-3 Video</a>


Ref 1: Network Diagram*
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/c5a76b8b-fff4-434a-9b2b-ae921e35ec37)

<b> Setting Up VM's </b
Configuring NAT settings Go to tools > Hamburger options > Network 
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/b10c7ef6-7b71-4a52-97de-24b19789ae84)

<b> Select Tab NAT network > Create </b> We selct CIDR range as per diagram 192.168.10.0/24 <b> Then Apply Enable DHCP remain clicked </b>

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/5b9a274b-045e-4a9e-bdf1-eb9946d3a327)

<p><b> Assign created NAT to all VM Resources </b> <span style="color:red;">Make Sure to Assign Created NAT to All VM's</span></b></p>
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/1ec1d94a-4bfe-441c-b6fb-4f02448981a0)

Login to Splunk VM Linux Ubuntu 20.04 LTS machine Run command : ip a wil show you Ip adr as 912.168.10.4/24 as per our diagram we need to install IP 192.168.10.10.
So we need to run command by setting up installer.config.yaml file
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/6a34d28b-4675-409a-bdfe-cef0f4915da1)
Configure File :
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/a2235cfa-76f5-48aa-83d0-5e64f41b558c)
-After DHCP- NO line hit enter to add new line and hit tab 3 times 
-After addresses line hit Enter then hot Tab 3 times again
-After nameservers line hit Enter for new line and then hit TAB 5 times to add DNS 8.8.8.8 (Google DNS)
- After that nameserver line hit tab 3 times
- After routes line hot TAB 5 times
- Enter new line press Enter then hit TAB 6 times
- CTRL+X then then Y Press Enter key
If see warnings rewlaetd to vswitch use this link to resolve issue it worked for me ! https://stackoverflow.com/questions/77352932/ovsdb-server-service-from-no-where
Run ip a command if see IP: 192.168.10.10/24 then it means netplan worked and configurations all setup .
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/71f34f0a-2e0d-4e3c-a777-3bdb2eedd311)
Last check ping www.google.com if you see reply it means all working else revisit your netplan config file formatting and indentation then apply netplan fiel again until you see ping response from google.com
<b>After this step completed then we are ready to Install SPLUNK on our machine .</b>
## Splunk Installtion 
After you sign up on splunk.com then click on 
### Step -1 
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/92c8f20d-f025-40df-b2ab-89e9499e8f60)
### Step -2
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/d49bb14b-89e6-4992-8ed3-7b0b5ef00dde)
### Step -3
Select Linux and Deb file as we are using Debian based Ubunt Distro for linux Downlaod and Save
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/bca032fe-5c80-489e-a0e4-0d7869868688)

### Step -4
Add on Virtual guest Add on to our VM
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/57ac0bc5-437d-49dd-ad28-f7cc42a660a0)

### Step -5 
Add shared folder to access Splunk download file 
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/bd6df385-0ae2-4d60-a902-edced90233e1)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/b501f2b0-d6d4-4b29-8501-dc935bf9296a)

### Step -6
Run comand sudo reboot to reboot VM
### Step-7
Add user to vboxsf command : sudo adduser <Your username for splunk VM> vboxsf
If see error group vboxsf not exit then we need to install additional guest utility
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/5b939fda-0543-413f-8c44-cf6599611877)

### Step-8 
sudo reboot

### Step -9
Run Add user to vboxsf command : sudo adduser <Your username for splunk VM> vboxsf
This time user will be added to group - Done 
### Step-10
Create shared directory command  mkdir share
### Step-11
Mount the share directory/folder [Change your created folder name !]
Command: ![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/245f3b71-0900-446c-8897-bf0bb55d1294)
If successful must see :
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/ccab40f5-afe5-488b-b64c-58e18bc6b400)

If see any error then try exit command reboot then try again !
### Step -11
cd to share and must see Splunk downloaded file
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/10454428-578e-4832-80fb-48f3ef0ba28c)

### Step -12 
Install splunk command : ![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/9dc2428b-39eb-406f-bb32-fafd5c1dac54)
Once see Complete means all good now !

### Step -13
CD to /opt/splunk 
la -ls
see all users are splunk 
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/79efb311-d3ba-4df9-8b2f-48e0cac2f09f)

run command :![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/8da8dc18-5886-465a-88c6-1730fc77fe72)
### Step-14
CD to /bin all binaries files will be displayed here ls-la

### Step -15
Run splunk installer using command : ![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/63843088-151c-4a87-9909-fe6a906ac262) <br>
IF see error like folder not found then reboot splunk VM
again run command : sudo -u splunk bash then run command : cd bin then ./splunk start read and accept and then select y choose admin name and password 
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/84e96856-8ce8-4b54-8bbc-b90f28635992)

### Step-16
Use command exit to exit splunk user 
Then cd bin
run command : ![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/e147bfb9-31fd-402e-b06b-b560b1838eb2) <br>
It will enable splunk servr to start everytime VM reboots or turns on!
