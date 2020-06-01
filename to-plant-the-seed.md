# To Plant A Seed - Writeup
### Description
```
Did you know flags grow on trees?
Apparently if you water them a specific amount each day the tree will grow into a flag!
The tree can only grow up to a byte each day. 
I planted my seed on Fri 29 May 2020 20:00:00 GMT.
Just mix the amount of water in the list with the tree for 6 weeks and watch it grow!
```

#### water.txt
```
Watering Pattern: 150 2 103 102 192 216 52 128 9 144 10 201 209 226 22 10 80 5 102 195 23 71 77 63 111 116 219 22 113 89 187 232 198 53 146 112 119 209 64 79 236 179
```

## Cracking
- After looking at the water text, the first word that comes to my mind is `pseudorandomness`.
- As we already know that epoch time is used to seed the random module sometimes and the description has served the time to us on a platter.
- Use the time given in the description to get the epoch time using an [online converter](https://www.epochconverter.com/), which gives us `1590782400` (seed).
- Now that we have the seed and as given in the description, we have to plant it for 6 weeks everyday which makes 6x7=42 days. Basically we need to get the first 42 numbers the seed generates.

##### getsalt.py
```python
import time
import random
from random import seed

def get_salt():
    epoch = 1590782400
    seed(epoch)
    inthe = []
    for i in range(42):
        inthe.append(random.randint(0, 255))
    return inthe

print(get_salt())
```
Which gives us:
```
[245, 99, 20, 18, 175, 170, 71, 195, 93, 214, 113, 173, 225, 140, 33, 85, 54, 53, 20, 164, 36, 112, 18, 75, 95, 43, 236, 37, 31, 61, 228, 145, 246, 64, 224, 47, 4, 226, 115, 43, 159, 206]
```
And we already have the water numbers:
```
[150, 2, 103, 102, 192, 216, 52, 128, 9, 144, 10, 201, 209, 226, 22, 10, 80, 5, 102, 195, 23, 71, 77, 63, 111, 116, 219, 22, 113, 89, 187, 232, 198, 53, 146, 112, 119, 209, 64, 79, 236, 179]
```
- I wonder what we could do with these two arrays of the same length `42` HmmMmmmMMmmmMmmmMmmmm?
- I wonder what's the readily used encryption in CTF challenges?

![XOR-meme](https://i.imgur.com/R9DlBMI.png)

### Script time!
```python
water = [150, 2, 103, 102, 192, 216, 52, 128, 9, 144, 10, 201, 209, 226, 22, 10, 80, 5, 102, 195, 23, 71, 77, 63, 111, 116, 219, 22, 113, 89, 187, 232, 198, 53, 146, 112, 119, 209, 64, 79, 236, 179]

salt = [245, 99, 20, 18, 175, 170, 71, 195, 93, 214, 113, 173, 225, 140, 33, 85, 54, 53, 20, 164, 36, 112, 18, 75, 95, 43, 236, 37, 31, 61, 228, 145, 246, 64, 224, 47, 4, 226, 115, 43, 159, 206]

for i in range(42):
    print(chr(water[i-1]^salt[i-1]), end="")
```

### flag
```bash
castorsCTF{d0n7_f0rg37_t0_73nd_y0ur_s33ds}
```
