## this is a bash scipt to connect to vpn via [Linux OpenConnect](https://wiki.archlinux.org/index.php/OpenConnect) cli client with [VIPAccess TOTP](https://vip.symantec.com/)

Works on LinuxMint 18.2, should be ok on correspond Ubuntu ver

## preparation:

1. install some needed packages in right order:
```
sudo apt-get install -y openconnect
sudo apt-get install -y python-pip
sudo pip install setuptools
sudo pip install lxml oath PyCrypto requests
```
2. install and setup VIPAccess TOTP:
```
#git clone https://github.com/dlenski/python-vipaccess.git
cd python-vipaccess
sudo pip install .
vipaccess provision -o ~/.vipaccess
```
3. now, you will need to login on VIPAccess page, and register CredentialsID, from last command output

(in order to do this, you shoud have already registered at list one CredentialsID on VIPAccess, and be able to login there)

4. add next to ~/.bashrc
(use actual data for variables!!!)


```
export LDAP_USERNAME=''
export LDAP_PASSWORD=''
export VIPACCESS_TOTP=$(vipaccess)
export VPN_PASSWORD=${LDAP_PASSWORD}${VIPACCESS_TOTP}
export VPN_SERVER=
export VPN_GROUP=
```

5. do some born stuff again :
```
source ~/.bashrc
cd ../
sudo chmod +x vpn_openconnect
sudo cp vpn_openconnect /usr/bin/
```


6. enjoy! :
```
vpn_openconnect start
```

# usage:
```
vpn_openconnect stop
vpn_openconnect start
vpn_openconnect restart
vpn_openconnect status
```
