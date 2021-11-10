# ssh

## Key Generation

```bash
ssh-keygen -f id_rsa
# private key: id_rsa
# public key: id_rsa.pub
```

## Key Insertion for root user

1. Generate key
2. copy `id_rsa.pub` to `/root/.ssh/authorized_keys`

## Perms Error

1. For private key file:
    1. `chmod 600 id_rsa`
2. For `authorized_keys` file:
    1. `chmod 700 /root/.ssh`
    2. `chmod 700 /root/.ssh/authorized_keys`

## flags for common errors

```bash
# flag for algorithm
-okexAlgorithms=+diffie-hellman-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1

# flag for public key
-oPubkeyAcceptedKeyTypes=+ssh-dss

# flag for cipher
-c aes128-cbc
```

## Kali ssh server (for incoming connection)

```bash
apt install openssh-server

# backup default keys; generate new pair
mkdir /etc/ssh/default_keys; mv /etc/ssh/ssh_host_* /etc/ssh/default_keys/
dpkg-reconfigure openssh-server

# change /etc/ssh/sshd_config
PubkeyAuthentication yes
PasswordAuthentication no
PermitRootLogin no

# start / stop / status service
systemctl [enable|disable] ssh.service
systemctl [start|status|stop] ssh.service
```

## References

* [lmgsecurity.com/enable-start-ssh-kali-linux/](https://www.lmgsecurity.com/enable-start-ssh-kali-linux/)