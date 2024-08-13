## How to use `ProxyCommand`
+ Generate SSH Key
```shell
# -t: rsa | ecdsa | ecdsa-sk | ed25519 | ed25519-sk | rsa
# -b: bits
# -C: comment
$ ssh-keygen -t rsa -b 2048 -C "account_name"
```
+ Copy public key to remote server
```shell
$ ssh-copy-id -i ~/.ssh/ssh_key.pub account@remote_host
```
+ `~/.ssh/config`
```shell

```shell
Host github.com
    HostName github.com
    User git
    Port 22
    # Private key
    IdentityFile ~/.ssh/ssh_key
    IdentitiesOnly yes
    # ForwardXll:  run graphical application on a remote server and display them on local machine
    # ForwardAgent: SSH agent forwarding
    ForwardAgent yes
    # ProxyCommand nc -X Connect -x ip:port -P account %h %p
    ProxyCommand connect-proxy -H account:password@proxy_ip:port %h %p
```
+ connect without password
```shell
$ eval `ssh-agent`
# add private key
$ ssh-add ~/.ssh/ssh_key

$ ssh -T git@github.com
```