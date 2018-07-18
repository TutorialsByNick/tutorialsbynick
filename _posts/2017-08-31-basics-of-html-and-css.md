---
layout: post
title: Basics of HTML and CSS
comments: true
author: Nicholas Day
category: "Web Development Basics"
email: true
---

HTML is the language that powers websites. You use HTML to structure the content that shows up on the webpage. CSS is the language that handles styling of the webpage and content layout. We will be making a basic todo list in this tutorial, so lets get started! Please follow along by writing the code yourself and using your browser to open the file. Make sure to refresh the webpage when you've saved your code.

# Table of Contents
* TOC
{:toc}

# A Basic HTML Page

Open up your favorite code editor (I like to use [Visual Studio Code](https://code.visualstudio.com/)). Make a new file and call it `something.html`. All html files end in either `.html` or `.htm`. First we put `<!DOCTYPE html>` at the top of the file. This will tell the browser that we are using the latest version of HTML. Next let's put a html tag in the document.

{% highlight html linenos %}
<!DOCTYPE html>
<html>
    Stuff inside of the html tag
</html>
{% endhighlight %}

As you can see, a html element has an opening (`<html>`) and closing (`</html>`) tag. Inside of the opening and closing tag are either other tags or content. Usually tags inside of other tags are indented by a tab or 4 spaces to allow for easier code reading.

The head element stores information that isn't shown to the webpage reader, but has information for search engines and links to styling resources and the title of the webpage. Let's add a title to our html file:

{% highlight html linenos %}
<!DOCTYPE html>
<html>
<head>
    <title>This is the title of my website!</title>
</head>
</html>
{% endhighlight %}

Like a letter webpages have a head and a body. The body is where the content that you see on the webpage is stored.

{% highlight html linenos %}
<!DOCTYPE html>
<html>
<head>
    <title>This is the title of my website!</title>
</head>
<body>
Hello, my amazing readers! You are fantastic!
</body>
</html>
{% endhighlight %}

# A Basic Todo List

Doesn't everyone always have too much on their plate? Let's make a simple todo list to lessen our stresses. In html, the `ul` tag creates a bullet list and the `ol` tag creates a numbered list. Inside of those tags you use `li` tags which contain the text you want to put on your list.

{% highlight html linenos %}
<!DOCTYPE html>
<html>
<head>
    <title>This is the title of my website!</title>
</head>
<body>
Why do I have so much to do...
<ul>
    <li>Write an article</li>
    <li>Write another article</li>
    <li>Write 2 more articles</li>
    <li>Read a few articles</li>
    <li>Write 3 more articles</li>
</ul>
The work never ends. :(
</body>
</html>
{% endhighlight %}

# A Prettier Todo List

Honestly, my todo list is too plain to look at. Let's use some CSS to stylize it and make it prettier. CSS is fairly simple. There are selectors which tell the browser what html elements to apply the styles to and properties which can change certain styles of our elements. We will go over some selectors and properties in a bit.

{% highlight css linenos %}
li {
    color: red;
}
.this-is-a-class-selector {
    color: blue;
}
#this-is-an-id-selector {
    color: green;
}
{% endhighlight %}

On line 1, we can see the selector is the `li` html element. This means that for every `li` element in our html the color will be red. On line 4, the selector is for CSS classes. 

A html element like this `<li class="this-is-a-class-selector another-class">Hi</li>` will have the styles from `this-is-a-class-selector` and `another-class` applied to it. But wait, we already changed a color for all `li` elements! What happens when we change the color again with a class? I'm glad you asked, dear reader. The later things in your CSS take precedence over the things before it. So `li` elements that don't have a class will be red, but `li` elements with a class will be blue because that style is written later in the CSS. 

On line 7, that is an id selector. Only one of those can be applied per element unlike classes. This is how they are applied: `<li id="this-is-an-id-selector">Hello again</li>`. Usually you'll see most web developers using classes everywhere even if there is only one selector needed because it's easier to add more styles with different classes later.

Phew, that was a lot of CSS information. Let's actually color our todo list now. Inside the head tag we'll create a style tag where we put our CSS code. 

{% highlight html linenos %}
<!DOCTYPE html>
<html>
<head>
    <title>This is the title of my website!</title>
    <style>
    li {
        color: red;
    }
    .this-is-a-class-selector {
        color: blue;
    }
    #this-is-an-id-selector {
        color: green;
    }
    </style>
</head>
<body>
Why do I have so much to do...
<ul>
    <li class="this-is-a-class-selector">Write an article</li>
    <li id="this-is-an-id-selector">Write another article</li>
    <li>Write 2 more articles</li>
    <li>Read a few articles</li>
    <li>Write 3 more articles</li>
</ul>
The work never ends. :(
</body>
</html>
{% endhighlight %}

You did it! You now have a colorized todo list. :) For more cool CSS styles, just search the web for things that you want to do. e.g. css font size. Here are a few interesting ones to get you started:
* background-color
* font-family
* font-size