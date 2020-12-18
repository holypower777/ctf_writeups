# Biggest Lowest (50 points)

## Description

I see you're eager to prove yourself, why not try your luck with this problem?

Target: nc challs.xmas.htsp.ro 6051

Authors: Gabies, Nutu

## Solution

```shell
$ nc challs.xmas.htsp.ro 6051
So you think you have what it takes to be a good programmer?
Then solve this super hardcore task:
Given an array print the first k1 smallest elements of the array in increasing order and then the first k2 elements of the array in decreasing order.
You have 50 tests that you'll gave to answer in maximum 30 seconds, GO!
Here's an example of the format in which a response should be provided:
1, 2, 3; 10, 9, 8

Test number: 1/50
array = [3, 6, 2, 6, 6]
k1 = 3
k2 = 1
```

A very simple task. It is necessary to write a script, I used python and the pwntools library for connection. (I'm not good at python, so the code is garbage)

```python
from pwn import *

conn = remote('challs.xmas.htsp.ro', 6051)

for x in range (50):
    conn.recvuntil("array = ")
    arr = conn.recvline().decode("utf-8") 
    conn.recvuntil("k1 = ")
    k1 = conn.recvline().decode("utf-8") 
    conn.recvuntil("k2 = ")
    k2 = conn.recvline().decode("utf-8") 

    newArr = [int(i) for i in arr[1:-2].split(', ')]
    sortedArr = sorted(newArr)
    newArr.sort(reverse = True)
    str1 = ', '.join(str(e) for e in sortedArr[:int(k1)])
    str2 = ', '.join(str(e) for e in newArr[:int(k2)])
    payload = str1 + "; " + str2
    conn.sendline(payload)

conn.interactive()
```

```shell
[*] Switching to interactive mode
Good, that's right!
Those are some was lightning quick reflexes you've got there!
 Here's your flag: X-MAS{th15_i5_4_h34p_pr0bl3m_bu7_17'5_n0t_4_pwn_ch41l}
[*] Got EOF while reading in interactive
```

Flag: X-MAS{th15_i5_4_h34p_pr0bl3m_bu7_17'5_n0t_4_pwn_ch41l}