## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution

We're given this text:

`PFMUM FYEQS MTHXZ WXCMD WQIJA YIUGN LRVLS GNGVH VAFRV PTZLR YLSGN STOEF VTPUZ MGEJC YGTKJ LRVLS GNPFA`

There's no formatting, no caps, no puncuation, and they're in sets of 5. Either this is something with squares or the author has worked hard to not give anything away. This was the last challengse from [Aaron](https://twitter.com/AaronToponce) and I was surprised that he hadn't done a Vigenère cipher as he recently built [https://ciphermonkey.rocks/](https://ciphermonkey.rocks/). I decided to check that before looking at the square stuff. Thankfully I did, as it WAS a Vigenère.

Before trying to crack it, as it's a CTF, I took a few seconds to try to guess it. This tool is great for guessing as it changes the text in realtime.:

http://rumkin.com/tools/cipher/vigenere-keyed.php

I was able to guess the key `bsidesslc`:

`ONERI NGTOR ULETH EMALL ONERI NGTOF INDTH EMONE RINGT OBRIN GTHEM ALLAN DINTH EDARK NESSB INDTH EMXXX`

Nice work!

You won't always be able to solve these by guessing. If you have to solve it manually, [Aaron](https://twitter.com/AaronToponce) has a really good tool to work on this:

https://ciphermonkey.rocks/hard.html

## Key
ONE RING TO RULE THEM ALL ONE RING TO FIND THEM ONE RING TO BRING THEM ALL AND IN THE DARKNESS BIND THEM
