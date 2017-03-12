## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution
So we're given this weird text file.
[message.txt](files/message.txt)

There's a lot of weird wording in it, and these weird symbols. 

I started googling sections and this one came up with some useful stuff:

[Search:](http://lmgtfy.com/?q=.%3C%2B%2B.-.%3E) .<++.-.>

Particurarly this link which referenced it as a programming language:

www.99-bottles-of-beer.net/download/1718

Ok! Cool, I guess this is a programming language. Oh yes! This was at the SaintCon 2016 CTF. 

Stick the code into [this](https://copy.sh/brainfuck/) editor & interpreter, hit run and you'll get an answer.

`0045.76.9...79`

Remove the extra `0` and `.` and you get an IP Address:

`45.76.9.79`

## Key
45.76.9.79
