---
layout: post
title: Perl rand48 - Just Because
categories:
- Perl
- Programming
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---
If one has ever needed to work with numbers in Perl they know funky things happen at times... Just for kicks here is an implementation of rand48 from libc.

{% highlight perl linenos %}

#!/usr/bin/perl                                                                 
                                                                                
use Math::BigFloat;                                                             
Math::BigFloat->precision(-16);                                                 
                                                                                
$next = Math::BigFloat->new(0);                                                 
$x = Math::BigFloat->new(0);                                                    
$a = Math::BigFloat->new(0x5DEECE66D);                                          
$c = Math::BigFloat->new(0xB);                                                  
$m = Math::BigFloat->new(2**48);                                                
$sd = Math::BigFloat->new(0x330E);                                              
$ls = Math::BigFloat->new(16);                                                  
                                                                                
srand($ARGV[0]);                                                                
doSeed($ARGV[0]);                                                               
                                                                                
$cnt = 50000;                                                                   
while(--$cnt)                                                                   
{                                                                               
   print int rand 64;                                                           
   print "\n";                                                                  
   print int doRand()*64;                                                       
   print "\n";                                                                  
}                                                                               
sub doRand{                                                                     
   $x = $next;                                                                  
   $next = (($a*$x+$c) % $m);                                                   
   return ($next/$m);                                                           
}                                                                               
                                                                                
sub doSeed{                                                                     
   $next = ((Math::BigFloat->new($_[0]) << $ls) + $sd);                         
}    

{% endhighlight %}

Sure, there is a zealous and probably over use of Math in there, but, it's simple enough to optimise if one feels like it. (Or just go do it in C...)
