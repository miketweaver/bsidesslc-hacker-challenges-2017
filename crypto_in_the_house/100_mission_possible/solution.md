## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution

So we're given this exciting string:

```
H4sIAJyVv1gAAx2OQQ6DMAwE733FPgDxCF6A1F56dIMhVkOMHLsVv2/odUY72qeGYZfWROuAljXKglMDKas2hisoJT4c4gOkXWBndkxkRXaqmMKd7RU2wDNDan0zH2wg/4PZqCapG2atZ9eYjHnAnTxsoRO09jn8K0W27CMema3760NnBcaJ5cNYw3rOeqG5RfJ+eLz9AJp8Z4S/AAAA
```

Which means nothing to most of us, except if you recognize it. This is a base64 encoded string. I was able to recoginze that because base64 has a limited charset: `A–Z, a–z, 0–9, +, and /`

Base64 has lots of uses, so why not [read up](https://www.sans.org/reading-room/whitepapers/detection/base64-pwned-33759) about it a bit.

Anyways, I dumped that string into my decoder at [quickcrypto.io](https://quickcrypto.io) and it gave me this gibberish.
```
¿XA0ï}Å>ñ^Ô^zt!VC»¿oèuF;Ú§aÖDë5ÊS)«6+(%>â¤]`gvLdEvªÂí6À3Cj}3l ÿÙ¨&©f­g×yÀ<l¡´ö9ü+E¶ì#­ûëCgÆåÃXÃzÎz¡¹Eò~x¼ý|g¿
```
Useless. 

Ok now what? It's not ASCII, so let's take a look at what it decodes to in raw binary. Basically I'm `echo`-ing the base64 string, `|` piping it to `base64` to decode it, and `>` writing it to a file. Then I used some tools (`xxd and file`) to look at the binary file to see if I find anything useful. I'm doing this on a Mac, so any commands may be a tad bit different in windows/linux.

```
$ echo -n "H4sIAJyVv1gAAx2OQQ6DMAwE733FPgDxCF6A1F56dIMhVkOMHLsVv2/odUY72qeGYZfWROuAljXKglMDKas2h \
isoJT4c4gOkXWBndkxkRXaqmMKd7RU2wDNDan0zH2wg/4PZqCapG2atZ9eYjHnAnTxsoRO09jn8K0W27CMema3760NnBcaJ \
5cNYw3rOeqG5RfJ+eLz9AJp8Z4S/AAAA" | base64 -D > binary

$ xxd binary
00000000: 1f8b 0800 9c95 bf58 0003 1d8e 410e 8330  .......X....A..0
00000010: 0c04 ef7d c53e 00f1 085e 80d4 5e7a 7483  ...}.>...^..^zt.
00000020: 2156 438c 1cbb 15bf 6fe8 7546 3bda a786  !VC.....o.uF;...
00000030: 6197 d644 eb80 9635 ca82 5303 29ab 3686  a..D...5..S.).6.
00000040: 2b28 253e 1ce2 03a4 5d60 6776 4c64 4576  +(%>....]`gvLdEv
00000050: aa98 c29d ed15 36c0 3343 6a7d 331f 6c20  ......6.3Cj}3.l
00000060: ff83 d9a8 26a9 1b66 ad67 d798 8c79 c09d  ....&..f.g...y..
00000070: 3c6c a113 b4f6 39fc 2b45 b6ec 231e 99ad  <l....9.+E..#...
00000080: fbeb 4367 05c6 89e5 c358 c37a ce7a a1b9  ..Cg.....X.z.z..
00000090: 45f2 7e78 bcfd 009a 7c67 84bf 0000 00    E.~x....|g.....

$ file binary
binary: gzip compressed data, last modified: Wed Mar  8 05:24:44 2017, from Unix
```

Bingo! It's a gzip file. That's easy to fix.

```
$ mv binary binary.gz
$ gzip -d binary.gz
$ cat binary
Your mission, should you choose to accept it, is to meet Barliman Butterbur, the innkeeper at the Prancing Pony in Bree, Saturday after twilight. There, you will receive further instruction.
```

Submit that, and you've solved it.

## Key
Your mission, should you choose to accept it, is to meet Barliman Butterbur, the innkeeper at the Prancing Pony in Bree, Saturday after twilight. There, you will receive further instruction.
