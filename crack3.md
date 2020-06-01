# Password Crack 3 - Writeup
### Description
```
7adebe1e15c37e23ab25c40a317b76547a75ad84bf57b378520fd59b66dd9e12
```

## Cracking

- Trying to solve this with hashcat does not work because this time the word is already wrapped with `castorsCTF{...}` already and probably the word which is wrapped is from the same wordlist (`rockyou.txt`)
- Writing a script using `hashlib` in python seems like the way to go here because we'll be able to use `hashlib` to encrypt word from the `rockyou.txt` already wrapped with `castorsCTF{...}`.


### Getting the flag
#### Script

```python
import hashlib
f = open('rockyou.txt', 'r', encoding='utf-8', errors='ignore') # Open file on read mode
lines = f.read().splitlines()
for i in lines:
    i = "castorsCTF{"+i+"}"
    i = i.encode('utf-8')
    encrypted = hashlib.sha256(i).hexdigest()
    if(encrypted=="7adebe1e15c37e23ab25c40a317b76547a75ad84bf57b378520fd59b66dd9e12"):
        print(i.decode('utf-8'))
        break
```
- Running the script will give the flag as using this because here we've wrapped all the words in `rockyou.txt` with the flag format already.
#### flag: `castorsCTF{theformat!}`

