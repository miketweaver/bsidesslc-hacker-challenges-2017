## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution
Awesome they give us this file `naes`. Ok, let's do the same checking as before:

```
$ file naes
naes: data

 $ xxd naes | head
00000000: 0d0a 1a0a 0000 000d 4948 4452 0000 019f  ........IHDR....
00000010: 0000 0117 0802 0000 00fd 63de 7600 0000  ..........c.v...
00000020: 0173 5247 4200 aece 1ce9 0000 4000 4944  .sRGB.......@.ID
00000030: 4154 7801 e4bd d9af 6449 72e6 7763 8fb8  ATx.....dIr.wc..
00000040: 6bee 4b2d cdaa ea6a 768b 1a0d 4614 4081  k.K-...jv...F.@.
00000050: 7aa0 0891 0350 2020 5098 87f9 c704 0890  z....P  P.......
00000060: a027 41f3 2e40 8246 33a0 4012 230c 879c  .'A..@.F3.@.#...
00000070: a1c4 2139 147b 2976 57b1 d6ac 5cee 7e6f  ..!9.{)vW...\.~o
00000080: acfa 7df6 9d63 e1f7 44c4 cdcc eacc ea62  ..}..c..D......b
00000090: b7e7 4d0f 7373 7373 7373 773b e67e fc9c  ..M.ssssssw;.~..
...
...
000252d0: 4d59 9f39 87cf 1716 967c f8cf 51aa 2ce0  MY.9.....|..Q.,.
000252e0: b838 b496 08d2 b7e1 4674 631d e087 0a33  .8......Ftc....3
000252f0: c897 6191 09d2 a9e3 fd99 93ec c7cf 826a  ..a............j
00025300: 96b2 53f5 d4a8 24aa 8353 a229 1f85 aa66  ..S...$..S.)...f
00025310: 1976 a574 1a4f 6090 69ab 4af3 76e0 707b  .v.t.O`.i.J.v.p{
00025320: b092 876b 5624 61f9 2bf7 8a78 f9d1 e19e  ...kV$a.+..x....
00025330: a71d 10af 0dd8 18f8 db33 840f 210d 763a  .........3..!.v:
00025340: bc43 5e7d 3649 2083 aad6 30db 4f63 0fc9  .C^}6I ...0.Oc..
00025350: c71e 2dae 8d03 fa0b 4f54 bb83 74be bca6  ..-.....OT..t...
00025360: 0a0c 25fd 69ec d930 24aa 080b ceb2 d642  ..%.i..0$......B
00025370: f6ff 0f43 c352 f2b4 d94e c000 0000 0049  ...C.R...N.....I
00025380: 454e 44ae 4260 82                        END.B`.
```

Ok. File isn't picking it up again, but there is data here. We'v got to figure it out.

There's a few things that stand out in the Hexdump:

`IHDR sRGB IDAT END.B`

Let's do a [search](http://lmgtfy.com/?q=IHDR) for `IHDR`.

That comes up with a PNG file. Ok. Let's take a look at a 'good' PNG file and compare the beginnings. 

```
$ wget -q https://upload.wikimedia.org/wikipedia/commons/4/47/PNG_transparency_demonstration_1.png

$ xxd PNG_transparency_demonstration_1.png | head -n 2
00000000: 8950 4e47 0d0a 1a0a 0000 000d 4948 4452  .PNG........IHDR
00000010: 0000 0320 0000 0258 0806 0000 009a 7682  ... ...X......v.

$ xxd naes | head -n 2
00000000: 0d0a 1a0a 0000 000d 4948 4452 0000 019f  ........IHDR....
00000010: 0000 0117 0802 0000 00fd 63de 7600 0000  ..........c.v...
```

Perfect. That's the same as [200 - Reverse Me](reversing_required/200_reverse_me/challenge.md). Let's fix it.

Add `89504e47` to the beginning of the binary file using your hex editor. After that's done, let's look at it.

```
$ file naes
naes: PNG image data, 415 x 279, 8-bit/color RGB, non-interlaced

$ mv naes naes.png
```

Looks good! Now take a look at it:

![solution.png](solution-files/solution.png)

Ok. That's weird. Very flattering picture, but...

What do we enter in as the key? 

The title of the challenge is: `Who's got a handle on this?`, and the filename is `sean` backwards. So maybe [Sean Jackson's](https://twitter.com/74rku5) handle `74rku5`?

Yes!

## Key
74rku5
