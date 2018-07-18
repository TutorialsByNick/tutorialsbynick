---
layout: post
title: Javascript Animation Basics
comments: true
author: Nicholas Day
category: "Web Development Basics"
email: true
---

Javascript is a language that allows you to make interactive websites. Websites that host games, are dynamic applications, or do extensive animation or visualization. It's very versatile to say the least. We will be making a ball bounce around the screen in this tutorial.

# Table of Contents
* TOC
{:toc}

# Annoying Pop Ups

Open up your favorite code editor (I like to use [Visual Studio Code](https://code.visualstudio.com/)). Make a new file and call it `something.html`. Put a basic html structure like in [my HTML and CSS Basics tutorial]. It should look similar to this:

{% highlight html linenos %}
<!DOCTYPE html>
<html>
<head>
<title>Wow animation stuffs!</title>
<body>
</body>
</html>
{% endhighlight %}

This time around we are going to add a new tag, `<script>`. Place it inside of the body tag. The `<script>` tag is sort of similar to the `<style>` tag. Inside of the `<script>` tag we put our Javascript code that we want to execute on our page.

Just to make sure it's working let's create a little pop up. 

{% highlight html linenos %}
<!DOCTYPE html>
<html>
<head>
<title>Wow animation stuffs!</title>
<body>
<script>
alert("Hello!")
</script>
</body>
</html>
{% endhighlight %}

If you reload the page, an annoying pop up box should come up. Yay it works! But why `alert()`? What is it and what does it do? 

`alert("Hello!")` is a function. Functions are blocks of code you can run over and over. They can take some kind of input and give some kind of output but they don't always. You can tell by how there is a name and two parenthesis right next to it. The name `alert` itself was chosen by some of the people who originally created Javascript. They handily included functions that are useful for us. Inside of the parenthesis there is `"Hello!"`. This is some input given to the `alert` function, and with this input the browser makes the alert box with your text inside of it and shows it to you.

# A Blank Canvas

Enough of these annoying pop up thingys you say?! Say no more, let's draw things. For this we will need the `<canvas>` tag, which should go before the `<script>` tag and inside the `<body>` tag. Also, you should give it an id like `myBeautifulCanvas`.

{% highlight html linenos %}
<!DOCTYPE html>
<html>
<head>
<title>Wow animation stuffs!</title>
<body>
<canvas id="myBeautifulCanvas">
<script>
</script>
</body>
</html>
{% endhighlight %}

To use our beautiful canvas, we have to let the code know where it is. We can do that with the following piece of code:

{% highlight js %}
var myCanvas = document.getElementById("myBeautifulCanvas")
{% endhighlight %}

This is a lot of new information, so let's go over it. `var` stands for the word variable. That line creates a new variable with name `myCanvas`. A variable is sort of like a box that you can use to carry around useful pieces of data and use them over and over. You can also change the item inside the box but keep the box name (variable name) for data that changes. After we name it `myCanvas`, we have an equal sign and a function. The equal sign means put the piece of data from the right side of the equal sign into the variable box named `myCanvas`. The function `document.getElementById()` gives us the element that is uniquely named by an id passed to it as input. We use an id because we want to make sure that we are using only one element. In our case we are getting the canvas element so we can draw on it.

Next, we need to set up the `<canvas>` element for drawing. To do this we make another variable, `context` and set it equal to a function on the `<canvas>` element. The `getContext('2d')` function initializes the canvas for drawing in 2d. You can also initialize it by giving `getContext()` input like `webgl` for 3d drawing, or `bitmaprenderer` to draw images.

{% highlight js %}
var context = myCanvas.getContext('2d')
{% endhighlight %}

To draw a circle, we'll need 4 functions: `context.beginPath()`, `context.arc()`, `context.closePath()`, and `context.fill()`. I know this is a lot of functions at once, but they're not too hard. `beginPath()` creates the path for drawing. `closePath()` ends it. `arc()` draws an arc at some (x, y) pixel coordinate from a certain start angle to a certain end angle with a certain radius. In our case that would be `0` to `2*Math.PI` (`Math.PI` is a variable provided by the browser that approximates pi) because we want to draw all the way around the circle not just a slice of it. `fill()` draws the path on the canvas and fills it with a color.

Let's try and put this all together to draw a circle:

{% highlight js %}
var myCanvas = document.getElementById("myBeautifulCanvas")
var context = myCanvas.getContext('2d')

context.beginPath()
// This is a comment
// comments aren't read by the computer and can be used for documentation
// 50, 50 is x, y
// 10 is radius
// 0 is start angle
// 2*Math.PI is end angle
context.arc(50, 50, 10, 0, 2*Math.PI)
context.closePath()
context.fill()
{% endhighlight %}

I used comments in the code above to tell you what each of the inputs to the function does. These inputs are usually called arguments by other programmers.

# Animating Things!

You may have heard about how movies are just a series of pictures one after the other so fast that your brain thinks you're watching something moving. It's true. We will use the same technique here by drawing our circle, erasing it, drawing it again at a different position again and again at _high speeds_.

To do this, we will create our very first function!

{% highlight js %}
function draw() {
    // yay functions
}
{% endhighlight %}

Functions in Javascript are made by typing the word `function` then the name of said function (draw, in our case). Then some parenthesis and an opening curly bracket and a closing curly bracket. Our code to draw the circle will go inside of the curly brackets that way we can run this function over and over and it will draw our circle over and over. 

{% highlight js %}
function draw() {
    context.beginPath()
    context.arc(50, 50, 10, 0, 2*Math.PI)
    context.closePath()
    context.fill()
}

draw()
{% endhighlight %}

So you can see we made a function named `draw` and then we ran it one time. Because we want to run it over and over, we'll need to use another function named `requestAnimationFrame()`. This function synchronizes our drawing function with the browsers drawing function that draws all webpages.

We can run `requestAnimationFrame()` at the end of our draw function and give it the name of our draw function as input. That way the browser will know to call our draw function after we drew our previous circle.


{% highlight js %}
function draw() {
    context.beginPath()
    context.arc(50, 50, 10, 0, 2*Math.PI)
    context.closePath()
    context.fill()
    requestAnimationFrame(draw)
}
{% endhighlight %}

Now we should be drawing millions and billions and bajillions of circles over and over each of them on top of each other resulting in the magnificent effect of a single circle on the screen. Great isn't it? Okay, let's get that circle moving. You know that to move the circle, you want it to change the coordinates just a little bit each time the circle is drawn. This is the perfect use for a variable! Let's make one for the x coordinate and one for the y coordinate and start the position at (0, 0). We have to create the variables outside of the draw function because we don't want the variables to be created from scratch each draw. We want the coordinates to be updated with a slightly different position each time based on the old one.

An important fact to note is that canvas coordinate systems are strange. (0,0) is the top left corner of the canvas and (positive max width, positive max height) is the bottom right of the canvas.

{% highlight js %}
var x = 0
var y = 0
x = x + 10
y = y + 10
{% endhighlight %}

So in this block of code we make new variables `x` and `y` and set them both equal to 0. Then we set those variables equal to the previous item in the box (0), with 10 added to it (0 + 10). Now 0 + 10 or 10 is stored inside both `x` and `y`.

So what we will do now is put the `x = x + 10` parts inside of the draw function and use the variables `x` and `y` as inputs to the `arc()` function so that the position of the circle updates with every draw call.

{% highlight js %}
var x = 0
var y = 0

function draw() {
    x = x + 10
    y = y + 10
    context.beginPath()
    context.arc(x, y, 10, 0, 2*Math.PI)
    context.closePath()
    context.fill()
    requestAnimationFrame(draw)
}

draw()
{% endhighlight %}

Now if you run this code, you should see a bunch of overlapping circles quickly going diagonally across your beautiful canvas. :) We are almost there! Just need to clear the canvas before each draw to make it seem like a video. Luckily for us, there is a handy function called `clearRect()` that we can use. It draws a white rectangle from a start point with a width and a height given to it.

{% highlight js %}
var x = 0
var y = 0

function draw() {
    context.clearRect(0, 0, myCanvas.width, myCanvas.height)
    x = x + 10
    y = y + 10
    context.beginPath()
    context.arc(x, y, 10, 0, 2*Math.PI)
    context.closePath()
    context.fill()
    requestAnimationFrame(draw)
}

draw()
{% endhighlight %}

You should see a circle moving across your screen now. :) Not too bad right? If the canvas is too small for you, add width and height attributes (sizes in pixels) to your canvas element html like so:

{% highlight html %}
<canvas id="myBeautifulCanvas" height="500" width="500"></canvas>
{% endhighlight %}

You can also use `<canvas>` to draw rectangles, images, and other neat things. With Javascript and canvas, it's possible to make games in the web browser!

[my HTML and CSS Basics tutorial]: {% post_url 2017-08-31-basics-of-html-and-css %}
