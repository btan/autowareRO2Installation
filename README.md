# Autoware RO2 Source Installation Behind Firewall - Humble Edition
## Prerequisites
Ubuntu 22.04 on WSL2
[wsl-vpnkit](https://github.com/sakai135/wsl-vpnkit/)
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
- Firewall policy to deny gdown
--Please do a separate download on the computer and install manually

