# Create a box

## click on "new instance"

## configure the instance
- set the name to something recognizable, such as __openvpn__, or __myopenvpn-server__
- choose "g1-small" instance (f1-micro won't work)
- modify description to be a CentOS 7 box in whatever Zone you like
- "Management, disk, network, access, and security options" -> Network
- "External IP" -> "Static" and "IP forwarding" -> "On"
*Copy the static IP address. You'll need it later.*
- Click on create

## configure the firewall
- cick on the machine name -> Network
- "Firewall rules" -> "Create a new firewall rule"
    - Name: "allow-openvpn"
    - Source IP Ranges: 0.0.0.0/0
    - Allowed protocols and ports: udp:1194

## configure the machine
- Click on SSH for the running machine
- Follow instructions in configure-server.md






