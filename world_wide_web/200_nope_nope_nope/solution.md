## Author
bashNinja - [@miketweaver](https://twitter.com/miketweaver)

## Solution
```
Names are the thing. Hosts to be found.
THE LEPRAUCHAN IS NOW HIDDEN IF ONLY HE COULD BE BIDDEN TO GIVE US UP HIS GOLD AND HIS NAME SO IS THE PATH TO BIG FAME
```

Ok we're looking for a Name, and they have the word Hosts? Weird. Let's look at the page they gave us in the previous challenge.

What we saw was a page that said 'nope nope nope'. If you pull up the source code you see a comment saying they haven't setup their DNS, the domain should be `slc.punk`, and that you could add it into your hosts file. Notice the use of the word 'hosts'? This is what we're lookin for. Let's add that to our hosts file.

On a Mac:
`sudo echo -n "45.76.9.79	slc.punk" >> /etc/hosts`

If you pull up the page `http://slc.punk` it now shows a login screen. Cool! But what's the flag?

The flag is the domain name.

## Key
slc.punk
