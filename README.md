# pfSense Lab

## Objective



### Skills Learned

- 

## Steps

To begin, I am creating two virtual networks, the first for the Windows VM and the second for the Kali Linux VM. The pfSense VM will have two NIC's and act as a router to route traffic between both networks. This is to simulate a real network in a virtual setting. I am using 10.0.2.0/24 for the Windows machine and 192.168.2.0/24 for the Kali Machine. It is important to change the adapter of the VMs to its corresponding networks.

<img src="NATnetworks.png" alt="NAT Networks" width="600">
 
After installing pfSense, I configured em0 (LAN) and em1 (LAN) to have IP addresses in the corresponding subnet which was created in the first step.

<img src="WAN_LAN.png" alt="LAN and WAN" width="600">

Now that we have our LAN and WAN, I will manually configure the IPv4 settings on the Windows VM to have an IP address in the LAN subnet and to set the default gateway to the pfSense LAN address.

<img src="IPv4.png" alt="IPv4 Settings" width="400">

Those changes will now grant access to the pfSense login page via the default gateway IP address entered into the search bar. Using the default credentials, we can now log in (User: admin / Password: pfsense)

<img src="pfSense_login.png" alt="pfSense Login Page" width="600">

In pfSense, I navigated to System -> Routing -> Gateways to add the LAN gateway associated with the pfSense LAN. The WAN gateway is already configured, so only a configuration for LAN needs to be made.

<img src="LAN_gateway.png" alt="LAN Gateway" width="600">

To ensure that the network is correctfully configured, I will ping the LAN and WAN interfaces from the Windows machine.

<img src="pingLAN_WAN.png" alt="Network Setup Complete" width="500">

On the Kali Linux machine, I will add the default gateway of the pfSense WAN address. 

<img src="defaultGateway.png" alt="Kali Linux WAN Gateway" width="500">

That is all for setting the network up. When attempting a ping of the Windows Machine from Kali Linux, it will fail because pfSense denies all traffic by default. 

<img src="failedPing.png" alt="Failed Ping Attempt" width="600">

In order to allow traffic between the two machines, we have to create a firewall rule. In this rule, I specify that all traffic from the address 192.168.2.5 (Kali Linux) should be allowed to pass. I also chose WAN for the interface.

<img src="passFirewallRule.png" alt="Allow Traffic Firewall Rule" width="600">

Now we can try the ping again to see if the firewall rule is allowing traffic from Kali Linux to be sent to the Windows machine.

<img src="successPing.png" alt="Successful Ping Attempt" width="600">

