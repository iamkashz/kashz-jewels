# ipsec ike-vpn :500/udp

## IPSEC type of Internet Security Association Key Management Protocol (ISAKMP)

Framework for authentication and key exchange. Phases in setting up security association (SA) between endpoints:

1. Establish secure channel using PreSharedKey (PSK) or certificates. It can use main mode (3 pairs of messages) or aggressive mode.
2. (optional) Extended AUTH Phase - authenticates the user trying to connect.
3. Negotiates the parameter for data security using ESP or AH. Can use different algorithm than phase

## Connect

```bash
sudo ipsec statusall

# auto=start
sudo ipsec [start --nofork]

# auto=add
sudo ipsec [start | stop]
sudo ipsec [up | down] CONFIG-NAME
```

## Config files

### /etc/ipsec.secrets

```bash
/etc/ipsec.secrets
| this file hold shared secrets or RSA private keys for authentication

# add line
TARGET-IP %any : PSK "PASSWORD"
```

### /etc/ipsec.conf

```bash
/etc/ipsec.conf
| setup to enable verbose debugging
| conn profile to connect
config setup
    charondebug="all"

config CONFIG-NAME
    # basic config
    auto=start [ | add]
    authby=secret [ | psk]

    # tunnel when have subnets
    type=transport [ | tunnel]

    # left side config
    left=KALI-IP
    leftsubnet=KALI-IP[PROTOCOL] | leftprotoport=PROTOCOL

    # right side config
    right=TARGET-IP
    leftsubnet=TARGET-IP[PROTOCOL] | leftprotoport=PROTOCOL

    # IKE config
    keyexchange=ikev1 [|ikev2]
    # example: 3des-sha1-modp!
    ike=ALGORITHM-HASH-GROUP!
    esp=ALGORITHM-HASH!
```

## Install Strongswan

```bash
sudo apt install strongswan libstrongswan-standard-plugins libstrongswan-extra-plugins
```

##
