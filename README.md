# Autoware RO2 Source Installation Behind Firewall - Humble Edition
## Prerequisites
- Ubuntu 22.04 on WSL2
- [wsl-vpnkit](https://github.com/sakai135/wsl-vpnkit/)
## Terminal Launch
Launch a CMD terminal and start wsl-vpnkit.
Make sure it it can connect to Internet before proceeding...
```sh
wsl
wsl.exe -d wsl-vpnkit service wsl-vpnkit start
```
## Installation
Please follow through the [source installation](https://autowarefoundation.github.io/autoware-documentation/main/installation/autoware/source-installation)

Common build issue:
- Certificate errors when connecting to s3.amazonaws.com
-- Disabling APT OCSP Verification
```sh
sudo su
touch /etc/apt/apt.conf.d/s3amazonautostuff-cert
echo 'Acquire::https::s3.amazonaws.com::Verify-Peer "false";' > /etc/apt/apt.conf.d/s3amazonautostuff-cert
exit
```

- Certificate errors when installing kvaser driver
For example, when executing the following command to add the PPA repository to the list, common issue found like: "ssl.SSLCertVerificationError: [SSL: CERTIFICATE_VERIFY_FAILED]". 
```sh
sudo apt-add-repository ppa:astuff/kvaser-linux
```
Manually create the source list in directory: /etc/apt/sources.list.d, and disable OCSP verification
add the following link to source (jammy if your ubuntu version is 22.04):
deb [trusted=yes] https://ppa.launchpadcontent.net/astuff/kvaser-linux/ubuntu jammy main 
deb-src [trusted=yes] https://ppa.launchpadcontent.net/astuff/kvaser-linux/ubuntu jammy main

```sh
cd /etc/apt/sources.list.d
sudo vi kvaser.list
```
If you are sure the package is trusted, please do the following
-- Disabling APT OCSP Verification
```sh
sudo su
touch /etc/apt/apt.conf.d/kvaser-cert
echo 'Acquire::https::ppa.launchpadcontent.net::Verify-Peer "false";' > /etc/apt/apt.conf.d/kvaser-cert
exit
```
- Firewall policy to deny gdown
--Please do a separate download on the computer and install manually

