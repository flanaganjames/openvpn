# install packages

    sudo yum update
    sudo yum install epel-release
    sudo yum install openvpn easy-rsa

# now work as root

    sudo -s
    cd /usr/share/easy-rsa/2.0/
    source ./vars
    ./clean-all
    ./build-dh
    ./pkitool --initca
    ./pkitool --server myserver
    ./pkitool macbook
    cd keys
    cp ca.crt myserver.{crt,key} /etc/openvpn/
    # only the ca.crt and the myserver.* files have to be copied to the /etc/openvpn (not the macbok.* files
    
    cd /usr/share/doc/openvpn-2.3.8/sample/sample-config-files

    
    cp server.conf /etc/openvpn/
    cp client.conf /usr/share/easy-rsa/2.0/keys/  
    # the client conf file will be a ovpn file for macbook VNC server and client
    
    cd /usr/share/easy-rsa/2.0/keys/
    cp dh2048.pem /etc/openvpn/
    # this also has to be in the /etc/openvpn
    
    cd /etc/openvpn
    vi server.conf
    vi server.conf
    # update this copy of file so that: port 1194, proto udp, dev tun, ca ca.crt, cert server.crt, key server.key, dh dh2048.pem
    # topology subnet, server 10.8.0.0 255.255.255.0, ifconfig-pool-persist ipp.txt, client-to-client, keepalive 10 120, verb 3
    # are all uncommented
    
    
    # rename these files in /etc/openvpn
    mv myserver.key server.key
    mv myserver.crt server.crt
    openvpn --config server.conf
    
    systemctl start openvpn@server
    systemctl status openvpn@server.service
    cd /usr/share/easy-rsa/2.0/
    ./pkitool macbook
    cd keys
    # the macbook files can be left in /usr/share/easy-rsa/2.0/keys
    #you need a different set of macbook files for each macbook client to connect

    systemctl restart openvpn@server
    systemctl status openvpn@server
    cat /proc/sys/net/ipv4/ip_forward
    echo 1 > /proc/sys/net/ipv4/ip_forward
    # /proc/sys/net/ipv4/ip_forward must have a 1 in it for forwarding to occur
    
    ip route ls
  
    vi /etc/sysctl.conf 
    
    # ask John about this? 
    echo 0 > /proc/sys/net/ipv4/ip_forward
    sysctl -p
    
    
    systemctl enable openvpn@server
