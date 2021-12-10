# rpc

## Recon

```bash
# rpcbind port converts RPC to universal address 
# allows to access the NFS, port:111 
nmap --script=nfs-ls,nfs-statfs,nfs-showmount -p 111 $ip

nmap --script rpcinfo.nse -p 111 $ip
rpcinfo –p IP
rpcbind -p IP

# dumps the remote RPC endpoints information via epmapper.
impacket-rpcdump @[IP | DOMAIN]
```

## rpclient

* [Plundering Windows Account Info via **
  Authenticated** SMB Sessions](https://www.sans.org/blog/plundering-windows-account-info-via-authenticated-smb-sessions/)

```bash
rpcclient -U ['' | USER%PASS | DOMAIN\USER%PASS] IP [-N]
# -N: no password

srvinfo: server information => os.version, samba-version.
netshareenum: enumerate shares

# basic info
querydominfo: domain info
enumdomusers: enum domain users
enumdomgroups: enum domain groups
dsr_enumtrustdom: enumerate trusted domains

# query group info and membership
querygroup 0xGROUP
querygrupmem 0xGROUP

# query specific user by RID
queryuser USER
lookupnames USER (if user exists)

# password policy
querydompwinfo

enumdrivers
enumprinters
```

## enumerate users using SIDs (windows only)

```bash
# needs some user creds (smb also works)
impacket-lookupsid USER:PASS@IP
```
