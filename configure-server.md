# install packages

    sudo yum update
    sudo yum install epel-release
    sudo yum install openvpn easy-rsa

    cd /etc/openvpn
    sudo vi server.conf

# now work as root

    sudo -s
    cd /usr/share/easy-rsa/2.0/
    source vars
    ./pkitool
    source ./vars
    ./clean-all
    ./build-dh
    ./pkitool --initca
    ./pkitool --server myserver
    ./pkitool macbook
    cd keys
    cp ca.crt myserver.{crt,key} /etc/openvpn/
    cd /usr/share/doc/openvpn-2.3.8/sample/sample-config-files
    cp server.conf /etc/openvpn/
    cp client.conf /usr/share/easy-rsa/2.0/keys/
    cd /usr/share/easy-rsa/2.0/keys/
    cp dh2048.pem /etc/openvpn/
    cd /etc/openvpn
    vi server.conf
    openvpn --config server.conf
    mv myserver.key server.key
    mv myserver.crt server.crt
    systemctl status openvpn@server.service
    systemctl start openvpn@server
    cd /usr/share/easy-rsa/2.0/keys/
    ./pkitool --help
    ./pkitool macbook
    cd keys
    view client.conf 
    mkdir ~/macbook
    cp macbook* ~/macbook
    chmod -R +r ~/macbook
    systemctl restart openvpn@server
    systemctl status openvpn@server
    cat /proc/sys/net/ipv4/ip_forward
    echo 1 > /proc/sys/net/ipv4/ip_forward
    ip route ls
    ping 10.8.0.2
    vi /etc/sysctl.conf 
    echo 0 > /proc/sys/net/ipv4/ip_forward
    sysctl -p
    systemctl enable openvpn@server
