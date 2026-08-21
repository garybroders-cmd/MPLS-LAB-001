# MPLS-LAB-001 - Notes

No security atm.  TBA.

r-mpls-1- 6 are simple MPLS using ISIS routing
PE routers for sites
CDE routers
SPINE Routers

leaf a and b doing extended VXLAN using EVPN for VLAN 20 and VLAN 10.


Linux devices using DHCP via switches for VLAN 10 and VLAN 20.

Commands

leaf-b-site-4# show nve peers

Interface Peer-IP                                 State LearnType Uptime   Route
r-Mac       
--------- --------------------------------------  ----- --------- -------- -----------------
nve1      172.6.5.1                               Up    CP        02:16:55 500f.0000.1b08   


leaf-a-site-6# show nve vni
Codes: CP - Control Plane        DP - Data Plane          
       UC - Unconfigured         SA - Suppress ARP        
       S-ND - Suppress ND        
       SU - Suppress Unknown Unicast 
       Xconn - Crossconnect      
       MS-IR - Multisite Ingress Replication 
       HYB - Hybrid IRB mode
    
Interface VNI      Multicast-group   State Mode Type [BD/VRF]      Flags
--------- -------- ----------------- ----- ---- ------------------ -----
nve1      1010     UnicastBGP        Up    CP   L2 [10]                 
nve1      1020     UnicastBGP        Up    CP   L2 [20]                 
nve1      50000    n/a               Up    CP   L3 [PROD]               

leaf-a-site-6# show nve vni 1010 detail
VNI: 1010 
  NVE-Interface       : nve1
  Mcast-Addr          : UnicastBGP
  VNI State           : Up
  Mode                : control-plane
  VNI Type            : L2 [10]
  VNI Flags           : 
  DCI Mcast-Addr      : Unconfigured
  Provision State     : vni-add-complete
  Vlan-BD             : 10
  SVI State           : UP [vrf-id: 4] [L3VNI: 50000]


leaf-a-site-6# show mac address-table vlan 10
Legend: 
        * - primary entry, G - Gateway MAC, (R) - Routed MAC, O - Overlay MAC
        age - seconds since last seen,+ - primary entry using vPC Peer-Link,
        (T) - True, (F) - False, C - ControlPlane MAC, ~ - vsan,
        (NA)- Not Applicable A – ESI Active Path, S – ESI Standby Path
   VLAN     MAC Address      Type      age     Secure NTFY Ports
---------+-----------------+--------+---------+------+----+------------------
*   10     0050.0100.1500   dynamic  NA         F      F    Eth1/10
*   10     0050.0100.1600   dynamic  NA         F      F    Eth1/10
*   10     0050.0100.1700   dynamic  NA         F      F    Eth1/10
C   10     0050.0100.1800   dynamic  NA         F      F    nve1(172.4.5.1)
C   10     0050.0100.1900   dynamic  NA         F      F    nve1(172.4.5.1)
C   10     0050.0100.1a00   dynamic  NA         F      F    nve1(172.4.5.1)
*   10     5001.0011.800a   dynamic  NA         F      F    Eth1/10
C   10     5001.0013.800a   dynamic  NA         F      F    nve1(172.4.5.1)
G   10     500f.0000.1b08   static   -         F      F    sup-eth1(R)



Pal-ALto Cheat Commands

set cli config-output-format set. - see the configuration set display mode


NAT
debug ip nat - see nat translations
debug ip icmp - see 


Palo Alto Cheat

show high-availability state
show high-availability all
show session info
show counter global filter delta yes

show high-availability state | match sync


>>>> Force a synce from actibve firewall
request high-availability sync-to-remote running-config


>>>> on passive firewall
debug software restart process management-server





Palo Alto

admin@PA-FW-SITE-4-a(active-primary)> show arp all

maximum of entries supported :      32000
default timeout:                    1800 seconds
total ARP entries in table :        4
total ARP entries shown :           4
status: s - static, c - complete, e - expiring, i - incomplete

interface                ip address      hw address        port              status   ttl  
--------------------------------------------------------------------------------
ethernet1/1              10.160.14.1     50:01:00:1f:00:01 ethernet1/1                c      995  
ethernet1/1              10.160.14.6     50:01:00:20:00:01 ethernet1/1                c      1490 
ethernet1/2              10.160.4.3      50:01:00:20:00:02 ethernet1/2                c      1490 
ethernet1/2              10.160.4.4      50:02:00:00:1b:08 ethernet1/2                c      1446 

admin@PA-FW-SITE-4-a(active-primary)> 


admin@PA-FW-SITE-4-a(active-primary)> show high-availability virtual-address 

Total interfaces with virtual address configured:   2
Total virtual addresses configured:                 2
--------------------------------------------------------------------------------
Interface: ethernet1/1                   
  Virtual MAC:               50:01:00:21:00:01
  10.160.14.4                             Active:yes Type:floating   Pri-Bind:no 
--------------------------------------------------------------------------------
Interface: ethernet1/2                   
  Virtual MAC:               50:01:00:21:00:02
  10.160.4.1                              Active:yes Type:floating   Pri-Bind:no 
--------------------------------------------------------------------------------
admin@PA-FW-SITE-4-a(active-primary)> 

