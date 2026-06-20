#college 
# Day 3
1. netstat
2. route -n
3. arn -n
4. ip (address)
5. show ip

## Step 1
1. Connects two or more VPCs with Switches and connect two such subnets through a router
## Step 2
1. Right click on router -> console
2. `enable`
3. `configure terminal`
4. 
   ```
 interface FastEthernet 0/0
 ip address <address> <mask>
 no shutdown
   ```
5. 
```
interface FastEthernet 0/1
ip address <address> <mask>
no shutdown
```
6. `exit`
7. `end`
8. `write`
## Step 3
1. open console for each VPC
2. `ip <address> <mask> <default gateway>` eg, `ip 172.16.0.10 255.255.255.0 172.16.0.1`
3. repeat for each VPC in each subnet

## Step 4
1. test connectivity between each VPC within the same subnet and different subnets through the router
2. `ping <ip address>`

# Day 4

 - DHCP(Dynamic Host Configuration Protocol) servers automatically assign IP addresses to end-users to prevent IP conflicts.
 - RARP(Reverse ARP)
 - DHCP uses the UDP protocol(Server Port: 67, Client Port: 68)
 ==Unlike Other protocols, the port number is not randomly assigned by the OS(use `less /etc/services` to  view the services list)==
 - DHCP assigns *pools* and *lease times*
 - DORA(Discover=>Broadcast, Offer=>IP Address, Request=>OK(client), Acknowledgement=>OK(server))
	- The DORA process follows:
		1. 1. DHCPDISCOVER (Client to Server): The client broadcasts a message to locate available DHCP servers on the network.
		2. DHCPOFFER (Server to Client): The DHCP server receives the broadcast and sends a unicast offer message containing an available IP address, subnet mask, gateway, and lease time.
		3. DHCPREQUEST (Client to Server): The client accepts the offer by broadcasting a message requesting the offered IP address.
		4. DHCPACK (Server to Client): The server sends a final unicast confirmation (Acknowledgement) assigning the IP address and confirming the lease, allowing the client to start using it

## Steps
1. Assign IP address to router(10.0.0.1/24)
2. Exclude IP Addresses 10.0.0.1 to 10.0.0.10
3. DHCP Pool -> Network=>10.0.0.0/24, default Gateway=>10.0.0.1, DNS=>10.0.0.2, specify domain name=>("name)
### Commands
setup wireshark between switch and any one VPC
#### Step 1
1. show running-config
2. configure terminal
3. interface FastEthernet 0/0
4. ip address 10.0.0.1 255.255.255.0
5. no shutdown
6. exit(use end to go to the lowest mode)
#### Step 2
1. ip dhcp ? (to show all commands)
2. ip dhcp excluded-address {lower IP address = 10.0.0.1} {higher IP Address = 10.0.0.10} (use '?' for help)
#### Step 3
1. ip dhcp pool {pool-name} (pressing Enter enters dhcp-config mode; use '?' to show dhcp configure commands)
2. network {network number, ie NID,  in dotted-decimal notation} {network mask in / notation or dot-notation}
3. default-router {10.0.0.1}
4. dns-server {server IP; 10.0.0.2}
5. domain-name {name}
6. lease {no. of days or 'infinite'} {no. of hours} {no. of minutes}
7. end
8. write (to save the configuration to flash)
9. show running-config (to check the configurations made)
10. show ip dhcp ?
### Step 4
1. (go to gns3 interface and turn on the pc and switch to console)
2. ip dhcp -d (shows the DORA messages) (the VPC must be connected through wireshark)
3. show ip (shows the ip configurations set in the previous steps)
### Step 5
1. (set up wireshark on the pc connection)
2. (enter ip dhcp command in the pc)
3. (wireshark intercepts DORA messages, gratuitous ARPs)
### Step 6
1. show ip dhcp pool
2. show ip dhcp binding

# Day 5
VLANs are used to logically seperate subset of machines within a LAN. It solves the problem of large Broadcast domains, IP Address Conflicts and Security risks in Layer 2. It provides flexibility by allowing for connection and isolation of two or more set of machines. By default, two seperate VLANs cannot communicate with each other.

With a VLAN ID of $n$ bits, we can have $2^n$ IDs. IDs 0, 1 and 2^(n-1) are reserved. ID 1 is reserved for _Native VLAN_.

Trunk ports are used to connect multiple VLANs unlike _Access Ports_.

Nowadays, VLANs used 802.1q protocol.

## Using Built-in Swtich
### Steps

1. Use two Ethernet Switches. Connect 4 VPCs to the first one and 2 to the other.
2. Do not connect PCs to the switch yet because VLAN info cannot be changed once set.
3. Right click on a switch1 and select configure.
4. Select the first entry from the ports and delete all the ports.
5. Add Port 0 with VLAN 10 of access type.
6. Add Port 1 with VLAN 10 of access type.
7. Add Ports 2 and 3 with VLAN 20 of type access.
8. Add Port4 with VLAN 1 of type .1q(trunk port).
9. Repeat steps 3 to 8 for Switch 2. Add three ports with VLAN 10, 20  and 1(of .1q type).
10. Connect the VPCs to the respective ports to the switches.
11. Connect the trunk ports of the switches with each other.
12. Optionally add notes with VLAN IDs and trunk ports with respective colour codes.
#### Testing the VLANs
1. Start all PCs and open consoles. Enter the following commands
2. `ip 10.0.0.1/24`{PC1}, `ip 10.0.0.2/24`{PC2} .... {till PC6}
3. `save` {all PCs}
4. Test using `ping`

## Using Add-on Switch
### Steps
1. Use Cisco L2 Switch and connect the VPCs in the same topology as before.
2. The PCs can be connected in this case because the configuration occurs in software.
3. Optionally, to make it easier to remember the ports, use first 4 for VLANs and the last port for trunking.
4. Optionally use labels as before.
5. The switch may not turn on due to licensing issues. Run keygen.py to generate a license ID. Copy [license] ... ;
6. `vim .iourc` and paste the ID and put a new line at the end.
7. The L2 switch should now start. Enter console.
#### Configuring the Switch
1. `configure terminal`
2. `vlan {id; 10}` {use ? to list all commands}
3. `name {name; red}`
4. `no shutdown`
5. `exit`
6. `vlan {id; 20}`
7. `name {name; green}`
8. `no shutdown`
9. `exit`
10. `interface range {first_interface; ethernet 0/0} - {last_interface; 1}` {range is optional to configure a range of ports together}
11. `switchport mode {mode; access}`
12. `switchport access vlan {id; 10}`
13. `no shutdown`
14. `exit`
15. Repeat 10 to 12 for ethernet 0/2 - 3 and vlan 20
16. `interface {trunk_interface; ethernet 3/3}`
17. `switchport trunk encapsulation dot1q` {specify protocol before setting mode to trunk. Use ? to view all commands}
18. `switchport mode trunk`
19. Optionally allow specific vlan IDs, otherwise allow all VLAN IDs as `switchport trunk allowed vlan 10, 20`
20. `no shutdown`
21. `end`
22. `show vlan brief` to view VLAN info
23. `show running-config` for additional info about the ports
24. `write`
25. Switch to the gns3 interface
26. Switch on all machines
27. `ip {address; 10.0.0.1/24, ..., 10.0.0.4/24}` on PCs 1 through 4
28. `save`
29. `ping {ip_address}` to ping PCs in the same VLAN.

# Day 6
Switches cannot have loops because of infinite message passing, especially in case of broadcasts, leading to **Broadcast Storms**.

The Spanning Tree Protocol is used to create a loop-free logical topology such that there may exist physical loops which can be used as redundant links in case the primary link fails. The flow through these  loops are controlled by the STP.

STP Standards are:

1. Original STP
2. Rapid Spanning Tree
3. Multiple Spanning Tree

Bridge Protocol Data Units(BPDUs) are frames exchanged between network switches running Spanning Tree Protocol (STP) to detect network loops, elect a root bridge, and ensure a loop-free topology.

## Steps
1. Create 3 L2-Sw2s and connect them through a loop using any ports.
2. Start one of the switches and open the console.
3. `show spanning-tree` to see all port roles. Initially all ports are listening/learning, however after some time they become designated.
4. `show spanning-tree detail` to see details like RSTP etc.
5. `show spanning-tree bridge detail` and `show spanning-tree root detail`.
6. Switch on another switch and open console.
7. `show spanning-tree` initially shows learning/forwarding states and finally settles at designated state. The port through which the other turned on switch is connected becomes the Root port.
8. `show spanning-tree root detail` `show spanning-tree bridge detail` . To verify, `show spanning-tree root detail` in the other switch.
9. Turn on the final switch which will create a loop. In the console, `show spanning-tree` initially shows learning states and later become designated. One of the port will be blocked, ie, the alternated port which causes the loop.
10. `show spanning-tree root detail` `show spanning-tree bridge detail` to verify the information.
11. `show spanning-tree blockedports` and `show spanning-tree summary`
12. Shutting down one of the switches and `show spanning-tree` shows learning and then to designated.


# Day 7
Looking up IP address for a given domain:
- `nslookup www.google.com`
- `dig www.google.com`
- using _dig_ for a reverse lookup
	`dig -x <ip address>`

For resolution of Fully Qualified Domain Name(FQDN):
`dig +trace www.google.com`

Common terms associated with DNS:
- Name Servers
- Authoritative Name Servers
- Caching Name Server
- Recursive Query
- DNS Resolvers
- Reverse Lookup

Record Types and their Purpose:
- SOA - Start of Authority
- A and AAAA - IP Address, IPV4, IPV6 respectively
- PTR - pointers for reverse lookup
- NS - Name Servers
- MX - SMTP Mail Exchangers
- CNAME - Canonical Name or Domain Name Alias

To view these records:
`dig -t <record type> www.google.com`

==DNS runs on UDP, Port: 52==

## Installing and Setting up a DNS Server

**Pre-requisite:** Need a static IP

1. `cat /etc/hostname` and setup _hostname_
2. `cat /etc/hosts` and setup hostname to IP address mapping
3. `cat etc/resolv.conf` and delete the nameserver, options and search lines. Then set namesserver to 127.0.0.1
4. Install `bind9, bind9-utils` in Ubuntu
5. Update necessary bind options


6. Change to root using `sudo su -`
7. `vi /etc/named.conf` to view information about DNS server configuration
8. `vi /etc/named.rfc1912.zones` and copy `zone "localhost.localdomain" IN{...};` block and paste at the end of the file and replace "localhost.localdomain" to "jecassam.ac.in", ie, the domain name.
	- Set "file" property to `"named.jecassam.forward";`
	- Copy `zone "1.0..." IN {};` and paste it at the end of the file
	- Change to "0.168.192.in-addr.arpa", ie, the domain IP
	- Change "file" property to `"named.jecassam.reverse"`
	- Save the file `named.rfc1912.zones`
	- If `named-checkconf` returns no ouput, the configuration was successful

9. `cd /var/named`
10. `cat named.ca` to check info on the root servers
11. `cp named.localhost named.jecassam.forward`
12. `cp named.loopback named.jecassam.reverse`
13. `vi named.jecassam.forward`
	- replace @ in `IN SOA @` with `ns.jecassam.ac.in. root.jecassam.ac.in. (...`
	- replace value in "serial" with `2026050701`, ie, the current date and increment it after each modification
	- replace "replace" value with `3600`, ie the time it remains in the cache
	- the remaining properties may/may not be changed
	- Change @ corresponding to NS with `ns.jecassam.ac.in.` 
	- Change IN value to `IN MX 10 mx.jecassam.ac.in`
	- Delete the remaining two lines
	- Without any indentation, put in `ns IN A 192.168.0.53`
	- Similarly `mx IN A 102.168.0.25`
	- Then `ftp IN A 102.168.0.21`
	- Then `www IN A 102.168.0.80`
	- Then `bhogdoi IN CNAME www.jecassam.ac.in.`
14. `vi named.jecassam.reverse`
	- Change similar to the forward file
	- Change `IN NS ns.jecassam.ac.in.` with indentation
	- Delete the remaining lines at the end
	- Without indentation, `53 IN PTR ns.jecassam.ac.in.`
	- Then `25 IN PTR mx.jecassam.ac.in.`
	- Then `21 IN PTR ftp.jecassam.ac.in.`
	- Then `80 IN PTR www.jecassam.ac.in.`
	- Save the file and exit
15. `chgrp named named.jecassam.*`
16. Verify with `ls -l`
17. `named-checkzone jecassam.ac.in named.jecassam.forward`
18. `cat /etc/named.rfc1912.zone`
19. `named-checkzone <IP address of last block> named.jecassam.reverse`
20. `systemctl start named`
21. `journalctl -afm`
22. `dig @127.0.0.1 www.jecassam.ac.in`
23. `dig @127.0.0.1 bhogdoi.jecassam.ac.in`
24. `dig @127.0.0.1 <ns, max>.jecassam.ac.in`
25. `dig @127.0.0.1 -x 192.168.0.25`
26. `dig @127.0.0.1 -x 192.168.0.80`
27. `dig @127.0.0.1 -t <mx, soa, ftp> jecassam.ac.in`

## Assignment

1. `sudo dnf install httpd -y`
2. `sudo systemctl enable --now httpd`
3. `sudo firewall-cmd --permanent --add-service=http`
4. `sudo firewall-cmd --reload`
5. `sudo nano /var/www/html/index.html`
6. `ip a` and test by entering the IP address in the browser
7. `sudo dnf install bind bind-utils -y`
8. `sudo nano /etc/named.conf`
	- near the bottom, add:
		```
		zone "mysite.local" IN {
	    type master;
	    file "mysite.local.db";
	};
		``` 
9. `sudo nano /var/named/mysite.local.db`
	- add the following:
		```
		$TTL 1D
@       IN SOA  mysite.local. root.mysite.local. (
                                        1       ; serial
                                        1D      ; refresh
                                        1H      ; retry
                                        1W      ; expire
                                        3H )    ; minimum

@       IN NS   mysite.local.

@       IN A    <your IP>
www     IN A    <your IP>
		```
10. Validate
		- `sudo named-checkzone mysite.local /var/named/mysite.local.db`
		- `sudo named-checkconf`
11. 
    ```
	      sudo chown root:named /var/named/mysite.local.db
		  sudo chmod 640 /var/named/mysite.local.db
    ```
12. `sudo restorecon -v /var/named/mysite.local.db`
13. `sudo firewall-cmd --permanent --add-service=dns`
14. `sudo firewall-cmd --reload`
15. `sudo nano /etc/named.conf`
		- change`listen-on port 53 { 127.0.0.1; };` to `listen-on port 53 { any; };`
		- change `allow-query     { localhost; };` to `allow-query     { any; };`
		- make sure `listen-on-v6 port 53 { ::1; };` exists
		- validate `sudo named-checkconf`
16. `sudo systemctl restart named`
17. `nslookup www.mysite.local 127.0.0.1`

## Assignment Final
1.  `sudo dnf install httpd -y`
2.  `sudo systemctl enable --now httpd`
3.  Allow HTTP through firewall
```
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
``` 
4.  Create webpage `sudo nano /var/www/html/index.html`

5.  Find IP address `ip a`
    
6. Test Apache by entering the IP in browser `http://<your-ip>`
7. Install DNS server `sudo dnf install bind bind-utils -y`
8. Configure DNS zone `sudo nano /etc/named.conf`
    Add near the bottom:
    ```
    zone "mysite.test" IN {    type master;    file "mysite.test.db";};
    ```
9. Configure named options in `/etc/named.conf`
    Change:
    ```
    listen-on port 53 { 127.0.0.1; };
    ```
    to:
    ```
    listen-on port 53 { any; };
    ```
    Change:
    ```
    allow-query     { localhost; };
    ```
    to:
    ```
    allow-query     { any; };
    ```
    Make sure this exists:
    ```
    listen-on-v6 port 53 { ::1; };
    ```
    
10.  Create zone file `sudo nano /var/named/mysite.test.db`
    Add:
	```
	$TTL 1D@   IN  SOA mysite.test. root.mysite.test. (        2026051301 ; Serial        1D         ; Refresh        1H         ; Retry        1W         ; Expire        3H )       ; Minimum@       IN  NS      mysite.test.@       IN  A       <your-ip>www     IN  A       <your-ip>
    ```

11.  Validate configuration `sudo named-checkzone mysite.test /var/named/mysite.test.db`
12. `sudo named-checkconf`    
13. Set permissions `sudo chown root:named /var/named/mysite.test.db
14. `sudo chmod 640 /var/named/mysite.test.db`
15.  Restore SELinux context `sudo restorecon -v /var/named/mysite.test.db`
16. Allow DNS through firewall `sudo firewall-cmd --permanent --add-service=dns`
17. `sudo firewall-cmd --reload` 
18. Start and enable DNS server `sudo systemctl enable --now named` 
19. Restart named after configuration changes 
    ```
    sudo systemctl restart named
    ```
20. Test DNS directly against local DNS server
    ```
    nslookup www.mysite.test 127.0.0.1
    ```
21. Configure resolver
    
    Check network interface:
    
    ```
    resolvectl status
    ```
    
    Set local DNS server for the interface:
    
    ```
    sudo resolvectl dns <interface-name> 127.0.0.1
    ```
    
    Example:
    
    ```
    sudo resolvectl dns wlp3s0 127.0.0.1
    ```
    
    Set domain routing:
    
    ```
    sudo resolvectl domain <interface-name> "~."
    ```
    
    Example:
    
    ```
    sudo resolvectl domain wlp3s0 "~."
    ```
    
    Flush DNS cache:
    
    ```
    sudo resolvectl flush-caches
    ```
    
22. Test domain resolution
    
    ```
    ping www.mysite.test
    ```
    
23.  Test webpage using domain name `curl http://www.mysite.test`
24. Open in browser
    
    ```
    http://www.mysite.test
    ```
    
25. Verify services
    
    ```
    sudo systemctl status httpd
    sudo systemctl status named
    ```


# Day 8
Types  of Sockets:
- Local Socket(Unix Domain Socket)
- Network Socket

## TCP Socket

### Server Side:
1. create a socket using `socket()`
2. name the local socket through a file name or, assign ports to network sockets through `bind()`
3. create an incoming request queue for clients to connect through `listen()`
4. create a new socket upon connection through `accept()`
5. communicate using the socket using `read()/write()`

### Client Side
1. call `socket()`
2. `connect()`
3. `read()/write()`

## UPD Socket

### Server Side:
1. `socket()`
2. `bind()`
3. `recvfrom()/sendto()` to communicate using the socket

## Local Socket

Note: Use the following for the syntax:
- `man socket`
- `man 2 bind`
- `man listen`

Note 1: Get the header files from the man pages of the functions used

Note 2: An "echo server" is a server that sends back the character(s) sent by the client

## Inet Socket
### Server Side
The basic setup code is same except for the following:
1. `AF_INET` instead of `AF_UNIX`
2. `inet_addr("127.0.0.1")` or `inet_any()`
3. Port `44332`
	Since the TCP uses Big Endian Notation and x86_64 uses Little Endian, the port number gets reversed. We can use the following for conversions:
	- `uint32_t htonl(uint32_t hostlong);`
	- `uint16_t htons(uint16_t hostshot);` 
	- `uint32_t ntohl(uint32_t netlong);`
	- `uint16_t ntohs(uint16_t netshot);` 

Note: Use `watch netstat -ant` to see the running services and states

### Client Side
1. use `AF_INET` instead of `AF_UNIX`
2. `inet_addr("127.0.0.1")` or `inet_any()`
3. Port `44332` with `hton()`

## Lab Work
1. Write a simple chat program in C using sockets
2. Write a simple socket program in C to demonstrate the use of UDP sockets.


# Socket Programming
## Client, TCP, AF_UNIX(local domain) sockets
1. Initialize macros for buffer size and socket location
2. initialize `sock` through `socket` function, exit if error
3. initialize `sockaddr_un` struct type variable, set its memory to 0, and set it's `sun_family` and `sun_path`
4. initialize a buffer array with buffer macro size
5. attempt connection through `connect` function, exit if error
6. connection is successfull
7. read from client through `fgets`, send to server using `send`
8. read from server using `recv` and store to buffer
9. print buffer message
10. break if size of buffer is 0 or specific message is typed
11. close the socket


## Server, TCP, AF_UNIX(local domain) sockets
1. define macros for buffer size and socket location
2. initialize `sockaddr_un` struct, set values through 0 with `memset` and assign `sun_family` and `sun_path`
3. initialize `server_fd` using `socket`, exit if error
4. `UNLINK()` socket location macro for safety
5. `bind`, `listen` and `accept`, exit if error in each case
6. connection is successfull
7. `recv` from client into buffer and print
8. `fgets` into buffer and `send`
9. break if exit condition is met
10. close `server_fd` and `client_fd`
11. `UNLINCK()` socket location

## Client, UDP, AF_INET(IP) sockets
1. define macros for PORT and BUFFER_SIZE
2. define array buffer with size BUFFER_SIZE
3. define struct sockaddr_in type addr
4. initialize `addr.sin_family` as AF_INET and `addr.sin_PORT` as `htons` of PORT
5. initialize `addr.sin_addr.s_addr` as `inet_addr` of "127.0.0.1"
6. define `sock` using `socket()`
7. define a string `message` and send it using `sendto()`
8. initialize `int bytes` using `recvfrom()` and recieve server message into `buffer`
9. print the message and close the socket

## Server, UDP, AF_INET(IP) sockets
1. define macros for BUFFER_SIZE and PORT
2. initialize `struct sockaddr_in` type `serv_fd` and `client_fd`
3. set the attributes `sin_port` to `htons` of PORT, `sin_addr.s_addr` to INADDR_ANY and `sin_family` to AF_INET
4. initialize `serv_fd` using `socket()`
5. use `bind()` and exit if error
6. print the server listening message
7. initialize `bytes` using `recvfrom`
8. close the socket