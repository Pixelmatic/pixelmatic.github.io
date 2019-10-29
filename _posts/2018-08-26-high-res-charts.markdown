---
layout: post
title:  "[HOW-TO] Make Nice High-Res Charts and Graphs"
excerpt: "Whenever you need to communicate charts and/or graphs, Google Sheets and consort only provide you with low resolution resources. Here we propose a solution to fix that."
date:   2018-08-26 23:29:59 +0800
categories: general charts
---
Requirements:
* LibreOffice [https://www.libreoffice.org/](https://www.libreoffice.org/){:target="_blank"} (It may also work with OpenOffice)
* Inkscape [https://inkscape.org/](https://inkscape.org/){:target="_blank"}
* A chart or a graph you want to export in high resolution
* 5-10 minutes

Nothing could be simpler... 

First of all, if you are not working with LibreOffice yet, then download it right away. After that start LibreOffice Calc, import your data and generate the chart you like. 

Once your chart is ready, right-click on it and select: *Export as image*, as displayed in the picture below.

![calc](/assets/posts/high-res-charts/calc.png)

You will then be invited to select where and how to save your image. The idea is to take profit of the vector format, so we are going to save our image as an SVG file. 

![svg](/assets/posts/high-res-charts/svg.png)

Once saved, open the SVG file into Inkscape and you should see somehting like below. 

![inkscape](/assets/posts/high-res-charts/inkscape.png)

Here you can still edit the picture as you want actually. If you changed your mind and wants to change your colors scheme or resize some elements. Everything is possible. For example here I just added outlines to the pie and its slices. 

Then you can export in PNG in high resolution so that you  make sure you don't lose quality like in the screenshot below.

![export](/assets/posts/high-res-charts/export.png)

# Rasterized exports

![awesome_pie-1](/assets/posts/high-res-charts/awesome_pie-1.png)
<p style="text-align: center;"><small>High Resolution: 300 DPI export</small></p>

![low_res_pie](/assets/posts/high-res-charts/low_res_pie.png)
<p style="text-align: center;"><small>Low Resolution: 60 DPI export</small></p>

# Vector exports

And after all if your communication support allows SVG files, I would advice you to just save a copy as *Plain SVG* and display the SVG directly. Like every modern browser supports SVG. 

![plain_svg-1](/assets/posts/high-res-charts/plain_svg-1.svg)
<p style="text-align: center;"><small>Plain SVG edited in Inkscape</small></p>

![libreoffice](/assets/posts/high-res-charts/libreoffice.svg)
<p style="text-align: center;"><small>Plain SVG from LibreOffice</small></p>
