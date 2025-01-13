<p align="center">
</p>

<h1>Cisco Packet Tracer |  Hotel Topology<h1>
  
This project focuses on designing a functional and efficient network for a three-story hotel using Cisco Packet Tracer. The network will support both business operations and guest services while ensuring scalability, security, and ease of management. Each floor has distinct departments that need tailored connectivity and configurations based on their specific needs.

<h2>Environments and Technologies Used</h2>

- Cisco Packet Tracer

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Objectives</h2>

- Connectivity: All devices communicate across VLANs and floors.
- Secure Access: SSH enables secure remote login.
- Dynamic IP Allocation: DHCP assigns IPs dynamically.
- Port Security: Unauthorized devices cannot access the IT network
- Scalable Design: VLANs and OSPF allow future expansion.

<h2>Network Design Implementation</h2>

<p>

</p>
<p>
<h2>1. Network Topology</h2>
  
To ensure inter-floor connectivity, three routers were deployed, with one router assigned to each floor. The routers were interconnected using serial DCE cables with the following IP subnets:

Router Connections and Subnets:

Router1 ↔ Router2: 10.10.10.0/30

Router2 ↔ Router3: 10.10.10.4/30

Router1 ↔ Router3: 10.10.10.8/30

Configuration:

-Router1 Configuration:

Interfaces:

Serial0/0 (to Router2): 10.10.10.1/30

interface Serial0/0

ip address 10.10.10.1 255.255.255.252

clock rate 64000

no shutdown

Serial0/1 (to Router3): 10.10.10.9/30

interface Serial0/1

ip address 10.10.10.9 255.255.255.252

clock rate 64000

no shutdown


-Router2: Configuration

Interfaces:

Serial0/0 (to Router1): 10.10.10.2/30

interface Serial0/0

ip address 10.10.10.2 255.255.255.252

no shutdown

Serial0/1 (to Router3): 10.10.10.5/30

interface Serial0/1

ip address 10.10.10.5 255.255.255.252

clock rate 64000

no shutdown

-Router 3 Configuration:

Interfaces:

Serial0/0 (to Router2): 10.10.10.6/30

interface Serial0/0

ip address 10.10.10.6 255.255.255.252

no shutdown

Serial0/1 (to Router1): 10.10.10.10/30

interface Serial0/1

ip address 10.10.10.10 255.255.255.252

no shutdown


Switches:
Each floor was equipped with a dedicated switch connected to the respective router to facilitate wired connections and departmental VLAN segregation.

Wireless Access Points:

To provide wireless connectivity for laptops and mobile phones, one wireless access point was installed on each floor. These access points were configured to serve the specific VLANs assigned to the departments on their respective floors.

Printers:
Each department was allocated a printer connected to its designated VLAN. The printers were configured to be accessible only by devices within the same VLAN.

<h2>Topology</h2>

![image](https://github.com/user-attachments/assets/a6f36ea7-798a-4875-baf4-5e4efe8bc04b)

<h2>Floor 1 IP addresses</h2>

![image](https://github.com/user-attachments/assets/7b954a86-3ee3-4abe-b15e-cabc8716bf3a)

<h2>Floor 2 IP addresses</h2>

![image](https://github.com/user-attachments/assets/fe8fafad-f6fe-4a5b-b17d-d3dad53800b9)

<h2>Floor 3 IP addresses</h2>

![image](https://github.com/user-attachments/assets/713a354f-b6c7-402a-89c4-b9d243c58091)




</p>
<br />

<p>
</p>
<p>
<h2>2. VLAN Configuration</h2>
  
Unique VLANs were assigned to each department to ensure logical separation and enhance security. The VLANs were configured as follows:
  
Third Floor:

VLAN 10: IT

interface range FastEthernet0/1-10

switchport mode access

switchport access vlan 10

VLAN 20: Admin

interface range FastEthernet0/11-20

switchport mode access

switchport access vlan 20


Second Floor:

VLAN 30: Sales

interface range FastEthernet0/21-30

switchport mode access

switchport access vlan 30
  
Second Floor:

VLAN 40: HR

interface range FastEthernet0/31-40

switchport mode access

switchport access vlan 40

VLAN 50: Finance

interface range FastEthernet0/41-50

switchport mode access

switchport access vlan 50

First Floor:

VLAN 60: Logistics

interface range FastEthernet0/51-60

switchport mode access

switchport access vlan 60

VLAN 70: Store

interface range FastEthernet0/61-70

switchport mode access

switchport access vlan 70

VLAN 80: Reception

interface range FastEthernet0/71-80

switchport mode access

switchport access vlan 80

Each VLAN was mapped to specific switch ports to segregate traffic and ensure efficient communication within the respective departments.

<h2>Floor 1 VLANS<h2>

![image](https://github.com/user-attachments/assets/bdd7118f-38b7-4f04-a500-bb76674acc3d)

<h2>Floor 2 VLANS<h2>
  
![image](https://github.com/user-attachments/assets/14c54b06-f6f2-49ce-85e1-5bec5c1f923b)

<h2>Floor 3 VLANS<h2>

![image](https://github.com/user-attachments/assets/eea53c10-01bf-4a98-a5a7-8d93485ecb34)



</p>
<br />

<p>

</p>
<p>
<h2>3. Routing Protocol</h2>
To enable communication between routers and ensure efficient route advertisement, OSPF (Open Shortest Path First) was configured. The following configurations were implemented:
Each router was assigned to OSPF process 1.
Subnets associated with each router’s interfaces were advertised using the network command.

Router 1 Configuration:

router ospf 1

network 10.10.10.0 0.0.0.3 area 0  # Router1 to Router2 link

network 10.10.10.8 0.0.0.3 area 0  # Router1 to Router3 link

Router 2 Configuration:

router ospf 1

network 10.10.10.0 0.0.0.3 area 0  # Router2 to Router1 link

network 10.10.10.4 0.0.0.3 area 0  # Router2 to Router3 link

Router 3 Configuration:

router ospf 1

network 10.10.10.4 0.0.0.3 area 0  # Router3 to Router2 link

network 10.10.10.8 0.0.0.3 area 0  # Router3 to Router1 link


</p>
<br />
</p>
<br />

<p>

</p>
<p>
<h2>4. DHCP Configuration</h2>

Dynamic Host Configuration Protocol (DHCP) was configured on each router to provide automatic IP address assignment for devices connected to their respective VLANs. 

Key steps included:

Defining separate DHCP pools for each VLAN. Assigning the appropriate gateway IP for each VLAN within the DHCP configuration. Ensuring the DHCP configuration matched the VLAN’s IP range to prevent conflicts.

Router 1:

ip dhcp pool Reception

 network 192.168.8.0 255.255.255.0
 
 default-router 192.168.8.1
 
 dns-server 192.168.8.1
 
ip dhcp pool Store

 network 192.168.7.0 255.255.255.0
 
 default-router 192.168.7.1
 
 dns-server 192.168.7.1
 
ip dhcp pool Logistics

 network 192.168.6.0 255.255.255.0
 
 default-router 192.168.6.1
 
 dns-server 192.168.6.1

Router 2:
 
ip dhcp pool Finance

 network 192.168.5.0 255.255.255.0
 
 default-router 192.168.5.1
 
 dns-server 192.168.5.1
 
ip dhcp pool HR

 network 192.168.4.0 255.255.255.0
 
 default-router 192.168.4.1
 
 dns-server 192.168.4.1
 
ip dhcp pool Sales

 network 192.168.3.0 255.255.255.0
 
 default-router 192.168.3.1
 
 dns-server 192.168.3.1

Router 3:
 
ip dhcp pool Admin

 network 192.168.2.0 255.255.255.0
 
 default-router 192.168.2.1
 
 dns-server 192.168.2.1
 
ip dhcp pool IT

 network 192.168.1.0 255.255.255.0
 
 default-router 192.168.1.1
 
 dns-server 192.168.1.1

</p>
<br /></p>
<br />

<p>

</p>
<p>
<h2>5. SSH Configuration</h2>
SSH was enabled on all routers to facilitate secure remote management. The configuration included:
Setting up a username and password for authentication.
Generating RSA keys to support encrypted communication.
Enabling SSH access while disabling Telnet for security purposes.

Router 1:

hostname Router1

ip domain-name example.com

username admin password admin

crypto key generate rsa

ip ssh version 2

line vty 0 4

transport input ssh

login local

do wr
 
Router 2:

hostname Router2

ip domain-name example.com

username admin password admin

crypto key generate rsa

ip ssh version 2

line vty 0 4

transport input ssh

login local

do wr

Router 3:

hostname Router3

ip domain-name example.com

username admin password admin

crypto key generate rsa

ip ssh version 2

line vty 0 4

transport input ssh

login local

do wr

</p>
<br /></p>
<br /></p>
<br />

<p>

</p>
<p>
<h2>Conclusion</h2>
The network was successfully designed and implemented in Cisco Packet Tracer to meet the hotel’s operational requirements. All configurations were verified, ensuring:
Seamless inter-department and inter-floor communication.
Robust security mechanisms through VLAN segmentation, SSH, and port security.
Dynamic IP allocation for all devices using DHCP.
This network design is scalable and can be adapted for future expansions while maintaining its efficiency and security standards.

</p>
<br />
