# rpc

## Recon

```bash
# rpcbind port converts RPC to universal address 
# allows to access the NFS, port:111 
nmap --script=nfs-ls,nfs-statfs,nfs-showmount -p 111 $ip

nmap --script rpcinfo.nse -p 111 $ip
rpcinfo –p IP
rpcbind -p IP

# dumps the remote RPC enpoints information via epmapper.
/opt/impacket/examples/rpcdump.py @[IP | DOMAIN]
```

## rpclient

```bash
rpcclient -U ['' | USER | DOMAIN\USER] IP
srvinfo: server information => os.version, samba-version.

querydominfo
enumdomusers: enum DOM users
enumalsgroups domain: ?

lookupnames USER: looks up USER if exists
queryuser USER: Get more information about user

enumprinters: enum printers
```

## enumerate users using SIDs (windows only)

```
# needs some user creds (smb also works)
lookupsid.py <USER>:<PASS>@<IP>
```
