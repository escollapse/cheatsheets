# ****THIS IS JUST TO GET YOU UP AND RUNNING WITH A STATIC KEY****

# ****THERE ARE A MULTITUDE OF WAYS TO MAKE THIS MORE SECURE****

## seriously, tailor this to your needs (and harden it).  i just wanted to capture the final solution

# env:
* vpn svr = centos
* phone = android

# ****got ADB?****

# ****got debugging enabled on your phone?****

# ****know your public IP?****

## prepare server
openvpn --genkey --secret static.key

sudo firewall-cmd --permanent --add-port=<desiredPort>/udp

sudo firewall-cmd --permanent --add-masquerade

sudo firewall-cmd --reload

sudo vim /etc/sysctl.conf

* net.ipv4.ip_forward = 1

sudo /sbin/sysctl -p

## author server.conf
ifconfig <server tunnel IP> <phone tunnel IP>

port <desiredPort>

proto udp

dev tun

secret </path/to/static.key>

user nobody

group nobody

cipher AES-256-CBC

auth SHA256

status openvpn-status.log

verb 6

explicit-exit-notify 1

## author client.ovpn
client

ifconfig <phone tunnel IP> <server tunnel IP>

proto udp

dev tun

cipher AES-256-CBC

auth SHA256

remote <your public IP> <desiredPort>

user nobody

group nobody

secret static.key

verb 3

## prepare phone
* from Play Store, download "OpenVPN for Android" by Arne Schwabe
* adb push </path/to/client.ovpn> /sdcard/Download
* adb push </path/to/static.key> /sdcard/Download
* in application, add profile
* IP AND DNS --> searchDomain --> <clear-out>
* ROUTING --> IPv[4|6] --> Use default route --> <check box>

## prepare Internet-facing router
(and mesh-wifi configuration, if necessary)

* port forward <<desiredPort>> to <<server>>

## set it off
on server:

* sudo openvpn --config </path/to/server.conf>

on phone, in application:

* tap profile and connect