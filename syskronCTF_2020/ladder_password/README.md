# Ladder password (100 points)

## Description

A BB engineer encoded her password in ladder logic. Each "r" can be either 0 or 1 and represents a character in her password. "r1" is the first character, "r2" the second one, and so on. We assume that n1 is a small value and n3 is big. n2 may be between n1 and n3.

Please decode the password to demonstrate that this technique of storing passwords is insecure.

[Attached image](https://github.com/holypower777/ctf_writeups/syskronCTF_2020/ladder-password/ladder-password.png)

## Solution

Opening the picture, you can understand that the Ladder logic method is used here. The easiest way to solve this problem is to google "ladder logic online". Immediately, you can find the site https://www.plcfiddle.com/ in which we build exactly the same scheme as in the picture. Variables **b** and **r** are of type boolean, and variable **n** is digit. Having built the circuit, we look at the variables **r** and those that highlited are equal to 1

Flag: 0011100011