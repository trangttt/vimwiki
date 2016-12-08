* `ssh-keygen` : generate pub and private keys
* `ssh-agent <shell>` : start ssh-agent spawing shell
* `ssh-add <priv_key>` : add private key to repository
* `cat <pub_key> | ssh user@hostname 'cat <pub_key> >> ~/.ssh/authorized_keys'`  or `ssh-copy-id [-i id ] user@hostname`
* `known_hosts` : files to store known public key(meaning known websites)
* `ssh -oStrictHostChecking=no` : No checking new hostkey
