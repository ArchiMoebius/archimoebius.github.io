---
layout: post
title: Cyanogenmod - incorporate bitbucket hosted app in build with local_manifest
categories:
- Android
- Programming
tags:
- android
- bitbucket
- configuration
- cyanogenmod
- manifests
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---
<a href="http://www.cyanogenmod.org/" title="Cyanogenmod" target="_blank">Cyanogenmod</a> is a ROM for android devices.

As an extension to the page for <a href="http://wiki.cyanogenmod.org/w/Doc:_adding_your_own_app" title="adding your own android app" target="_blank">adding your own android app</a> to the build process; this is how you setup a <a href="http://bitbucket.org" title="bitbucket" target="_blank">bitbucket.org</a> project to the process.

### Step 1.

Create a .xml file under: android/system/.repo/local_manifests with the following contents:

{% highlight xml linenos %}

<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote 
    name="bitbucket" 
    fetch="https://bitbucket.org/username" 
  />
  <project 
    name="reponame" 
    path="packages/apps/reponame" 
    remote="bitbucket" 
    revision="refs/heads/master"
  />
</manifest>

{% endhighlight %}

### Step 2.

Update the username and reponame to match that of your username and repository.

### Step 3.

Change back to your android/system folder and do a 'repo sync'

Your project should now reside under android/system/packages/apps/reponame.