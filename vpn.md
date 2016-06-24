Setting up OpenVPN server on Raspberry Pi
=========================================
Deployed on Raspbian 8 Jessie running on Raspberry Pi 3.

## Server setup
1.  Install OpenVPN and Easy-RSA from repository.

        apt-get install openvpn easy-rsa

2.  Extract `server.conf` template from examples.

        gunzip -c /usr/share/doc/openvpn/examples/sample-config-files/server.conf.gz > /etc/openvpn/server.conf

3.  Make the following changes to `server.conf`:

    * `port 1194` to desired port
    * `dh dh1024.pem` to `dh dh2048.pem`
    * Uncomment `;push "redirect-gateway def1 bypass-dhcp`
    * Uncomment `;push "dhcp-option DNS ..."`
    * Uncomment `;user nobody` and `;group nogroup`
    * Uncomment `;log-append openvpn.log`

4.  Enable IPv4 packet forwarding in `/etc/sysctl.conf`:

    * Uncomment `#net.ipv4.ip_forward=1`

5.  Add `iptables` allow rule. Create `/etc/network/if-pre-up.d/firewall-openvpn` with the contents:

    ~~~~
    #!/bin/sh

    iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o wlan0 -j SNAT --to-source <server IP>
    ~~~~

## Create server certificates

1.  `cp -r /usr/share/easy-rsa/ /etc/openvpn`
2.  `mkdir /etc/openvpn/easy-rsa/keys`
3.  Open `/etc/openvpn/easy-rsa/vars` and customize the following lines:

    ~~~~
    export KEY_COUNTRY=
    export KEY_PROVINCE=
    export KEY_CITY=
    export KEY_ORG=
    export KEY_EMAIL=
    export KEY_OU=
    export KEY_NAME="server"
    ~~~~

4.  Generate DH parameters.

        openssl dhparam -out /etc/openvpn/dh2048.pem 2048

5.  Build the CA. Press Enter for every prompt that appears.

        cd /etc/openvpn/easy-rsa
        . ./vars
        ./clean-all
        ./build-ca

6.  Generate certificate and key. Accept or yes any prompt that appears.

        ./build-key-server server

7.  Move files to OpenVPN directory.

        cp /etc/openvpn/easy-rsa/keys/{server.crt,server.key,ca.crt} /etc/openvpn

## Create client certificates

In this configuration, each client must have a unique certificate and key
generated manually by the server. Change `client1` in directions to the desired
name of the client machine. This section must be repeated for each client.

1.  Generate key. Accept any prompts that appear.

        cd /etc/openvpn/easy-rsa
        ./build-key client1

2.  Copy client template configuration. Note the change of extension from `.conf` to `.ovpn`.

        cp /usr/share/doc/openvpn/examples/sample-config-files/client.conf keys/client.ovpn

3.  Make the following changes to `client.ovpn`:

    * `remote my-server-1 1194`: change `my-server-1 1194` to public IP and port of VPN server.
    * Uncomment `#user nobody` and `#group nogroup`
    * Comment out the following:

        ~~~~
        ca ca.crt
        cert client.crt
        key client.key
        ~~~~

    * Append the contents of `ca.crt`, `client1.crt`, `client1.key`:

        ~~~~
        <ca>
        (insert ca.crt here)
        </ca>
        <cert>
        (insert client1.crt here)
        </cert>
        <key>
        (insert client1.key here)
        </key>
        ~~~~

4.  Transfer `client1.ovpn` to the client device. This file contains all the necessary configuration information for the client to establish a VPN connection. An OpenVPN client is required to use the configuration file.

## Usage

Having completed the above, both server and client should be configured and
ready to go. 

### Starting and stopping the server

    service openvpn start
    service openvpn status
    service openvpn stop

### Server logs

With the above configuration, server logs are kept in `/etc/openvpn`. Log
location can be changed in `server.conf`.

*   Logfile: `/etc/openvpn/openvpn.log`
*   Status: `/etc/openvpn/openvpn-status.log`

### Connecting the client

The client must have its `.ovpn` file containing its unique key and certificate.
Open the file using an OpenVPN client such as Tunnelblick to connect to VPN.
