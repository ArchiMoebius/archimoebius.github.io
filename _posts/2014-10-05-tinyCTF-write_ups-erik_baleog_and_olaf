---
layout: post
title: TinyCTF - erik-baleog-and-olaf
categories:
- CTF
tags: [ctf]
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---

Content found at: [Tiny CTF 2014 write-ups](https://github.com/ctfs/write-ups/tree/master/tinyctf-2014/erik-baleog-and-olaf "TinyCTF 2014 write-ups")

Extract the provided [stego100.zip](https://github.com/ctfs/write-ups/raw/master/tinyctf-2014/erik-baleog-and-olaf/stego100.zip) file:

```bash
$ unzip stego100.zip
Archive:  stego100.zip
  inflating: stego100
```

Well, what is this?

```bash
$ file stego100
stego100: PNG image data, 640 x 480, 8-bit/color RGB, non-interlaced
```

Looks like it's a PNG image, hmmm... *looks at image*, not much here?...Let's see what else is in there:

```bash
$ strings stego100 | tail
`ML|w
{>+_O
l^$V
+{>6#4
-AQA
~?:,
LdfO;
#tEXthint
http://i.imgur.com/22kUrzm.png
IEND
```

Well look at that, a URL...*visits URL*...it's the same image... or is it!?

[That hint URL](https://i.imgur.com/22kUrzm.png) is [another image](https://raw.githubusercontent.com/ctfs/write-ups/master/tinyctf-2014/erik-baleog-and-olaf/hint.png) that looks the same:

![](https://raw.githubusercontent.com/ctfs/write-ups/master/tinyctf-2014/erik-baleog-and-olaf/hint.png)

```bash
$ diff stego100 22kUrzm.png
Binary files stego100 and 22kUrzm.png differ
```

Ah ha! So something is going on, let's write a script and see if we can find out what.

{% highlight python linenos %}
#!/usr/bin/python

import numpy, Image

def dumpEachLayer(imageName):
  a1 = numpy.asarray(Image.open(imageName)) # pass Image
  for x in range(0, 255):
    Image.fromarray(numpy.asarray(map(lambda i: i & x, a1)), 'RGB').save('%d.png' % x)

def orEachUpperLower(func, imageOne, imageTwo, imageOut):
  a1 = numpy.asarray(Image.open(imageOne)) # pass Image
  a2 = numpy.asarray(map(lambda i: i & 0x0f, a1)) # lower 4 bits: 0x0f = 00001111
  a1 = numpy.asarray(Image.open(imageTwo)) # decoy Image
  a3 = numpy.asarray(map(lambda i: i & 0xf0, a1)) # higher 4 bits: 0xf0 = 11110000
  a4 = func(a2,a3) # bitwise or of both the images to reproduce 8 bit image.
  img = Image.fromarray(a4, 'RGB')
  img.save(imageOut)

def allBits(func, imageOne, imageTwo, imageOut):
  a1 = numpy.asarray(Image.open(imageOne)) # pass Image
  a2 = numpy.asarray(Image.open(imageTwo)) # decoy Image
  Image.fromarray(func(a1, a2), 'RGB').save(imageOut)

def sub(a1, a2):
  return a1 - a2

# Let's start out dumping all the layer's to see if there is anything there...
dumpEachLayer('stego100')
# Nope, all we got was a bunch of images...useless...

# Perhaps there is some funny things going on in the bits?
orEachUpperLower(numpy.bitwise_or, '22kUrzm.png', 'stego100', 'testOr.png')
orEachUpperLower(numpy.bitwise_xor, '22kUrzm.png', 'stego100', 'testXor.png')
orEachUpperLower(numpy.bitwise_and, '22kUrzm.png', 'stego100', 'testAnd.png')
# Nope...

# Okay...Hmmm, how about playing with all of the bits?
allBits(numpy.bitwise_or, '22kUrzm.png', 'stego100', 'testOr.png')
allBits(numpy.bitwise_xor, '22kUrzm.png', 'stego100', 'testXor.png')
allBits(numpy.bitwise_and, '22kUrzm.png', 'stego100', 'testAnd.png')
# Nope...

# Welp, we've two images - hell, let's subtract them.
allBits(sub, '22kUrzm.png', 'stego100', '22kUrzm-stego100.png')
allBits(sub, 'stego100', '22kUrzm.png', 'stego100-22kUrzm.png')
# MONEY!
{% endhighlight %}

[`diff.png`](https://raw.githubusercontent.com/ctfs/write-ups/master/tinyctf-2014/erik-baleog-and-olaf/diff.png) reveals a QR code:

![](https://raw.githubusercontent.com/ctfs/write-ups/master/tinyctf-2014/erik-baleog-and-olaf/diff.png)

Decoding the QR code gives `flag{#justdiffit}`, which is the flag.


