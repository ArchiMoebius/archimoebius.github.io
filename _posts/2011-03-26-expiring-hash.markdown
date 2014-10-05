---
layout: post
title: Expiring Hash
categories:
- PHP
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---
For those who are working with systems which require a time based access restriction imposed upon some resource; there is no easier way to-do this than by using a time based hash! Basically we start out with something like so:

{% highlight php linenos %}
<?php
$someConstant = "The logged in user's name and or database ID";
$hash = md5($someConstant);
?>
{% endhighlight %}

Now the above code does give you a unique hash which can be generated on the fly for whoever. The only issue with this comes when you need a time restraint for the hashes validity. Since we all like to code smarter, lets put our time in our hash/API key/Promo code/Whatever!

{% highlight php linenos %}
<?php
$someConstant = "The logged in user's name and or database ID";
$hash = md5(date('l jS \of F Y').$someConstant);
?>
{% endhighlight %}

Now we have a hash which will expire in a days time depending on how you do your verification.

{% highlight php linenos %}
<?php
$someConstant = "The logged in user's name and or database ID";
$hash = md5(date('l jS \of F Y').$someConstant);
$postHash = $_POST['hash'];

if(strcasecmp($hash, trim($postHash)) == 0)
    echo "You are just in time!";
else
    echo "You are using an expired hash!";
?>
{% endhighlight %}

Now go create some time based hashes!!!

Note: Don't flame me for not cleaning my input. It's code snippets not enterprise work!
