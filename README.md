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
- Create 4 VM's For setting up these VM's watch Video-2 In Links & references section FOr VM's configurations watch Lab-3 Video.
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
It will enable splunk servr to start everytime VM reboots or turns on! you will see init script is configured to run at startup .
### Step -17 Setup Windows Target Machine
Change hostname to Target-PC
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/ee6fbfd4-0634-497d-a7b6-1a62c182003f)

Restart Machine.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/738f1801-cce3-44fd-b726-d19aad672de7)
Check IP run : ipconfig from CMD 
Assign static IP 192.168.10.100 with defauly gateway 192.168.10.1 DNS 8.8.8.8
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/0d9486a0-4ad1-4ddc-bc8c-c53fa2518ff2)

### Step-17
Access Splunk server started at 192.168.10.10:8000
### Step-18 Install Universal Forwarder
Go to splunk.com login with your account 
Go to Products > Free Trials & Downloads > Universal Forwarder
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/cdf8caa8-5cf0-438d-bb79-f27f56a70546)

<b>Downlaod relevant OS file after downloading double click file from downlaods folder.</b>
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/c9207574-1f7e-4e71-8fa2-d155e456b440)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/12bc1277-9d58-42b2-b9b4-6e56b9f401ba)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/adc93a6f-293d-4707-b685-da8d207abb6c)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/f5112769-e495-48cc-9abe-6f67e127dc11)

### Install SYSMON
Search Google sysmon 

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/5a08af61-d8fb-4b6f-b64f-15e68c813cfa)

<b>Use sysmon olaf config search o Google sysmon olaf config</b>
https://raw.githubusercontent.com/olafhartong/sysmon-modular/master/sysmonconfig.xml


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/3609ba7f-543e-4ea4-bfd9-c35316b04d1f)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/f18701a1-f829-4127-b129-4fffec232309)

<b>Open powershell as Amdin after copying path of sysmon downloaded folder</b>

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/df69935f-2298-4577-9e22-09f782ca9d7c)


Run command ./sysmon64.exe -i sysmonconfig.xml ( if you sysmon.conf fil ein other folder then give that path I copied mine to same sysmon folder)
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/63c0bc06-644e-4eca-9785-434c3a42a921)

If all goes smooth see this .
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/2584353b-d60f-4074-abc9-4b35a25657b7)

### Step 18 Configure Splunk Forwarder
<b>It will instruct what needs to be forwarded to our Splunk server</b>
Need to configure file inputs.conf
Path to file : C:\Program Files\SplunkUniversalForwarder\etc\system\default
<b>Note : we need to copy inputs.conf file from default folder and then paste into \system\local folder do not modify master inouts.conf file in default folder.</b>
Modify inputs.conf file and paste contents from <a href="https://github.com/MyDFIR/Active-Directory-Project">inputs.conf file</a> to your /system/local inputs.conf file ( you can only modilfy it when select open notepad right click then select open as admin admin privileges then go to location of file open and paste then save"

Restart Splunk Universal Forwarder Go to services run ad admin find splunk forwarder right click then restart.
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/34712f4b-fbfc-4afa-9a96-541fb20c27c9)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/af0def4f-b3b5-4b99-ad8a-519c89717f82)

<b> IF see NETSRV account we need to change it to local system account </b>
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/9d3b5b5c-6996-4db5-a571-45b59b04fc82)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/5bf207ce-400e-4ac1-a15d-7276ae312d3d)

### Setting Up & Final Touches to Splunk Server 
Login to Splunk sever with you credentials
<b>Since our inputs.conf file contains index=endpoint we need to create same index at splunk to collect logs </b>
Go to Setting > Indexes
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/43dd3341-df00-4d29-8ec2-62b3c7a73723)

Enter Name : endpoint Click SAVE
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/974abb2e-62e3-4976-89e9-be7b0c6ab1d2)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/507ac6de-d47c-4e33-b87b-1398917a5c96)

<b>Enable Splunk Server To recive data :</b>
Settings > Forwarding and receiving
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/a9fb610b-be38-4980-a91a-26eed96f676d)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/2d9683dd-6b2f-4486-b80b-ca96e8716f11)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/72f3622b-69e4-4a8b-a278-34a8a3f091c0)

To check if we are getting Data from endpoint to splunk server.
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/c866b10e-d883-4c50-921e-66a9f9afe05f)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/aa845af8-f63d-44f5-9f78-b14c02edb002)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/5ea47fee-4b45-45d5-974c-0703fe3290d8)

Addiitionally use/install splunk sysmon APP for getting more enriched data/fields. Find more Apps
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/9c517924-98f9-4e2c-9308-d60be41d816b)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/5dc61c85-445a-45f5-b9e9-ec00df947433)










