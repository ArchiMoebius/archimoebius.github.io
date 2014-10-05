---
layout: post
title: TinyCTF - tt3441810
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

Content found at: [Tiny CTF 2014 write-ups](https://github.com/ctfs/write-ups/tree/master/tinyctf-2014/tt3441810 "TinyCTF 2014 write-ups")

Un-zip [the provided `rev100.zip` file](https://github.com/ctfs/write-ups/raw/master/tinyctf-2014/tt3441810/rev100.zip):

{% highlight bash linenos %}
$ unzip rev100.zip
Archive:  rev100.zip
  inflating: rev100
{% endhighlight %}

The extracted `rev100` file looks like a hexdump:

{% highlight bash linenos %}
$ file rev100
rev100: ASCII text, with CRLF line terminators

$ cat rev100
00400080  68 66 6C 00 00 48 BF 01  00 00 00 00 00 00 00 48
00400090  8D 34 24 48 BA 02 00 00  00 00 00 00 00 48 B8 01
004000A0  00 00 00 00 00 00 00 0F  05 68 61 67 00 00 48 BF
004000B0  01 00 00 00 00 00 00 00  48 8D 34 24 48 BA 02 00
004000C0  00 00 00 00 00 00 48 B8  01 00 00 00 00 00 00 00
004000D0  0F 05 68 7B 70 00 00 48  BF 01 00 00 00 00 00 00
004000E0  00 48 8D 34 24 48 BA 02  00 00 00 00 00 00 00 48
004000F0  B8 01 00 00 00 00 00 00  00 0F 05 68 6F 70 00 00
00400100  48 BF 01 00 00 00 00 00  00 00 48 8D 34 24 48 BA
00400110  02 00 00 00 00 00 00 00  48 B8 01 00 00 00 00 00
00400120  00 00 0F 05 68 70 6F 00  00 48 BF 01 00 00 00 00
00400130  00 00 00 48 8D 34 24 48  BA 02 00 00 00 00 00 00
00400140  00 48 B8 01 00 00 00 00  00 00 00 0F 05 68 70 72
00400150  00 00 48 BF 01 00 00 00  00 00 00 00 48 8D 34 24
00400160  48 BA 02 00 00 00 00 00  00 00 48 B8 01 00 00 00
00400170  00 00 00 00 0F 05 68 65  74 00 00 48 BF 01 00 00
00400180  00 00 00 00 00 48 8D 34  24 48 BA 02 00 00 00 00
00400190  00 00 00 48 B8 01 00 00  00 00 00 00 00 0F 05 68
004001A0  7D 0A 00 00 48 BF 01 00  00 00 00 00 00 00 48 8D
004001B0  34 24 48 BA 02 00 00 00  00 00 00 00 48 B8 01 00
004001C0  00 00 00 00 00 00 0F 05  48 31 FF 48 B8 3C 00 00
004001D0  00 00 00 00 00 0F 05
{% endhighlight %}

Hmmm, ok...So what are we looking for again?

A flag, in the format: flag{??????}

Alright, so, what does flag look like in hex?

{% highlight bash linenos %}
echo 'flag' | xxd
0000000: 666c 6167 0a                             flag.
{% endhighlight %}

In hex, flag == 666c 6167, ok, so is that pattern in the hexdump?

YUP!!! And it looks like a constant seperation / pattern, two characters, garbage, two characters...

Let's first get this file into something we can read in a simply manner...

{% highlight bash linenos %}
cat rev100 | cut -f 3- -d ' ' | tr ' ' '\n'
{% endhighlight %}

Now let's script it:

{% highlight python linenos %}
#!/usr/bin/python

f = open('i2', 'r')

values = []

# Load all of the lines in
for line in f.readlines():
  v = line.strip().replace('\n', '')
  if v != '':
    values.append(v)

f.close()

# Skip the first char (it was junk and no the 66 we are looking for)
values = values[1:]

flag = ''

# Get our flag out following the pattern: two chars, 40 chars, two chars....
for i in range(0,len(values)-1,41):
  flag = flag + values[i] + values[i+1]

print flag.decode('hex')
# MONEY!!!
{% endhighlight %}
