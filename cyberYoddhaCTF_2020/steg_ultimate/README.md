# Steg Ultimate (450 points)

## Description

You reached the final stage, can you unravel your way out of this one?

[Attached image](stegultimate.jpg)

## Solution

Having tried all the standard steganography utilities, such as binwalk, strings, pngcheck, zsteg, I decided to try steghide without passphrase.

```shell
$ steghide extract -sf stegultimate.jpg
Enter passphrase:
wrote extracted data to "steg3.jpg".
```

Success! After another round of standard utilities, I came back to steghide.

```shell
$ steghide extract -sf steg3.jpg
Enter passphrase:
wrote extracted data to "steganopayload473955.txt".
```

```shell
$ cat steganopayload473955.txt
https://pastebin.com/YnKqT9s3
```

Huge string. Let's just paste it into [CyberChef](http://icyberchef.com/)
The first thing I see is that it is a png format. The recipe we need is **Render Image** input format: Raw. It outputs image with the flag.

Flag: CYCTF{2_f0r_th3_pr1c3_0f_1_b64}