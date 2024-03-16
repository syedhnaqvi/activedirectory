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
- Create 4 VM's
- Windows 10 Machine , Kali Linux machine , Ubuntu 20.04 LTS for Splunk deployment , Active Directory
- Setup & Configuee VM's based on network diagram based on your system vailable resources (RAM)

  ## Links & References
- <a href="https://youtu.be/mWqYyl89QaY">Lab-1 Video</a>
- <a href="https://youtu.be/2cEj3bS5C0Q">Lab-2 Vidoe</a>
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

