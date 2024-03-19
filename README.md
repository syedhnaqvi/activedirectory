# Active Directory Lab

## Objective
The purpose of utilizing the active directiry funcitinaly and attack vectors for detectiona & analysis .

### Skills Learned

- Active directory installtion.
- Setting up Windows & Linux VM's.
- Setting up Splunk Server .
- Create detection & log analysis.


### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis Wazuh
- Kali Linux for attacking windows based victim machine 
- WIndows & Linux VM's. ( Target Win machine and Linux 22.05 LTS Ubuntu server) Win 2022 server trial 
- Darw.io for digramatic flow 

## Steps
- Create 4 VM's For setting up these VM's watch Video-2 In Links & references section FOr VM's configurations watch Lab-3 Video.
- Windows 10 Machine , Kali Linux machine , Ubuntu 20.04 LTS for Splunk deployment , Active Directory
- Setup & Configuee VM's based on network diagram based on your system vailable resources (RAM)

  ## Links & References
- <a href="https://youtu.be/mWqYyl89QaY">Lab-1 Video</a>
- <a href="https://youtu.be/2cEj3bS5C0Q">Lab-2 Video</a>
- <a href="https://youtu.be/uXRxoPKX65Q">Lab-3 Video</a>
- <a href="https://www.youtube.com/watch?v=1XeDht_B-bA">Lab-4 Video</a>


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

### Step 19 Configure Splunk Forwarder
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


### Setting up & Configure Linux Universal Forwarder 
Follow this detailed video for installing universal forwarder for linux and forwarding logs to splunk server
<a href="https://youtu.be/smyLZ6ataK0">Installing & Setting Up Linux Universal Splunk Forwarder</a><br>
<a href="https://community.splunk.com/t5/Getting-Data-In/How-to-setup-universal-forwarder-on-linux/m-p/97458">Other helpful article</a>


### Ingesting Windows Firewall Logs to Splunk
Make these chnages to inputs.conf file :
[WinEventLog://Microsoft-Windows-Windows Firewall With Advanced Security/Firewall]

index = firewall

disabled = false

sourcetype = [WinEventLog://Security]
<b> Make sure to restart Splunk Universal Forwarder Service</b>

### Step -20 Configure AD Server 
Assign Static IP to AD server 
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/f7c68aa0-f7fd-445d-a556-0a2357118632)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/d76ed3f4-286b-4c36-8a19-52b24e3879cf)

Select IPV4 settings then add these settings .
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/f8b5de88-bea7-491c-b544-75415a7bbdd9)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/38d2891d-19a9-4108-9eb0-4957ac8fec81)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/a2ea0636-6960-4bdd-a32e-99e603fa59c6)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/b726a252-9177-4046-96f6-e3b147ef66eb)

Click NEXT

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/e2362d8e-4549-4f0e-b3aa-d2acfa65287e)

Click NEXT

Click & Select Active Directory Domain Service a.k.a ADDS
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/8903e2da-2755-4966-b45e-56b70a4e4df0)

Click Add Feature.
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/0a25f801-ce37-4817-938f-7c0f1a2d8e95)

Keep Clikcing Next Unitil see this Screen and click Install.
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/1567c578-a35b-4d3a-b461-1c8d1a2bfaa2)

Will take sometine to install .
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/76d096b9-2be8-437e-93d0-2a06ba62f25c)

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/badbf7a1-f636-4100-9e71-b02b5425f520)

Click Close.
![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/d5aa41e0-5a46-4652-b0a8-7e210d534cdb)

Check Notification.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/6a9295b2-001b-478f-8c69-c227d07d8ade)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/e27ed7e0-93a6-4e0f-a031-20fe5422ce30)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/c09987e7-7a9d-4d07-b200-5746714c1e0e)

Put Password and all defaults and Click NEXT.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/ea81895b-2a9a-4b9b-ac67-31b62edfb512)

Keep Clicking NEXT.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/0cb3242e-5538-4a63-8e8b-e450d97532a5)

Click INSTALL.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/129d459b-5d68-42c9-a6ed-e0f47c50d6e7)

Once all completed server will automatically restart.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/4eb35c9c-6530-4181-9c10-2024a903e9ec)

After server reboots will see domain screen .

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/075051c6-34ca-4271-b625-54e68716978b)

Login and Add users.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/d090701e-62fd-4771-b148-3625e1ed44f6)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/e700025b-f4bd-4797-83f5-d83547a648f6)

Expand domain & click Builtin will show you builtin groups created automatically 

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/c6dc8ea2-b311-4633-9c7e-11c58fb5e5f3)

Users option will show users .

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/d995c2f3-a542-4135-841e-4041191087ce)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/c809fd45-d394-4f48-9513-39315c6aeb42)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/f5371099-e6ca-4f11-a4db-873d8db44526)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/0bfdd842-2ded-48d8-a3ba-7853d38de90b)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/a35635f7-537f-4922-836f-5f67f034ee8a)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/2fca809d-f216-4c4d-acfa-a950a20a0b7b)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/82523152-5905-4e6e-85f4-16e0fd2246f8)

Click Finish.

### Step -21 From Cleint Win10 Machine join domain 
Search PC then click on Properties.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/0912cdbb-6693-4f63-bb43-7a407d4e332c)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/e5b7a86c-8d04-4aa9-8daa-c3d29df1e6ae)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/8318ed30-d314-4eb3-b9f6-851b965da798)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/c6ddaaff-7ebd-4c70-9e86-0e0ed9412086)

Chnage domain DNS server . Change it to our Domain server address 192.168.10.7

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/b68ec598-1fb1-4fd0-9a48-9112a8bf7a96)

To validate settings.

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/70f54ae1-4b5c-41e4-b4f5-b9ca18597add)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/3f1ba95a-b9f3-4e7c-ae39-7b4827c67344)


![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/751c76ba-8ba9-49ed-aa02-50fccf55e251)

After Clint machine logs back user jsmith user we created .

![image](https://github.com/syedhnaqvi/activedirectory/assets/39069507/559b19de-71a5-43ee-854d-8ed2ef00756b)

### Adding users in bulk with Powershell script .
<a href="https://blog.netwrix.com/2018/06/07/how-to-create-new-active-directory-users-with-powershell/">Create bulk Users</a>




