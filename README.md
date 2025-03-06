for all routers....
enable secret enpa55 
line console 0
password conpa55
login
exit

for all routers....
ip domain-name ccnasecurity.com 
username admin secret adminpa55
line vty 0 4
login local
exit
crypto key generate rsa 
1024

R1
router ospf 1 
network 192.168.1.0 0.0.0.255 area 0 
network 10.1.1.0 0.0.0.3 area 0

R2
router ospf 1 
network 10.1.1.0 0.0.0.3 area 0
network 10.2.2.0 0.0.0.3 area 0

R3
router ospf 1
 network 10.2.2.0 0.0.0.3 area 0 
 network 192.168.3.0 0.0.0.255 area 0 

R1
R1# show version 
R1(config)# license boot module c1900 technology-package securityk9
-type yes
R1# copy run start 
R1# reload 
R1# show version

R1# mkdir ipsdir 
ip ips config location flash:ipsdir 
 ip ips name iosips 
 ip ips notify log 
exit
R1# clock set hr:min:sec date month year 
 service timestamps log datetime msec
logging host 192.168.1.50
ip ips signature-category
category all 
retired true 
 exit 
 category ios_ips basic 
retired false 
 exit 
 exit

 int gig0/0 
 ip ips iosips out 
R1# show ip ips all
(Click the Syslog server->Services tab-> SYSLOG 
(Output))

R1
 ip ips signature-definition 
 signature 2004 0 
 status 
 retired false 
 enabled true 
 exit 
 engine 
event-action produce-alert 
event-action deny-packet-inline 
exit 
exit 
 exit

R1# show ip ips all
PCC> ping 192.168.1.2(Unsuccessful – Request timed out) 
PCA> ping 192.168.3.2(Successful)
Click the Syslog server->Services tab-> SYSLOG
