# Advanced networking

## ip address (internet)
127.0.0.1 ---> this is the loopback address or home address
01111111.00000000.00000000.00000001 ---> in binary is 127.0.0.1 (This is how the computer reads the ip address in binary)
(an ip address in made up of four parts with eight 0s or 1s) --> ipv4

Not enough ip addresses for the whole world
So an ip address is owned by isp (internet server provider)
  - eg A company has 1 ip address all employees have private addresses for their laptops/phones/electronic devices
So people use private addresses

## Private address (works locally)
- 10.0.0.1 class A           ----> (few networks, massive number of computers)
- 172.16.0.0 class B
- 192.168.0.0 class C       ----> (big networks, small number of computers)

## subnets
- May be used to break network into smaller chunkes, firewall or router used to segment networks from eachother
- Whenever you have a subnet traffic will no longer flow normally
- Analogy of the hotel
- For all subnets need Default Gateway (Default Gateway acts as receptionist in hotel analogy)
- Whenever you have 2 computers in different subnets you need a router or a default gateway

## Using the subnet mask
- Subnet mask is needed to be able to differentiate which part of ip address belongs to the network and which part belongs the the host or computer
- If the network part of ip address is same they belong to same subnet
- An ip address is made up of 2 parts ---> host and network
- For an ip address all the 1s belong to network, all 0s belong to host

## CIDR (classless inter-domain routing)
10.0.0.0/8        -----> (means first 8 bits belong to network ie first part network)
10.0.0.0/16       -----> (means first 16 bits belong to network ie first 2 parts network)
10.0.0.0/24       -----> (means first 24 bits belong to network ie first 3 parts are network)

aws vpc Daniel using 10.0.0.0/16 create subnets
10.0.1.0/24
therefore 10.0.1.1 would be the first computers
10.0.1.254 last computer

- If you want more computers create another subnet
10.0.12.0/24
10.0.12.1 first computer
10.0.12.254 last computer

## IPv6
- The latest version of IP

## Network Address Translation or NAT
- When your computer (private address) makes a request
  - request goes to default gateway, it takes traffic and swaps with the actual ip address and makes the request to the internet
  - when it gets response it remember the private address ip of the computer and send it to this computer
