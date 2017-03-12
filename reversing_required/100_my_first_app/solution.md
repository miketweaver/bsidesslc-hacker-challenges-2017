## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution
So we're given this file `MyFirstApp`. Let's figure out what it is.

```
$ file MyFirstApp
MyFirstApp: Mach-O 64-bit executable x86_64
```
Awesome it's a [Mach-O](https://en.wikipedia.org/wiki/Mach-O) executable. Most commonly used by MacOS. Ok. Before we run it, let's see if there's anything is plaintext within the binary.

```
$ strings MyFirstApp
Flag: Not bad for your first reverse
```

... yup. There was something in plaintext. The flag.

## Key
Not bad for your first reverse
