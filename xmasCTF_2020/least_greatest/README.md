# Least Greatest (500 points)

## Description

Today in Santa's course in Introduction to Algorithms, Santa told us about the greatest common divisor and the least common multiple.
He this gave the following problem as homework and I don't know how to solve it.
Can you please help me with it?

Target: nc challs.xmas.htsp.ro 6050

Authors: Gabies, Nutu

## Solution

```shell
$ nc challs.xmas.htsp.ro 6050
Hey, you there! You look like you know your way with complex alogrithms.
There's this weird task that I can't get my head around. It goes something like this:
Given two numbers g and l, tell me how many pairs of numbers (x, y) exist such that gcd(x, y) = g and lcm(x, y) = l
Also, i have to answer 100 such questions in at most 90 seconds.

Test number: 1/100
gcd(x, y) = 87641
lcm(x, y) = 750862998151937487679256930365054379979841
```

I found a ready-made function for the same task: [link](https://www.geeksforgeeks.org/given-gcd-g-lcm-l-find-number-possible-pairs-b/). But this code gave errors on 3-4 tests. It was only necessary to add a second slash to divide large integers. Here is the finished code:

```python
from pwn import *

conn = remote('challs.xmas.htsp.ro', 6050)

def totalPrimeFactors(n):  
    count = 0;  

    if ((n % 2) == 0):  
        count += 1;  
        while ((n % 2) == 0):  
            n //= 2;  
  
    i = 3; 
    while (i * i <= n):  
        if ((n % i) == 0):  
            count += 1;  
            while ((n % i) == 0):  
                n //= i;  
        i += 2; 

    if (n > 2):  
        count += 1;  
  
    return count;  
  
def countPairs(G, L):  
    if (L % G != 0):  
        return 0;  
  
    div = int(L // G);  

    return (1 << totalPrimeFactors(div)); 

conn.recvuntil("Test number")

for x in range (100):
    conn.recvuntil("gcd(x, y) = ")
    g = conn.recvline()
    conn.recvuntil("lcm(x, y) = ")
    l = conn.recvline()

    payload = countPairs(int(g), int(l))
    conn.sendline(str(int(payload)))
    print(x+1, conn.recvline().decode("utf-8"))

conn.interactive()
```

```shell
[*] Switching to interactive mode
Wow, you really know this kind of weird math?
Here's your flag: X-MAS{gr347es7_c0mm0n_d1v1s0r_4nd_l345t_c0mmon_mult1pl3_4r3_1n73rc0nn3ct3d}
[*] Got EOF while reading in interactive
```

Flag: X-MAS{gr347es7_c0mm0n_d1v1s0r_4nd_l345t_c0mmon_mult1pl3_4r3_1n73rc0nn3ct3d}