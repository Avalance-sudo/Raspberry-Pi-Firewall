# Raspberry-Pi-Firewall
Useing a Raspberry Pi to monitor and control network traffic between devices-turing it into 
a dedicated firewall that filters, logs, and protects systems on the network.

# What you need: 
-Raspberry Pi (any model with Ethernet + Wi-Fi or USB-to-Ethernet adapter)

-microSD card (8GB+)

-Raspberry Pi OS Lite

-Two network interfaces:

-eth0 → connects to your modem/router

-wlan0 or eth1 → connects to your secured devices

# Step 1: Update 

```sudo apt update && sudo apt full-upgrade -y```
We ran this code to ensure the Rasoberry Pi is fully up to date with the latest package lists and 
software upgrades. This helps avoids bugs or compatibility isues when installing new tools like the firewall.

 # Step 2: Install firewall and bridge tools                                                 
```sudo apt-get install ufw ```
```sudo apt update && sudo apt install bridge-utils iptables-persistent -y```
Next, we installed bridge-utils and iptables-persistent using sudo apt install bridge-units iptables -persistent -y.  bridge-untils will allow us to create a virtual bridge between network interfaces and iptables-persistent saves firewall rules. 

# Step 3:CHeck firewall status 
 ```sudo ufw status```
Then we checked the current status of the firewall with sudo ufw status to confirm wheather UFW was active or not.

 # Step 4: Creat bride device br0 and add interfaces 
 ```sudo brctl addbr br0```
 ```sudo brctl addif br0 eth0 eth1```
 We create a new bridge interface named br0 with sudo brctl addbr which willl act as a virtual link between two physical interfaces. THen we added both etho (connected to the router) and eth1 (connected to the secured device) to bride using sudo brctl addif br0 eth0 eth1.
 
 # Step 5: Allow SSH access to Pi
```sudo ufw allow ssh```
``` sudo ufw allow 2222/tcp  -custom port if needded ```
This code ensure we can still conenct to the Pi remotely through the default SSH port (22). Then we change the SSH port to 2222 for security, that allows the custom port to run sudo ufw allow 2222/tcp.

 # Step 6: Allow web traffic 
```sudo ufw allow 80```
```sudo ufw allow 443```
We finally opend port 80 (HTTP) and 443 (HTTPS) with sudo ufw allow 80 and sudo ufw allow 443, whcih allowed web traffic to flow through the PI while filtering web content. 

# Step 7: Enable firewall
```sudo ufw enable```
```sudo ufw status verbose```
Fianlly we truned on the firewall using sudo ufw enable, which actived all the rules we created. Then we ran sudo ufw status verbose to view all fireall rules with detailed output including allowed services and interfaces.
# Step 8 : Turm on logging 
```sudo ufw logging on```
Finally, we enabled firewall loggin with sudo ufw logging on so we can track and blacok traffic in our logs.
