# Password Crack 2 - Writeup
### Description
```
867c9e11faa64d7a5257a56c415a42725e17aa6d
You might need this: 653589
Wrap the result with castorsCTF{...}
```

## Cracking

- This looks like a md5 hash to me but with a salt
- As we know that hashes are one way so there's not much that we can do other than using a wordlist and guessing it.
- There's a tool to crack hashes called [`hashcat`](https://hashcat.net/hashcat/) which can be used to crack hashes using a widely used wordlist named as `rockyou.txt`

#### Using hashcat to crack this

```
hashcat -m 160 "867c9e11faa64d7a5257a56c415a42725e17aa6d:653589" rockyou.txt --force
```

#### Getting the flag
```
867c9e11faa64d7a5257a56c415a42725e17aa6d:653589:pi3141592
```

- Now it seems that `pi3141592` should be the flag here but no, what you get after putting the salt with hash in `hashcat` is the password but the whole hash is `$password.$salt`, which makes it `pi3141592653589`
#### flag: `castorsCTF{pi3141592653589}`


