# Password Crack 1 - Writeup
### Description
```
3c80b091de0981ec64e43262117d618a
Wrap the result with castrosCTF{...}
```

## Cracking

- This looks like a md5 hash to me
- As we know that hashes are one way so there's not much that we can do other than using a wordlist and guessing it.
- There's a tool to crack hashes called [`hashcat`](https://hashcat.net/hashcat/) which can be used to crack hashes using a widely used wordlist named as `rockyou.txt`

#### Using hashcat to crack this

```
 hashcat -m 0 "3c80b091de0981ec64e43262117d618a" rockyou.txt --force
```

#### Getting the flag
```
3c80b091de0981ec64e43262117d618a:irocktoo
```
#### flag: `castorsCTF{irocktoo}`



