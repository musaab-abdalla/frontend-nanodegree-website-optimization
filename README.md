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
###1: Critical Rendering Path
######Overview
Get index.html achieves a PageSpeed score of at least 90 for Mobile and Desktop.
######Optimizations:
* Used the async javaScript method to load Google fonts.
* Reduced size of `pizzeria.jpg` image to 100px width.
* Convert profilepic.jpg to png.
* Optimized images using Grunt plugin `grunt-contrib-imagemin`.
* Loaded `google-analytics` JavaScript asynchronously.
* Inline a CSS `style.css` file.
* Minifying a javaScript `.js` file.
* Added media attribute for `print.css`.

######After above optimizations, PageSpeed improved to:
* mobile: 97/100
* desktop: 95/100

###2: Frame Rate
######Overview
Optimizations made to `views/js/main.js` make views/pizza.html render with a consistent frame-rate at 60fps when scrolling. You will find instructional comments in `main.js`.
######Optimizations:
* Improves loading performance moved elements outside the loop. Using a local variable instead of a property lookup can speed up the loops.
```
    var pizzasDiv = document.getElementById("randomPizzas");
```
* Using local variables is especially important when dealing with HTMLCollection objects. Using getElementsByClassName is faster way to access the DOM than querySelectorAll.
```
    var items = document.getElementsByClassName('mover');
```
* Calculates the five phase into its own for loop that appends each phase to an array, rather than declaring and setting the phase variable each time.
```
    var phase = [];
    var top = document.body.scrollTop / 1250;
    for (var i = 0; i < 5; i++) {
        phase.push(Math.sin(top + i) * 100);
    }
```
* The pizza item positions are changed by accessing the relevant element of the phase array, rather than reusing the phase variable.
```
    for (var i = 0, max = items.length; i < max; i++) {
    items[i].style.left = items[i].basicLeft + phase[i % 5] + 'px';
    }
```
* Since the control statement (i < items.length) is executed each time through the loop. The function will run faster when this value is stored in a local variable and then accessed from there.
```
    for (var i = 0, max = items.length; i < max; i++) {
      }
```
* Moved scrollTop request outside the for loop and the browser has to give the most up-to-date value. Using a local variable instead of a property lookup can speed up the loops.
```
    var top = document.body.scrollTop / 1250;
```
* Add this property to `.mover` class in `style.css`
```
    -webkit-backface-visibility: hidden;  Chrome, Safari, Opera
    backface-visibility: hidden;
  ```
* Generate max number of pizza number is now dynamic, based on screen height.
```
    var rows = Math.ceil(window.screen.height / s);
    var numberOfPizzas = rows * cols;
  ```
* Using document.getElementById() Web API call is faster, saved this DOM call outside the for statement and save it into a local variable.
```
  var movingPizzas = document.getElementById('movingPizzas1');
  ```
* Declaring the elem variable (var elem;) in the initialization of the for-loop will prevent it from being created every time the loop is executed.
```
    for (var i = 0, elem; i < numberOfPizzas; i++) {
    }
```

###3: Computational Efficiency
######Overview
Time to resize pizzas is less than 5 ms using the pizza size slider on the `views/pizza.html` page. Resize time is shown in the browser developer tools.
######Optimizations:
* Fixed forced synchronous layout issue with pizza sliders
* Unrolling loop to improve performance. The basis of this is limiting the number of iterations can mitigate the performance overhead of a loop. Which means making each iteration do the work of multiple iterations.
```
switch(size) {
      case "1":
        newWidth = 25;
        break;
      case "2":
        newWidth = 33.3;
        break;
      case "3":
        newWidth = 50;
        break;
      default:
        console.log("bug in sizeSwitcher");
    }
```
* Using a local variable instead of a property lookup can speed up the loops.
* Using getElementsByClassName instead of querySelectorAll is faster way to access the DOM.
```
var randomPizzas = document.getElementsByClassName("randomPizzaContainer");
```
* Modify width changes and remove px calculation.
* Stores the length of the randomPizzas HTMLCollection in a local variable, limiting the number of times the object is accessed directly.
```
for (var i = 0, randomPizzasLength = randomPizzas.length; i < randomPizzasLength; i++) {
        randomPizzas[i].style.width = newWidth + "%";
    }
  ```
