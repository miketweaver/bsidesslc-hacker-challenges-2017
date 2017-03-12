## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution
We're given a base64 text, just like [100 - Mission Impossible](/crypto_in_the_house/100_mission_possible/solution.md). Let's use the same techniques as before.

```
$ echo -n "iVBORw0KGgoAAAANSUhEUgAAAV4AAAFeAQAAAADlUEq3AAAABGdBTUEAALGPC/xhBQAAAAJiS0dE \
AAHdihOkAAAAB3RJTUUH4QMHFw46il1hJwAAAb1JREFUaN7t10FOxTAMBNDcxPe/lQ+CFGg946Qt \
SJ/E3U0RH7V5ZYETe2j98+urCQsLCwsLC7+GvZ2Xdbfjzs7v46HlinAFtvj0y+rPvXFFuAb7UYCz \
EChLPBorwoXY4yP2etwIv4Bjw7Mm1oWrcR9NJd/JH124CKOD+/Pr7wkr/G88X9j06DnzivAu9paB \
zyL7WbzEOgmX4M6ZmVVgP49XrptfeBlfdj1nZTN08V9OivAKxrMsC2I3J+it8wuv4ljC3MTqVCMc \
CeFdjPk4T0q+ivkpXIFzcWbs5nwuvI29sZ1w02eTeQ5N4WXcsfHzIPAuAqA/Kyi8gv0aQwLMqVu4 \
BEdNop/HrDQkQRwKE67A50JuduSTnKCsl/A2biOb2MgqjIC3JiO8jm0E7JYQMeXekYSX8fy3z9jn \
3P5+TTLC69hJpxDIBnNPjMLrmCfAuO0thub4l0Z4H/OaS4MImCUR3sfxx4+ewrrwSCCtCFdgw2da \
FARFiXXhfRyPUAAMSTQZ4y8TLsPN+ngtEopllxEuw+fyiH0+krZwCR5LGVA62w7zifA2HkOTR8Cy \
OplYhHfxZ5ewsLCwsLDwK/gbEmli3BCRr6MAAAAldEVYdGRhdGU6Y3JlYXRlADIwMTctMDMtMDdU \
MjM6MTU6MDItMDc6MDDmHWk5AAAAJXRFWHRkYXRlOm1vZGlmeQAyMDE3LTAzLTA3VDIzOjE0OjU4 \
LTA3OjAwlBLrkQAAAABJRU5ErkJggg==" | base64 -D > binary

$ xxd binary
00000000: 8950 4e47 0d0a 1a0a 0000 000d 4948 4452  .PNG........IHDR
00000010: 0000 015e 0000 015e 0100 0000 00e5 504a  ...^...^......PJ
00000020: b700 0000 0467 414d 4100 00b1 8f0b fc61  .....gAMA......a
00000030: 0500 0000 0262 4b47 4400 01dd 8a13 a400  .....bKGD.......
00000040: 0000 0774 494d 4507 e103 0717 0e3a 8a5d  ...tIME......:.]
00000050: 6127 0000 01bd 4944 4154 68de edd7 414e  a'....IDATh...AN
00000060: c530 0c04 d0dc c4f7 bf95 0f82 1468 3de3  .0...........h=.
00000070: a42d 489f c4dd 4d11 1fb5 7965 8113 7b68  .-H...M...ye..{h
00000080: fdf3 ebab 090b 0b0b 0b0b 0bbf 86bd 9d97  ................
00000090: 75b7 e3ce ceef e3a1 e58a 7005 b6f8 f4cb  u.........p.....
000000a0: eacf bd71 45b8 06fb 5180 b310 284b 3c1a  ...qE...Q...(K<.
000000b0: 2bc2 85d8 e323 f67a dc08 bf80 63c3 b326  +....#.z....c..&
000000c0: d685 ab71 1f4d 25df c91f 5db8 08a3 83fb  ...q.M%...].....
000000d0: f3eb ef09 2bfc 6f3c 5fd8 f4e8 39f3 8af0  ....+.o<_...9...
000000e0: 2ef6 9681 cf22 fb59 bcc4 3a09 97e0 ce99  .....".Y..:.....
000000f0: 9955 603f 8f57 ae9b 5f78 195f 763d 6765  .U`?.W.._x._v=ge
00000100: 3374 f15f 4e8a f00a c6b3 2c0b 6237 27e8  3t._N.....,.b7'.
00000110: adf3 0baf e258 c2dc c4ea 5423 1c09 e15d  .....X....T#...]
00000120: 8cf9 384f 4abe 8af9 295c 8173 7166 ece6  ..8OJ...)\.sqf..
00000130: 7c2e bc8d bdb1 9d70 d367 9379 0e4d e165  |......p.g.y.M.e
00000140: dcb1 f1f3 20f0 2e02 a03f 2b28 bc82 fd1a  .... ....?+(....
00000150: 4302 cca9 5bb8 0447 4da2 9fc7 ac34 2441  C...[..GM....4$A
00000160: 1c0a 13ae c0e7 426e 76e4 939c a0ac 97f0  ......Bnv.......
00000170: 366e 239b d8c8 2a8c 80b7 2623 bc8e 6d04  6n#...*...&#..m.
00000180: ec96 1031 e5de 9184 97f1 fcb7 cfd8 e7dc  ...1............
00000190: fe7e 4d32 c2eb d849 a710 c806 734f 8cc2  .~M2...I....sO..
000001a0: eb98 27c0 b8ed 2d86 e6f8 9746 781f f39a  ..'...-....Fx...
000001b0: 4b83 0898 2511 dec7 f1c7 8f9e c2ba f048  K...%..........H
000001c0: 20ad 0857 60c3 675a 1404 4589 75e1 7d1c   ..W`.gZ..E.u.}.
000001d0: 8f50 000c 4934 19e3 2f13 2ec3 cdfa 782d  .P..I4../.....x-
000001e0: 128a 6597 112e c3e7 f288 7d3e 92b6 7009  ..e.......}>..p.
000001f0: 1e4b 1950 3adb 0ef3 89f0 361e 4393 47c0  .K.P:.....6.C.G.
00000200: b23a 9958 8477 f167 97b0 b0b0 b0b0 b0f0  .:.X.w.g........
00000210: 2bf8 1b12 6962 dc10 91af a300 0000 2574  +...ib........%t
00000220: 4558 7464 6174 653a 6372 6561 7465 0032  EXtdate:create.2
00000230: 3031 372d 3033 2d30 3754 3233 3a31 353a  017-03-07T23:15:
00000240: 3032 2d30 373a 3030 e61d 6939 0000 0025  02-07:00..i9...%
00000250: 7445 5874 6461 7465 3a6d 6f64 6966 7900  tEXtdate:modify.
00000260: 3230 3137 2d30 332d 3037 5432 333a 3134  2017-03-07T23:14
00000270: 3a35 382d 3037 3a30 3094 12eb 9100 0000  :58-07:00.......
00000280: 0049 454e 44ae 4260 82                   .IEND.B`.

$ file binary
binary: PNG image data, 350 x 350, 1-bit grayscale, non-interlaced
```

Perfect! It's a png. Let's look at it:

`$ mv binary binary.png`

![binary.png](solution-files/binary.png)

And scan that with a qr decoder:

`Hvs Rccfg ct Rifwb, Zcfr ct Acfwo. Gdsoy, tfwsbr, obr sbhsf.`

Cool! Some text. Let's try some common ciphers, ceaser being the first:

http://www.xarg.org/tools/caesar-cipher/

If you use the 'guess' feature, it tells you to use key `12` and give you the answer:

`The Doors of Durin, Lord of Moria. Speak, friend, and enter.`

Sweet!

## Key
The Doors of Durin, Lord of Moria. Speak, friend, and enter.
