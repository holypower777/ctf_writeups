# Many Paths (500 points)

## Description

Today in Santa's course in Advanced Graph Algorithms, Santa told us about the adjacency matrix of an undirected graph. I'm sure this last problem, he gave us is unsolvable, but I don't know much, maybe you do.

Target: nc challs.xmas.htsp.ro 6053

Authors: Gabies, Nutu

## Solution

```shell
$ nc challs.xmas.htsp.ro 6053
I swear that Santa is going crazy with those problems, this time we're really screwed!
The new problem asks us the following:
Given an undirected graph of size N by its adjacency matrix and a set of forbidden nodes, tell me how many paths from node 1 to node N of exactly length L that don't pass through any of the forbidden nodes exist (please note that a node can be visited multiple times)?
And if that wasn't enough, we need to answer 40 of those problems in 45 seconds and to give each output modulo 666013. What does that even mean!?

Test number: 1/40
N = 5
adjacency matrix:
0,1,0,0,1
1,0,0,1,1
0,0,0,0,0
0,1,0,0,1
1,1,0,1,0
forbidden nodes: [3]
L = 4
```

I found an article that solves that problem: [link](https://cp-algorithms.com/graph/fixed_length_paths.html). So I need to raise the adjacency matrix to the power of the path length and the element (source, dest) % mod gonna be the answer. I tried to use numpy matrix_power function, but for me it doesn't work properly by some unknown reasons. So, i found another function how to raise matrix to the power, here it is (i modified it a little bit to optimise by using modulo):

```python
import numpy as np

class Mat(list) :
    def __matmul__(self, B) :
        A = self
        return Mat([[sum(A[i][k]*B[k][j] for k in range(len(B)))
                    for j in range(len(B[0])) ] for i in range(len(A))])
 
 
def identity(size):
    size = range(size)
    return [[(i==j)*1 for i in size] for j in size]

def power(F, n):
    mod = 666013
    result = Mat(identity(len(F)))
    b = Mat(F)
    while n > 0:
        if (n%2) == 0:
            b = np.remainder(b @ b, mod)
            n //= 2
        else:
            result = np.remainder(b @ result, mod)
            b = np.remainder(b @ b, mod)
            n //= 2
    return np.remainder(result, mod)
```

Now that we have a working function for raising a matrix to a power, I need to parse the server responses into the required types, and also remove the forbidden nodes, if they are present, here is the code:

```python
from pwn import *

conn = remote('challs.xmas.htsp.ro', 6053)

for task in range(40):
    conn.recvuntil("N = ")
    N = int(conn.recvline().decode('utf-8'))

    conn.recvline() #skips "adjacency matrix" line

    recievedMatrix = []
    for x in range(N):
        recievedMatrix.append(conn.recvline().decode('utf-8').replace('\n', '').split(','))
    
    # parses forbidden nodes
    conn.recvuntil("forbidden nodes: ")
    forbiddenLine = conn.recvline().decode('utf-8').strip()
    forbidden = forbiddenLine[1:-1]
    forbiddenNodes = []
    if (len(forbidden) > 1):
        forbidden = forbidden.split(',')
        for x in forbidden:
            forbiddenNodes.append(int(x))
    elif (len(forbidden) == 1):
        forbiddenNodes.append(int(forbidden))

    forbiddenNodes.sort(reverse=True)

    matrix = []
    for x in range(len(recievedMatrix)):
        matrix.append([])
        for elem in range(len(recievedMatrix[x])):
            matrix[x].append(int(recievedMatrix[x][elem]))

    # remove forbidden nodes and corresponding elemetes from each node
    for x in forbiddenNodes:
        matrix.pop(x-1)
        for node in matrix:
            node.pop(x-1)

    conn.recvuntil("L = ")
    length = int(conn.recvline().decode('utf-8'))

    matrixPower = power(matrix, length)

    #format N if forbidden nodes are deleted
    if (len(forbiddenNodes)):
        N = N - len(forbiddenNodes)

    
    payload = matrixPower[0][N - 1]

    conn.sendline(str(payload))
    print("Current task: ", task)
conn.interactive()
```

```shell
[*] Switching to interactive mode
I cannot believe you figured this one out, how does this code even work?
I'm baffled, here's the flag: X-MAS{n0b0dy_3xp3c73d_th3_m47r1x_3xp0n3n71a7i0n}
[*] Got EOF while reading in interactive
```

Flag: X-MAS{n0b0dy_3xp3c73d_th3_m47r1x_3xp0n3n71a7i0n}

