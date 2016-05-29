# Website Performance Optimization portfolio project

In this project I was Tasked to optimize this project so that it meets industry standards. the following optimizations this project required were:

#### 1. Achieve Pagespeed Insights score of 90+ on both Mobile and Desktop
#### 2. Achieve 60 FPS average when scrolling on pizza.html
#### 3. Achieve pizza size change speed of sub-5ms. (time is logged in console)

To get started, check out the repository, inspect the code, run the website live with the following links:
* <a href="http://ericbezanson.github.io/frontend-nanodegree-mobile-portfolio/"> index.html</a>
* <a href="http://ericbezanson.github.io/frontend-nanodegree-mobile-portfolio/views/pizza.html"> pizza.html</a>


####Part 1: Optimize PageSpeed Insights score for index.html.

to accomplish this the following changes were made:

* Compressed and optimized all images on the website.
* Inlined all styles to avoid render blocking CSS.
* Used media query to prevent print.css from becoming render blocking.
* used web font loader instead of render blocking googlefont api  (<a href="https://github.com/typekit/webfontloader">Information Source</a>)

####Part 2: Optimize Frames per Second in pizza.html.

to accomplish this the following changes were made:

* acording to research I have done GetElementsByClassName() is faster then querySelectorAll so I changed that within the updatePosition function (<a href="(https://www.nczonline.net/blog/2010/09/28/why-is-getelementsbytagname-faster-that-queryselectorall/)">Information Source</a>
* created scrolling var outside of for loop in updatePositions so it would be cached in global scope preventing multiple pulls of the DOM which would have otherwise created Reflow (Forced Synchronous Layout)
* lowered the amount of pizzas generated to 25 from 200. I had counted the pizzas on screen at multiple points during scroll and it never once had more then 25, anything more then 25 would be redundant and detremental to the framerate.

####Before
![Before](https://github.com/ericbezanson/frontend-nanodegree-mobile-portfolio/blob/gh-pages/img/PizzaPreOp.jpg "Before")

####After
![After](https://github.com/ericbezanson/frontend-nanodegree-mobile-portfolio/blob/gh-pages/img/PizzaPostOp.jpg "After")

####Part 3: Optimize time to resize pizza.

to accomplish this the following changes were made:

* Created var to store randomPizzaConatiner elements, decreasing the frequency of DOM access.
* Removed the Variables dx and newWidth from the for loop and into the global scope, caching them and preventing muliple iterations, this was the biggest boon to resize time.

Before Optimization it took between 95 - 105ms to change the images, this is the result after optimization.
![Result] (https://github.com/ericbezanson/frontend-nanodegree-mobile-portfolio/blob/gh-pages/img/PizzaChangerPostOp.jpg "Result")
