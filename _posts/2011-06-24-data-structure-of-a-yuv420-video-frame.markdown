---
layout: post
title: Data-Structure of a YUV420 Video Frame
categories:
- Formats
- video
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---
We all use video's on a day to day basis whether its just viewing the latest YouTube post or talking to a friend over Skype. The majority of today's web technologies use a frame encoding format called <a target="_blank" href="http://en.wikipedia.org/wiki/YUV">YUV</a>420. Now this format is what is used to compress each and every frame of your video/video stream. Lets take a look at one frame of a video at the byte level.

<img  width="300" height="500"  src="{{ site.url }}/assets/images/yuv420pByteLayoutPixelMapping.png" alt="YUV420 Byte Layout" /> 

In each frame of a video which is using the yuv420 format the frames contents are laid out as shown above. Unlike what you are probably used to, the frame above only has <a target="_blank" href="http://www.fourcc.org/yuv.php">Y, U, and V</a> components which make up the picture you view. (You are probablly used to RGB) If you want to learn more about the <a target="_blank" href="http://msdn.microsoft.com/en-us/library/bb530104%28v=vs.85%29.aspx">YUV color-space</a>, <a target="_blank" href="http://softpixel.com/~cwright/programming/colorspace/yuv/">Click Here</a>.

So in the frame, each 2x2 Y block has a corresponding U and V block. (These are what 'complete' the color-space).

As Shown above, each 2x2 block of Y Pixel's has a U and a V byte. In every frame there are (width times height) Y bytes, (width times height divided by four) U and V bytes. This nifty configuration helps compression and is many times better than RGB which stores each pixel color in three to four byte 'chunks'.

Also to be noted: YUV420 is a planner format which means all the Y values come first followed by the U and then the V; where as in an interleaved format your values would be YUV,YUV,YUV. (Instead of the former which is YYYYUV) 
