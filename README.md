# OSPF-MULTI-AREA
OSPF MULTI AREA
--------------

R1#
------
R1(config)#int g0/0
R1(config-if)#ip address 12.0.0.1 255.255.255.0
R1(config-if)#no shutdown

R1(config)#int g0/1
R1(config-if)#ip address 192.168.1.1 255.255.255.0
R1(config-if)#no shutdown 

R2
----
R2(config)#int g0/2
R2(config-if)#ip address 12.0.0.2 255.255.255.0
R2(config-if)#no shutdown 

R2(config)# int g0/0
R2(config-if)#ip address 23.0.0.1 255.255.255.0
R2(config-if)#no shutdown 

R2(config)#int g0/1
R2(config-if)#ip address 20.0.0.1 255.255.255.0
R2(config-if)#no shutdown 

R3
-----
R3(config)#int g0/0
R3(config-if)#ip address 23.0.0.2 255.255.255.0
R3(config-if)#no shutdown 

R3(config)#int g0/1
R3(config-if)#ip address 192.168.2.1 255.255.255.0
R3(config-if)#no shutdown 


router mode ospf
---------------

R1#
------
R1(config)#router ospf 1
R1(config-router)#router-id 1.1.1.1
R1(config-router)#network 12.0.0.0 0.0.0.255. area 1
R1(config-router)#network 192.168.1.0 0.0.0.255 area 1
R1(config-router)#exit

Passive interface
-----------------
R1(config)#passive-interface g0/1

R2
--------
R2(config)#router ospf 1
R2(config-router)#router-id 2.2.2.2
R2(config-router)#network 12.0.0.0 0.0.0.255 area 1
R2(config-router)#network 20.0.0.0 0.0.0.255 area 10
R2(config-router)#network 23.0.0.0 0.0.0.255 area 0

Passive interface
-----------------
R2(config)#passive-interface g0/1

R3
------
R3(config)#router ospf 1
R3(config-router)#router-id 3.3.3.3
R3(config-router)#network 23.0.0.0 0.0.0.255 area 0
R3(config-router)#network 192.168.2.0 0.0.0.255 area 0

Passive interface
-----------------
R3(config)#passive-interface g0/1
![OSPF MULT AREA](https://user-images.githubusercontent.com/106605770/177992114-9431aa1a-0a02-4661-947a-4d0f1eba6202.jpg)
