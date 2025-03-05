# 3-tiered-Hierarchy-work-in-progress-
Network A is on the left and network B is on the right.
I havent configured passwords and usernames on the network devices to make configuring the devices less tedious

Network A
In the access layer of network A portfast and bpduguard was enabled globally and will be in effect for any ports not in trunking mode.
I set up 2 different offices, one for upper management and one for human resources. Vlan 100 is for management, 200 is for HR and 199 is for the native vlan.
The uplink to the distribution layer is setup with etherchannel (vlan 199 is the native). Vlans are extended to the distribution layer and HSRP is configured between the SVIs between the distribution multilayer switches.
The management office has a 172.16.0.0 /25 network and the virtual IP/gateway is 172.16.0.3
The HR office has a 172.16.0.128 /25 network and the virtual IP/gateway is 172.16.0.66

I created a dhcp server with an ip address of 198.150.6.1. I placed a router infront the dhcp server so I would only need to configure one ip address as a helper address when configuring the SVIs as relay agents.
I configured ospf to avoid configuring static routes for ever. Area 0 is the core layer, area 1 is network A and area 2 is network B. The process id number used through out the whole network is 65. I havent configured router ids yet.
All links between networking devices uses a /30 subnet. 
Each redundant pair of multilayer switches has a layer 3 ethwechannel link between them.
The uplink from the distribution layer to the core layer ueses layer 3 etherchannel.

I plan on implementing NAT and ACls in the distribution layer later since the ASA firewall in packect tracer doesnt support them. 
Im trying to configure a ntp server in the core layer but, besides that the core layer focuses on just routing.
