---
layout: post
title: "ImageMagick"
description: "Automating the watermarking of images"
category: scripts
tags: [imagemagick image magick script convert morph watermark]
---

{% include JB/setup %}

So I had to create a little script to add a watermark to all pictures in a given folder. And while I was at it, I would also resize all the images and auto-orient them according to their Exif metadata. 

This was actually surprisingly simple to do with ImageMagick! 

First we create a directory that we will use to put the result inside (we'll also use it to copy the originals to and edit them in place)

{% highlight bash %}
mkdir -p ./out/
{% endhighlight %}

After that, we iterate over all the files in a folder given as an argument (for the sake of simplicity, we assume all files in that folder are images)

{% highlight bash %}
for j in `ls -1 $1`
do
  echo $j
  convert -auto-orient $1$j $1$j
  width=$(identify -format "%w" $1$j)
  if [ "$width" -gt 1800 ]
  then
    convert -resize 1800 $1$j $1$j
  fi
  convert $2 miff:- | composite -dissolve 75 -gravity SouthEast - $1$j ./out/t_$j.png &
done
{% endhighlight %}

Ok, so what does this do inside the loop? First of all, it will print the file it is working on (```echo $j```). It will then orient the image (in place) according to the exif information (```convert -auto-orient $1$j $1$j```). 

When that is finished, it will look up the width of the image, if it is bigger than 1800px, it will resize it to 1800px. After that it will add an image (the second argument when you run this script) to the bottom right corner, and make it a little transparent. It will daemonize this call, so it doesn't hang on it and can continue with the next iteration.

To call this script, one should just use: ```./myscript.sh picsfolder/ my_watermark.png``` (this also assumes you did a ```chmod u+x myscript.sh```).

