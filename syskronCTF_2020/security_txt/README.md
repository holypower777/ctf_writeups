# Security.txt (200 points)

## Description

The security.txt draft got updated (https://tools.ietf.org/html/draft-foudil-securitytxt-10).

Is Senork's file still up-to-date? [https://www.senork.de/.well-known/security.txt](https://github.com/holypower777/ctf_writeups/syskronCTF_2020/security_txt/security.txt)

## Solution

By clicking on the second link, we see a link to the OpenPGP key. We open it and see the key in the base64:

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

mDMEX1IeNRYJKwYBBAHaRw8BAQdAGkGzrffXJoSEuPxIZ+ADdMAH1COdISkwrmFC
ZyCWGP+0X0JCIEluZHVzdHJ5IGEucy4gUFNJUlQgKHN5c2tyb25DVEZ7V2gwLXB1
dDMtZmxhZzMtMW50by0wcGVuUEdQLWtleTM/Pz99KSA8cHNpcnRAYmItaW5kdXN0
cnkuY3o+iJYEExYIAD4WIQQb0Dqaer1Y3W4NxowpcUAVAB/owgUCX1IeNQIbAwUJ
AE8aAAULCQgHAgYVCgkICwIEFgIDAQIeAQIXgAAKCRApcUAVAB/owkYsAP9uMtdg
0YInW+JgxdZbGhP7dQS7Bv1fKARx2GDcVUt7BAD/cgkM1BSC3jT1PuutPA7HDwC7
709QGbka8o/G1t9EBwE=
=mLiy
-----END PGP PUBLIC KEY BLOCK-----
```

We decode from base64 and get the flag:

```
3_R5	+ÚG@A³­÷×&¸üHgàtÀÔ#!)0®aBg ÿ´_BB Industry a.s. PSIRT (syskronCTF{Wh0-put3-flag3-1nto-0penPGP-key3???}) <psirt@bb-industry.cz>>!Ð:z½XÝn
Æ)q@èÂ_R5	O	
	
	)q@èÂF,ÿn2×`Ñ'[â`ÅÖ[ûu»ý_(qØ`ÜUK{ÿr	ÔÞ4õ>ë­<Ç»ïOP¹òÆÖßD
```

Flag: syskronCTF{Wh0-put3-flag3-1nto-0penPGP-key3???}