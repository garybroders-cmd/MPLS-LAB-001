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

