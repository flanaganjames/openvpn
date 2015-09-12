## Configuring the Mac as a client

This assumes you've created an OpenVPN server at IP 1.2.3.4, and put the correctly-configured
a macbook.ovpn configuration file into the user's home directory on that server.

The IP of the client on the VPN is assumed to be 10.8.0.2

- download tunnelblick from the web and install

      type tunnelblick # verify it's installed

- verify access to openvpn server

      ping 1.2.3.4 # server's public key

- add public key to openvpn server's .ssh/authorized-keys

  - grab a copy of the macbook's public key

        pbcopy < ~/.ssh/id_rsa.pub

  - paste that into openvpn server's .ssh/authorized keys

- copy over configuration file from openvpn server

      scp -r joe_user@1.2.3.4:macbook.ovpn Desktop

- start tunnelblick

  - in the Finder, double-click *Desktop/macbook.ovpn*,
then start tunnelblick by clicking on tunnel icon
in status bar at the top of the screen

- connect to remote client

 - verify connectivity to remote client

        ping 10.8.0.2

  -  copy keys if necessary

          ssh copy-id j_workuser@10.8.0.2
          ssh j_workuser@10.8.0.2

- set up a convenient way to get in

  - add an alias to the mac's ssh config file

        cat << __EOF__ >> ~/.ssh/config
        Host work
        Hostname 10.8.0.2
        User j_workuser
        __EOF__

 - and test it

        ssh work
