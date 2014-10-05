---
layout: post
title: Arduino Automation Magic!
categories:
- arduino
- Programming
tags:
- arduion
- python
- security
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pw_single_layout: '1'
---
Recently I ran into a cool device called <a href="http://www.arduino.cc/" title="Arduino" target="_blank">arduino</a>. You write your own 'firmware', load it to the chip, and watch the magic happen!

The project here is with a simple infrared motion detector. Utilizing that, and a small amount of scripting, created was an infrared motion tripped web camera recording device.


Arduino code:
{% highlight c linenos %}
//Infrared Motion Sensor Device

int infraredOutput = 10;
int voltagePin = 8;
int value = 0;


void setup(){

  pinMode(voltagePin, OUTPUT);
  pinMode(infraredOutput, INPUT);
  Serial.begin(9600);

}


void loop(){

  digitalWrite(voltagePin, HIGH);
  value = digitalRead(infraredOutput);
  
  if(value == HIGH){
    Serial.print("DETECTED SOME CHANGE IN INFRARED\n");
  }
    else value = LOW;
  }
}
{% endhighlight %}

As seen above, some quick and dirty code to detect changes from the sensor. (Arduino code is c++/c ish in apperance)

Next we have our script which launchs once something/someone has tripped the sensor!

{% highlight python linenos %}
#!/usr/bin/python

import serial, os, time

ser = serial.Serial('/dev/ttyACM0', 9600)
value = 0

while 1:
	print ser.readline()
	value+=1
#	if value <=1:
#		time.sleep(20)
	print "WAITINGFORMOREINFO" + str(value)
	command = "ffmpeg -t 1800  -threads 0 -bt 512k -y -f video4linux2
 -i /dev/video0 -s 640x480
 -vcodec libx264 -flags +loop -me_method full -g 250 -qcomp 0.6 -qmin 15 -qmax 30
 -qdiff 10 -b_strategy 1 -i_qfactor 0.6 -cmp +chroma -subq 1 -coder 1 
 -sc_threshold 40 -crf 17 -cqp 20 -flags2 -bpyramid-wpred-mixed_refs-dct8x8+fastpskip
 -keyint_min 250 -refs 5 -trellis 0 -directpred 1 
 -partitions -parti8x8+parti8x8+partp4x4-partp4x4-partb8x8
 -an output{\%s}.mp4"%value

	if value >= 40:
        	p = os.system(command)
		time.sleep( 1 )

	ser.flushInput()
	ser.flushOutput()
	ser.flush()
ser.close()
{% endhighlight %}

Good'ol python to the party!

This is just a rough code chunk...If it were to be spruced up I would first create a u-dev mapper for my webcam/recording device sothat it is always located at /dev/whatever...
