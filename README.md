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

''sudo apt update && sudo apt full-upgrade -y''


 # Step 2: Install firewall and bridge tools                                                 
sudo apt-get install ufw 
sudo apt update && sudo apt install bridge-utils iptables-persistent -y


# Step 3:CHeck firewall status 
 sudo ufw status

 # Step 4: Creat bride device br0 and add interfaces 
 sudo brctl addbr br0
 sudo brctl addif br0 eth0 eth1
 
 # Step 5: Allow SSH access to Pi
sudo ufw allow ssh
 sudo ufw allow 2222/tcp  -custom port if needded 

 # Step 6: Allow web traffic 
sudo ufw allow 80
sudo ufw allow 443

# Step 7: Enable firewall
sudo ufw enable
sudo ufw status verbose

# Step 8 : Turm on logging 
sudo ufw logging on
