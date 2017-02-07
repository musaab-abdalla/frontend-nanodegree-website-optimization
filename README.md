#Website Optimization

######Overview

Website optimization project as part of the [Udacity](https://udacity.com) [Front-End Web Developer Nanodegree](https://classroom.udacity.com/nanodegrees/nd001). The task was to optimize a provided website with a number of optimization- and performance-related issues so that it achieves a target PageSpeed score and runs at 60 frames per second.

##Getting Started

######Live

**Go to** https://musaab-abdalla.github.io/website-optimization

######Locally

**1.** Clone this repo:

```
git clone https://github.com/musaab-abdalla/frontend-nanodegree-website-optimization.git
```
**2.** Serve the application:

```
$ python -m SimpleHTTPServer
```

Detailed Python Simple Server instructions can been found [here](https://docs.python.org/2/library/basehttpserver.html).

**3.** Open the application:

```
$ open "http://localhost:8000"
```

#1: Critical Rendering Path

######Overview

Get index.html achieves a PageSpeed score of at least 90 for Mobile and Desktop.

######Optimizations:

* Used the async javaScript method to load Google fonts.
* Reduce size of pizzeria.jpg image to 100px width.
* Convert profilepic.jpg to png.
* Optimizing images using Grunt plugin grunt-contrib-imagemin.
* Make google-analytics script async.
* Inline a CSS style.css file.
* Minifying a javaScript .js file.
* Add a media query for print.css.

######After above optimizations, PageSpeed improved to:

#######* mobile: 97/100
######* desktop: 95/100

#2: Frame Rate

######Optimizations:



#3: Computational Efficiency

######Optimizations:
