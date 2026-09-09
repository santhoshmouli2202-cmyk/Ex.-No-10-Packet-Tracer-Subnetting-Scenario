# Ex. No: 10 – Packet Tracer: Subnetting Scenario
# Date: 09/09/2026
________________________________________<br>
# Objective
Design, configure, and verify an IPv4 subnetting scheme in Cisco Packet Tracer.<br>
•	Subnet the 192.168.100.0/24 network into multiple subnets.<br>
•	Assign subnets to LANs and WAN link.<br>
•	Configure IP addressing on routers, switches, and PCs.<br>
•	Verify connectivity using ping and router show commands.<br>
________________________________________<br>
# Apparatus / Tools Required
•	Cisco Packet Tracer<br>
•	2 Routers (R1, R2 – 2911 or equivalent)<br>
•	4 Switches (S1, S2, S3, S4)<br>
•	4 PCs (PC1–PC4)<br>
•	Copper straight-through cables for LAN links<br>
•	Serial DCE/DTE cable for WAN link<br>
________________________________________
# Network Topology Diagram
<img width="1920" height="1080" alt="Screenshot 2026-09-09 104033" src="https://github.com/user-attachments/assets/815d3458-256d-4e79-b330-0b392928acdd" />

________________________________________
# Addressing Table
Device	Interface	IP Address	Subnet Mask	Default Gateway<br>
R1	G0/0	(1st host of Subnet 0)	(Mask)	N/A<br>
R1	G0/1	(1st host of Subnet 1)	(Mask)	N/A<br>
R1	S0/0/0	(1st host of Subnet 4)	(Mask)	N/A<br>
R2	G0/0	(1st host of Subnet 2)	(Mask)	N/A<br>
R2	G0/1	(1st host of Subnet 3)	(Mask)	N/A<br>
R2	S0/0/0	(Last host of Subnet 4)	(Mask)	N/A<br>
S1	VLAN1	(2nd host of Subnet 0)	(Mask)	R1 G0/0<br>
S2	VLAN1	(2nd host of Subnet 1)	(Mask)	R1 G0/1<br>
S3	VLAN1	(2nd host of Subnet 2)	(Mask)	R2 G0/0<br>
S4	VLAN1	(2nd host of Subnet 3)	(Mask)	R2 G0/1<br>
PC1	NIC	(Last host of Subnet 0)	(Mask)	R1 G0/0<br>
PC2	NIC	(Last host of Subnet 1)	(Mask)	R1 G0/1<br>
PC3	NIC	(Last host of Subnet 2)	(Mask)	R2 G0/0<br>
PC4	NIC	(Last host of Subnet 3)	(Mask)	R2 G0/1<br>
________________________________________<br>
# Procedure
# Part 1: Subnet the Assigned Network
1.	Start with network: 192.168.100.0/24.<br>
2.	Requirements: Each LAN ≥ 25 hosts.<br>
3.	Choose subnet mask: /27 (255.255.255.224) → 32 hosts per subnet.<br>
4.	Subnets:<br>
o	Subnet 0 → LAN (R1 G0/0)<br>
o	Subnet 1 → LAN (R1 G0/1)<br>
o	Subnet 2 → LAN (R2 G0/0)<br>
o	Subnet 3 → LAN (R2 G0/1)<br>
o	Subnet 4 → WAN (R1–R2 Serial link)<br>
________________________________________<br>
# Part 2: Configure the Devices
Router R1<br>
enable<br>
configure terminal<br>
hostname R1<br>
!<br>
interface g0/0<br>
 ip address <Subnet0-1stHost> 255.255.255.224<br>
 no shutdown<br>
!<br>
interface g0/1<br>
 ip address <Subnet1-1stHost> 255.255.255.224<br>
 no shutdown<br>
!<br>
interface s0/0/0<br>
 ip address <Subnet4-1stHost> 255.255.255.252<br>
 clock rate 64000<br>
 no shutdown<br>
end<br>
copy running-config startup-config<br>
Router R2<br>
enable<br>
configure terminal<br>
hostname R2<br>
!<br>
interface g0/0<br>
 ip address <Subnet2-1stHost> 255.255.255.224<br>
 no shutdown<br>
!<br>
interface g0/1<br>
 ip address <Subnet3-1stHost> 255.255.255.224<br>
 no shutdown<br>
!<br>
interface s0/0/0<br>
 ip address <Subnet4-LastHost> 255.255.255.252<br>
 no shutdown<br>
end<br>
copy running-config startup-config<br>
Switches (S1–S4)<br>
interface vlan1<br>
 ip address <2ndHostOfSubnet><br>
 no shutdown<br>
ip default-gateway <RouterInterface><br>
PCs (PC1–PC4)<br>
•	NIC IP → Last host of each subnet.<br>
•	Subnet mask → 255.255.255.224 (LANs), 255.255.255.252 (WAN).<br>
•	Default gateway → Router interface of subnet.<br>
________________________________________<br>
# Part 3: Verification & Testing
•	On Routers:<br>
o	show ip interface brief<br>
o	show ip route<br>
•	On PCs:<br>
o	Ping default gateway<br>
o	Ping across LANs (PC1 ↔ PC3)<br>
o	Ping across WAN (PC2 ↔ PC4)<br>
________________________________________<br>
# Commands Used (Summary)
•	Mode/navigation: enable, configure terminal, end<br>
•	Interface config: interface g0/0, ip address, no shutdown<br>
•	Show/verify: show ip interface brief, show ip route<br>
•	Save: copy running-config startup-config<br>
________________________________________<br>
# Output (Attach Screenshots)
•	show ip interface brief on R1 and R2<br>
<img width="1920" height="1080" alt="Screenshot 2026-09-09 103515" src="https://github.com/user-attachments/assets/e4c3b938-a5b1-424d-963c-3b1b28f7a5ae" />

•	Successful pings PC ↔ PC<br>
<img width="1920" height="1080" alt="Screenshot 2026-09-09 103927" src="https://github.com/user-attachments/assets/f0cbedbb-982b-4ba2-9ad7-e7a10f6832b6" />

________________________________________<br>

# Result
The IPv4 subnetting scheme was successfully designed and implemented. Routers, switches, and PCs were configured with correct addressing. Connectivity within LANs and across WAN was verified.

