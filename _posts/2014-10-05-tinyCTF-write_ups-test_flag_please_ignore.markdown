---
layout: post
title: TinyCTF - test-flag-please-ignore
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

Content found at: [Tiny CTF 2014 write-ups](https://github.com/ctfs/write-ups/tree/master/tinyctf-2014/test-flag-please-ignore "TinyCTF 2014 write-ups")

Un-zip [the provided `misc10.zip` file](https://github.com/ctfs/write-ups/raw/master/tinyctf-2014/test-flag-please-ignore/misc10.zip):

{% highlight bash linenos %}
$ unzip misc10.zip
Archive:  misc10.zip
  inflating: misc10
{% endhighlight %}

Extracting the provided `misc10.zip` file reveals a text file with the following contents:

{% highlight bash linenos %}
666c61677b68656c6c6f5f776f726c647d
{% endhighlight %}

Since this wasn't accepted as the solution (and neither was `flag{666c61677b68656c6c6f5f776f726c647d}`), I tried to hex-decode it:

{% highlight bash linenos %}
$ xxd -r -p <<< 666c61677b68656c6c6f5f776f726c647d
flag{hello_world}
{% endhighlight %}

The flag is `flag{hello_world}`.

## Other write-ups

Well, this is interesting, how long is it?

{% highlight bash linenos %}
python -c "print len('666c61677b68656c6c6f5f776f726c647d')"

34
{% endhighlight %}

That's not a hash length I know of...hmmm, what is it in ascii?

{% highlight bash linenos %}
python -c "print '666c61677b68656c6c6f5f776f726c647d'.decode('hex')"
{% endhighlight %}

MONEY!
