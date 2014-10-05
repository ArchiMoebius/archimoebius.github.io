---
layout: post
title: Dynamic Object Creation - PHP
categories:
- PHP
- Programming
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---
Being a scripting language were types are basically none existent when compared to a language such as C or AS3; the ability to create some pretty cool functionality with a small amount of code is a menial task. For example, lets create some objects dynamically, 'at run time'. This would be nice for things like <a href="http://en.wikipedia.org/wiki/Representational_State_Transfer" target="_blank">REST</a> based web-services. For simplicities sake I am going to throw together all the code in one big dump. Normally, it would be broken up more, sensibly.

{% highlight php linenos %}
<?php

//in file dummy.class.php
class dummy
{
    public function doDummyThing()
    {
        //thingDummyDoes;
    }
}

//in file dummyKid.class.php
class dummyKid
{
    public function doDummyThing()
    {
        //thingDummyKidDoes;
    }
}

//in file service.php
$classname = $_POST['loadfile'];
$method = $_POST['method'];
include_once("$classname.class.php")

dDummy = new $classname();
dDummy->{$method}();
?>
{% endhighlight %}

With the above code a simple <a href="http://en.wikipedia.org/wiki/POST_%28HTTP%29" target="_blank">HTTP POST</a>
with parameters set properly would load in the selected class and execute the selected function. Now this example is pretty boring... \-: However, if you think of this concept and how it could be applied you might come up with a pretty slick web-service framework. Assuming that the architecture was done properly and more convention than configuration was used the only part which would need to be documented for use is the actually URL's for the services and there related parameters/methods. Perhaps next month a simple PHP RESTful JSON based web-service framework will be born.

To be noted:
This is a basic example and like all examples on this site: Don’t flame me for not cleaning my input. It’s code snippets not enterprise work!
