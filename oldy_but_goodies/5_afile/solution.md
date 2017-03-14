## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution
We're given a large textfile. 

If we look at it, it follows Base64 standards. Take a look at [100 - Mission Possible](https://github.com/miketweaver/bsidesslc-hacker-challenges-2017/blob/master/crypto_in_the_house/100_mission_possible/solution.md#solution) to tell how you can recognize Base 64.

```
$ head -c 50 afile.txt
Vm0wd2QyUXlVWGxWV0d4V1YwZDRWMVl3WkRSV01WbDNXa1JTVj
```

Let's decode that:
```
$ cat afile.txt | base64 -D | head -c 100
Vm0wd2QyUXlVWGxWV0d4V1YwZDRWMVl3WkRSV01WbDNXa1JTVjAxV2JETlhhMUpUVmpBeFYySkVUbGhoTVVwVVZtcEJlRll5U2tW
...
...
c2NsZHVaRmhTYkd3MVdUTndWMVl5U2xaV2FsSldUVzVTVUZac1ZYaFdiRnBWVm14YVUyRXhWVEZXVlZwR1QxWkNVbEJVTUQwPQ==
```

Ok. It's another base64. If you keep decoding it's a ton of base64 strings. We could be at this for a long while. Let's script this.
_Note_: my code isn't the best, but it works.
```
#!/usr/bin/env python
import os
import sys
import base64

f = open("afile.txt", "r")
content = f.read()

for x in range(0,int(sys.argv[1])):
  content = base64.b64decode(content);
print(content)
```
Here's me running it. You have to guess and check the number of times to run it. Not elegant, but it works:
```
$ python decode.py 50
Wm1sc1pYTmtiM2RvWVhSaFptbHNaV1J2WlhNPQ==

$ python decode.py 55
Traceback (most recent call last):
  File "decode.py", line 11, in <module>
    content = base64.b64decode(content);
  File "/System/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/base64.py", line 76, in b64decode
    raise TypeError(msg)
TypeError: Incorrect padding

$ python decode.py 52
filesdowhatafiledoes
```
## Key
filesdowhatafiledoes
