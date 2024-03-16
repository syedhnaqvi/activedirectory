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


