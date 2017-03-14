## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution

Ok.  We're given this file, let's take a look at it. (take a look at [200 - Reverse Me](https://github.com/miketweaver/bsidesslc-hacker-challenges-2017/blob/master/reversing_required/200_reverse_me/solution.md#solution) for info on how `file` works.)
```
$ file party.lst
party.lst: ASCII text
```

Sweet it's an ascii file. Let's look at that:

```
$ cat party.lst
00000000: f01f 0010 c500 0000 dd0b 0000 c100 0000  ................
00000010: c100 0000 c100 0000 c100 0000 6ad0 ffef  ............j...
00000020: 0000 0000 0000 0000 0000 0000 c100 0000  ................
00000030: c100 0000 0000 0000 c100 0000 012d 0000  .............-..
00000040: c503 0000 3d04 0000 b504 0000 2d05 0000  ....=.......-...
..
..
0000ffb0: ffff ffff ffff ffff ffff ffff ffff ffff  ................
0000ffc0: ffff ffff ffff ffff ffff ffff ffff ffff  ................
0000ffd0: ffff ffff ffff ffff ffff ffff ffff ffff  ................
0000ffe0: ffff ffff ffff ffff ffff ffff ffff ffff  ................
0000fff0: ffff ffff ffff ffff ffff ffff ffff ffff  ................
```
Alright it's a hexdump of a binary. Let's use `xxd` to turn it into a binary, and then look at it.

```
$ cat party.lst | xxd -r > binary

$ file binary
binary: SysEx File - Clarity
```

At this point I did a lot of research on SysEx and got stuck. I loaded it up in SysEx Librarian on my Mac and didn't find anything. I didn't get past this part during the CTF, but later I've been able to progress.

I eventually ran strings on it to take a look at the binary:
```
$ strings binary
LK[j
!4KZj
%?J?K
...
...
...

( zt
$|a>v
0 zv
?h7p
C'bN
CF;F
Q03h
5h25
5556
4134
4d44
4646
5533
6c75
6444
6f67
4d48
4234
5a67
3d3d
battery:
.: @gr3yR0n1n :.
```

You'll see that intersting bit? It didn't appear in SysEx Librarian. Neither did any of that... Hexlike text? Awesome! Let's look at that.

Dump:
```
5556
4134
4d44
4646
5533
6c75
6444
6f67
4d48
4234
5a67
3d3d
```
into https://asciitohex.com (drop `5h25` because it's not valid hex)and you get: 

`UVA4MDFFU3ludDogMHB4Zg==`

That's Base64! (Check out [100 - Mission Possible](https://github.com/miketweaver/bsidesslc-hacker-challenges-2017/blob/master/crypto_in_the_house/100_mission_possible/solution.md#solution) if you can't recognize Base64)

Cool. Throw that into my crypto page [quickcrypto.io](https://quickcrypto.io) and you'll see it decodes from Base64 -> ASCII -> RO13:
`DC801RFlag: 0cks`

It's a bit out of order, let's fix that:

`Flag: DC801R0cks` 

Nice.

## Key
DC801R0cks
