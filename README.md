# Hotel-Management-Networking
Hotel Configurating and Installation
Steps of my work 

Hotel Networking Project :

First of all we install the routers and switches and everything is mentioned

Then we rename them by the floor Number , After that we should open physical device view and turn it off to add physical serial port by module HWIC-2T to be able to 
connect the Serial DCE cable and at last we should turn it ON. (we do this for the 3 routers).

Note: we should enable clock rate 

After installation we should start configuration

Clock Rate: In this case we use 64000 which we are setting the speed of the interface

In the configuration we Do a VLAN for each department with the written information

And with them to communicate with other departments 

We did trunk for f0/1 in each switch

The case study says that the ip address should be assigned automatically , so We are going to use f2 router as a DHCP Server and this should go hand in hand with 
interval routing 

Whenever we have many venues  and multiple venues in network we configure interval and route plus DHCP server 

Starting with interval and routing 

I’ll start on F1 router rate clock , we start by creating sub interfaces and we assign Vlan nbr and ip address to those sub interfaces and that IP addresses will act 
as the default gateway to the respective Vlan. 

We use command int gig0/0.80 starting with reception

Encapsulation dot1Q 80

Ip address 192.168.8.1 255.255.255.0

And continue on other Vlans with specific IP address for each department 

Lets configure DHCP server on the F1 router 

Since we have 3 departments we need to configure 3 pools , and whenever we are configuring DHCP server we click the pools 

By service DHCP

Ip dhcp pool Reception 

Network 192.168.8.0 255.255.255.0

Default-router 192.168.8.1

Dns-server 192.168.8.1

Here we finish the pool for The reception 

And continue the same steps with each department with the given ip

So After finishing with each floor we should ping 

Go for the PCS and to Desktop – IP Configuration—and change from static to DHCP and it will request IP address in the range that we give. Try to ping to check if 
everything is working well

But if we try to ping from any department in any floor to another department in different floor the host will be unreachable . Then we need to configure routing protocol on all routers 

Starting with F1 router we need to configure OSPF Protocol on this route to advertise all these networks 

Enable

Configure terminal 

Router OSPF 10

Network 10.10.10.4 255.255.255.252 area 0

Network 10.10.10.8 255.255.255.252 area 0

Network 192.168.8.0 255.255.255.0 area 0

Network 192.168.7.0 255.255.255.0 area 0

Network 192.168.6.0 255.255.255.0 area 0

Area 0 is the central area or the backbone area in OSPF routing and all areas must connect to . When traffic needs to pass from area to another it must traverse the 
backbone.

And do this on all the routers with the same range and same area but ofcourse different ip according to what is given and mentioned in the graph. 

In addition to that we just added 1 wireless device at each floor and configure the access point with SSID and password and connect each device wirelessly to the 
access point with username and password

Now we should configure SSH :

The first thing is to do configure the Host name of that particular device

Hostname F3-Router

Ip domain-name Technology password 112233 

Crypto key generate rsa

1024

Line vty 0 15 (which is 16 interfaces)

Login local 

Transport input SSH 

Do wr

‘’’’Do this for all routers with Different Host names¨¨¨¨



I have changed The name of PC in the IT department to TEST PC to solve the last problem in the given

We wan tot access the F2 router interface from our PC. We can choose any ip address of the interface from fast ethernet or serial. So I am going to choose the Serial 

By using the command in Test pc type “ssh -l Technology 10.10.10.1”

And the password 112233

At last we only need to configure port security to IT dept switch to allow only Test PC to access port fa0/2

Command for F3 Switch:

Enable 

Configure 

Interface fa0/2

Switchport port-security maximum 1

Switchport port-security mac-address sticky

Switchport port-security violation shutdown

Do wr

To check always try do show start

Try also show port-security

The End 















