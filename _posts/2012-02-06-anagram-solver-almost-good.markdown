---
layout: post
title: Anagram Solver, Almost Good.
categories:
- Perl
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---
Anagrams always seem to find there way into the latest paper/magazine and for those with limited vocabularies, they can pose a quite time consuming pastime. So I created a simple solver which handles a good portion of them, doing all that unscramble magic in a few seconds instead of half a hour!


{% highlight perl linenos %}
#!/usr/bin/perl

print "\\n\\nWords : \\n";

@wordsToSolve = `cat words`;
@listOfRealWords = `cat list`;
        foreach (@wordsToSolve){
                foreach $line(@listOfRealWords){

                        $line =~ s/[^a-zA-Z0-9]*//g;
                        @word = sort split(//, $line);
                        chomp $_;
                        @test = sort split(//, $_);

                        if(join("", @word) eq join("", @test)){
                                print $line.",";
                        }
                }
        }

print "\\n\\n";
{% endhighlight %}


It's a simple perl script. Yes, I know, there is that 2% of the English language where one words letters can be used to make another word (without subtracting or adding any characters). Outside of that case; it works flawlessly! Also to note: The files 'words' and 'list' (found at the top of the script), contain one anagram/word per line. (Where the file 'list' is a huge, well, list of words, word-list;dictionary)
