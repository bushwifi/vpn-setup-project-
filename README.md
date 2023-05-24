# vpn-setup-project-
ipsec vpn project 
we created using packet tracer 
ipsec protcal is used 


network configaration 
Hostname ISP 
Interface g0/1 
ip address 209.165.200.2 255.255.255.0 
No shut 
Interface g0/0 
ip address 209.165.100.2 255.255.255.0 
No shut 
Exit 
Hostname R3 
Interface g0/1 
ip address 192.168.3.1 255.255.255.0 
No shut 
Interface g0/0 
ip address 209.165.200.1 255.255.255.0 
No shut 
Exit 
ip route 0.0.0.0 0.0.0.0 209.165.200.2





Install security license 
Check for licenses 
Enter enable mode the type show version

To install the licenses 
You enter global configuration with conf t 





Then type 
License boot module c1900 technology-package 
securityk9

VPN CONFIGURATION 
Configure IPsec on the routers at each end of the 
tunnel 
ISAKMP POLICY (PHASE 1) ISAKMP 
R1 
Crypto isakmp policy 10 
 Encryption aes 256 
 Authentication pre-share 
 Group 5 
Crypto isakmp key secretkey address 209.165.200.1 
crypto ipsec transform-set R1-R3 esp-aes 256 esp-sha-hma 
Crypto map IPSEC-MAP 10 ipsec-isakmp 
 Set peer 209.165.200.1 
 Set pfs group5 
 Set security-association lifetime seconds 86400 
 Set transform-set R1-R3 
 Match address 100 
Interface GigabitEthernet0/0 
 Crypto map IPSEC-MAP 
Access-list 100 permit ip 192.168.1.0 0.0.0.255 192.168.3.0 
0.0.0.255 
R3 
Crypto isakmp policy 10 
 Encryption aes 256 
 Authentication pre-share 
 Group 5 
Crypto isakmp key secretkey address 209.165.100.1 
Crypto ipsec transform-set R3-R1 esp-aes 256 esp-sha-hmac 
! 
Crypto map IPSEC-MAP 10 ipsec-isakmp 
 Set peer 209.165.100.1 
 Set pfs group5 
 Set security-association lifetime seconds 86400 
 Set transform-set R3-R1 
 Match address 100 
Interface GigabitEthernet0/0 
 Crypto map IPSEC-MAP 
Access-list 100 permit ip 192.168.3.0 0.0.0.255 192.168.1.0 
0.0.0.255 




