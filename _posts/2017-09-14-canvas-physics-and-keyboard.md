---
layout: post
title: "Canvas: Physics and Keyboard Handling"
comments: true
author: Nicholas Day
email: true
category: "Web Development Basics"
---

Previously, we had gone over [Javascript Animation Basics]. In this tutorial, we will make our ball bounce around inside of the canvas element. We will also use the keyboard to control the movement of the ball. Let's get to it!

# Table of Contents
* TOC
{:toc}

# "Physics"

Our goal here is for the ball to change velocity when it hits the side of the canvas rather than keep going off infinitely. Because we have a `x` and `y` coordinate position for the ball, we can determine when it has gone past the boundaries of the canvas. For this we will use `if` statements to check whether the ball is outside of the canvas. We also create two variables called `vx` and `vy` which is the velocity of the ball in the x and the y axis respectively. `if` statements are read in your head like `if` `(condition)` is true then run the code inside of the `{}`'s.

{% highlight js %}
var x = 0
var y = 0
var vy = 10
var vx = 10

function draw() {
    context.clearRect(0, 0, myCanvas.width, myCanvas.height)
    x = x + vx
    y = y + vy
    if (x > myCanvas.width) {
        vx = -vx
    }
    if (y > myCanvas.width) {
        vy = -vy
    }
    context.beginPath()
    context.arc(x, y, 10, 0, 2*Math.PI)
    context.closePath()
    context.fill()
    requestAnimationFrame(draw)
}

draw()
{% endhighlight %}

Now the ball should bounce back after hitting the edge of the screen! :) But, it keeps going past the other side now. :( What we need to do is check if the ball has gone past the top left corner of the screen which is `(0, 0)`. We can change the `if` statements to say `if` the ball is past the bottom right corner, or `if` the ball is past the top left corner, change the velocity. We do that by changing our condition to `(past bottom right corner || past top left corner)`.

{% highlight js %}
if (x > myCanvas.width || x < 0) {
    vx = -vx
}
if (y > myCanvas.width || y < 0) {
    vy = -vy
}
{% endhighlight %}

Yay! It should bounce back and forth now. :)

# Keyboard Handling

Now, let's modify our program to use the keyboard to control the movement of the ball. Take out where the velocity is automatically added to the position of the ball because we want the keyboard to handle that.

{% highlight js %}
var x = 0
var y = 0
var vy = 10
var vx = 10

function draw() {
    context.clearRect(0, 0, myCanvas.width, myCanvas.height)
    if (x > myCanvas.width || x < 0) {
        vx = -vx
    }
    if (y > myCanvas.width || y < 0) {
        vy = -vy
    }
    context.beginPath()
    context.arc(x, y, 10, 0, 2*Math.PI)
    context.closePath()
    context.fill()
    requestAnimationFrame(draw)
}

draw()
{% endhighlight %}

Next, we add an event listener to the html page. We do that with the `document.addEventListener()` function. It takes the event name as input, along with the function that you want it to run every time that event happens. For us, we would use the `keydown` event because we want to be able to tell when a key on the keyboard has been pressed. That looks like this:

{% highlight js %}
document.addEventListener('keydown', function(event) {
    console.log(event)
})
{% endhighlight %}

The function provided to `document.addEventListener()` takes the event as an argument. This event has information like what key was pressed, which we can use to determine whether to move the ball left, right, up, or down. `console.log` takes any kind of input and prints this out to the browser's console. To see the console, right click on the webpage, click `Inspect`, then click `Console`. What you log with `console.log()` should show up in the window that pops up.

So, you might be wondering... Nick, how do we tell what key we pressed? Good question :) We can use those `if` statements that we just learned to tell what the key is named. Go back to your webpage and press keys. You should notice in the console there is a `event.key` variable. When you press the left arrow key, `event.key` is `ArrowLeft`. For the right arrow key, `event.key` is `ArrowRight`. `ArrowUp` for the up arrow key, and you guessed it `ArrowDown` for the down arrow key.

{% highlight js %}
document.addEventListener('keydown', function(event) {
    if (event.key == "ArrowRight") {
        console.log("right key pressed")
    }
    if (event.key == "ArrowLeft") {
        console.log("left key pressed")
    }
    if (event.key == "ArrowUp") {
        console.log("up key pressed")
    }
    if (event.key == "ArrowDown") {
        console.log("down key pressed")
    }
})
{% endhighlight %}

We use `==` rather than `=` because `==` checks if two things are equal, and `=` changes a variable. In the console you should see the "left key pressed" when you press the left arrow key, "up key pressed" for the up arrow key, etc.

So then, we can directly change the position inside of this event listener we created:

{% highlight js %}
var x = 0
var y = 0
var vy = 10
var vx = 10

document.addEventListener('keydown', function(event) {
    if (event.key == "ArrowRight") {
        x = x + vx
    }
    if (event.key == "ArrowLeft") {
        x = x - vx
    }
    if (event.key == "ArrowUp") {
        y = y - vy
    }
    if (event.key == "ArrowDown") {
        y = y + vy
    }
})

function draw() {
    context.clearRect(0, 0, myCanvas.width, myCanvas.height)
    if (x > myCanvas.width || x < 0) {
        vx = -vx
    }
    if (y > myCanvas.width || y < 0) {
        vy = -vy
    }
    context.beginPath()
    context.arc(x, y, 10, 0, 2*Math.PI)
    context.closePath()
    context.fill()
    requestAnimationFrame(draw)
}

draw()
{% endhighlight %}

# Advanced Keyboard Handling

Wowzers! Your code should now let you move the circle around the canvas! But wait... when you press and hold down an arrow key, the movement is jerky and doesn't look as nice as it should. Also, you can't press two keys at the same time to move the circle. You can only move the circle in one direction at a time. :( Let's fix that. What we want is to move the circle when a key is pressed in that direction and stop moving the object when the key is released. We can use the `keyup` event to tell when the key has been released. :) Isn't the browser great? So what we can do is say hey this key is pressed inside of a variable when the `keydown` event fires and change that variable to say the key is not pressed when we get the `keyup` event.

{% highlight js %}
var leftPressed = false
var rightPressed = false
var upPressed = false
var downPressed = false

document.addEventListener('keydown', function(event) {
    if (event.key == "ArrowRight") {
        rightPressed = true
    }
    if (event.key == "ArrowLeft") {
        leftPressed = true
    }
    if (event.key == "ArrowUp") {
        upPressed = true
    }
    if (event.key == "ArrowDown") {
        downPressed = true
    }
})

document.addEventListener('keyup', function(event) {
    if (event.key == "ArrowRight") {
        rightPressed = false
    }
    if (event.key == "ArrowLeft") {
        leftPressed = false
    }
    if (event.key == "ArrowUp") {
        upPressed = false
    }
    if (event.key == "ArrowDown") {
        downPressed = false
    }
})
{% endhighlight %}

You should see that we are using these weird true and false values rather than numbers or strings. `true` and `false` are boolean values. For a boolean variable, its value can be either `true` or `false`, and we can use them in `if` statements. So `if` `leftPressed` is `true`, then subtract the x velocity from the ball's position. `if` `rightPressed` is `true` add the x velocity to the ball's position, and so on for up and down. We put this inside of the `draw()` function because we want it to run every time the ball is drawn. We can't use the `keyup` and `keydown` events because they only run when the key is first pressed up or released and then infrequently. We want smooth motion while the key is pressed. 

{% highlight js %}
var x = 0
var y = 0
var vx = 10
var vy = 10

var leftPressed = false
var rightPressed = false
var upPressed = false
var downPressed = false

document.addEventListener('keydown', function(event) {
    if (event.key == "ArrowRight") {
        rightPressed = true
    }
    if (event.key == "ArrowLeft") {
        leftPressed = true
    }
    if (event.key == "ArrowUp") {
        upPressed = true
    }
    if (event.key == "ArrowDown") {
        downPressed = true
    }
})

document.addEventListener('keyup', function(event) {
    if (event.key == "ArrowRight") {
        rightPressed = false
    }
    if (event.key == "ArrowLeft") {
        leftPressed = false
    }
    if (event.key == "ArrowUp") {
        upPressed = false
    }
    if (event.key == "ArrowDown") {
        downPressed = false
    }
})

function draw() {
    context.clearRect(0, 0, myCanvas.width, myCanvas.height)
    if (x > myCanvas.width || x < 0) {
        vx = -vx
    }
    if (y > myCanvas.width || y < 0) {
        vy = -vy
    }

    if (leftPressed) {
        x = x - vx
    }

    if (rightPressed) {
        x = x + vx
    }

    if (upPressed) {
        y = y - vy
    }

    if (downPressed) {
        y = y + vy
    }
    context.beginPath()
    context.arc(x, y, 10, 0, 2*Math.PI)
    context.closePath()
    context.fill()
    requestAnimationFrame(draw)
}

draw()
{% endhighlight %}

Fantastic job! Now your ball should be controllable by your arrow keys. :)

[Javascript Animation Basics]: {% post_url 2017-09-01-javascript-animation-basics %}