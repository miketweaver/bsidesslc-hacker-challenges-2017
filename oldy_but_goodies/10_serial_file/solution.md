## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution

We're given this really long text file (I cut parts out):
```
00000000: 3a31 3030 3030 3030 3030 4339 3435 4430  :100000000C945D0
00000010: 3030 4339 3438 3530 3030 4339 3438 3530  00C9485000C94850
00000020: 3030 4339 3438 3530 3038 340d 0a3a 3130  00C94850084..:10
00000030: 3030 3130 3030 3043 3934 3835 3030 3043  0010000C9485000C
00000040: 3934 3835 3030 3043 3934 3835 3030 3043  9485000C9485000C
00000050: 3934 3835 3030 3443 0d0a 3a31 3030 3032  9485004C..:10002
...
...
00001530: 3030 3734 3333 3432 3739 3432 3739 3734  0074334279427974
00001540: 3333 3030 3044 3041 3030 3930 0d0a 3a30  33000D0A0090..:0
00001550: 3030 3030 3030 3146 460d 0a              0000001FF..
```

This is a hexdump. Let's turn this hexdump into a binary file using `xxd`.

```
$ cat load_em_up.txt | xxd -r > part2

$ file part2
part2: ASCII text, with CRLF line terminators

$ cat part2
:100000000C945D000C9485000C9485000C94850084
:100010000C9485000C9485000C9485000C9485004C
:100020000C9485000C9485000C9485000C9485003C
..
..
:10076200000000005301CF001C01FA000E019A01A3
:10077200466C61673A20423174427942317442795F
:0C0782007433427942797433000D0A0090
:00000001FF
```

What we have above there is another hexdump. I've seen this before in the [Saintcon 2016 CTF](https://github.com/SocialGeeks/hackerschallenge2016/blob/master/bl/300/walkthrough-bashninja.md). 
I'm going to quote it:
>I was stuck on this for a bit until I started googling it. I began by googling the bottom half, as it looked different then the rest.
>Using this [google search](https://www.google.com/search?q=%3A00000001FF), I was able to determine it was in **INTEL HEX** format.

I've found we can install the tools on a Mac:
```
$ brew tap osx-cross/avr
$ brew install avr-binutils
```
Here's the tools for Kali:

`apt install binutils-avr`

Cool. Let's take this HEX and turn it into a binary, then look at the binary.

```
$ avr-objcopy -I ihex -O binary part2 part3

$ file part3
part3: data

$ strings part3
Flag: B1tByB1tByt3ByByt3
```

Like Magic.

## Key
B1tByB1tByt3ByByt3
