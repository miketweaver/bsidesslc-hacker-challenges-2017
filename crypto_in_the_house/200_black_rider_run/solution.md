## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution

So I'm a little ashamed of the way I solved this, and I'll share the 'correct' way at the end of my solution, but it's good to knwo about the tools available during a CTF.

We were given:

```
GBTVT XZ AIBBSXCP CT TBVXCIBS QBXCUNQ XC MXZ WTAUNQ. MN PTQ XCQT I QOZZEN FXQM ZTRN TG QMN WIQBTCZ, QMNC VXZIWWNIBNV IGQNB GIEEXCP TC QMN GETTB. ZNNRZ QT MIDN VBIFC IQQNCQXTC. BOCCXCP.
```

I spend almost 20 minutes piling through various ciphers/keys and never got anywhere. By looking at it, it looks like a substution cipher as it keeps its formatting with commas and periods.

At this point I decided to through it through an automated tool:
http://quipqiup.com/

That's better:
`	FRODO IS CARRYING NO ORDINARY TRIN?ET IN HIS POC?ET. HE GOT INTO A TUSSLE WITH SOME OF THE PATRONS, THEN DISAPPEARED AFTER FALLING ON THE FLOOR. SEEMS TO HAVE DRAWN ATTENTION. RUNNING`

It looks like it missed the letter K, which we can guess from the words. Add that in, and we've got it!

## Better Solution

After talking with [Aaron](https://twitter.com/AaronToponce) after the competition, we discussed the best way to solve this is frequency analysis. (Hency why quipqiup worked so well) Frequency analysis is basically counting the number of occurances of a letter (or sets of letters). 
The tool I used for single character analysis was:
http://www.simonsingh.net/The_Black_Chamber/letterfrequencies.html

![solutionfile-frequency.gif](/crypto_in_the_house/200_black_rider_run/solutionfile-frequency.gif)

Now this looks pretty evenly spread. There are a few spikes, 

## Key
FRODO IS CARRYING NO ORDINARY TRINKET IN HIS POCKET. HE GOT INTO A TUSSLE WITH SOME OF THE PATRONS, THEN DISAPPEARED AFTER FALLING ON THE FLOOR. SEEMS TO HAVE DRAWN ATTENTION. RUNNING
