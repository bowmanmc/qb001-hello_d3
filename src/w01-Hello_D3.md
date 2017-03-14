---
layout: default
title: Day 1 - Hello D3
permalink: /01.html
---

Hello! Welcome to the Data Visualization with D3.js course by
QuickBits. We’ll be spending the next two weeks exploring D3 and
building some awesome visualizations with it. We’ll start with the
basics today, but quickly move on to building actual visualizations
you can tweak, build upon, and use in your own work.

The coding samples and exercises in this course will be done using
[CodePen](http://codepen.io), an interactive playground for web
development. If you don’t already have an account, I recommend creating
one. This will allow you to save your progress and share it with your
friends.

To get our feet wet, let’s build a simple hello world type application
with D3. Open the Hello D3 pen from
[http://codepen.io/QuickBits/pen/BpqXPJ](http://codepen.io/QuickBits/pen/BpqXPJ)
and take a look. I’ve set up a
simple HTML page with a heading saying “Hello D3” along with an empty
div with the id of “message”. This pen has the D3 library already
loaded into it as well as the Bootstrap CSS framework, so we’re ready
to get coding.

In the JavaScript (JS) editor, add the following line of code:

{% highlight JavaScript %}
d3.select('#message').text('Howdy');
{% endhighlight %}

Save the pen by pressing Ctrl+S, causing the pen to execute
immediately, displaying the word “Howdy” below the page heading.
Sweet! Congratulations on writing your first D3 program!

So what happened? Let’s pull it apart a bit. The d3 select function
comes from the
[d3-selection project](https://github.com/d3/d3-selection)
and allows users to grab a set of DOM elements to manipulate
with D3. D3 selection uses the standard W3C selector strings you’re
used to using with jQuery and other libraries, so in this case,
“#message” tells D3 to select the element with the id of “message”.
Note that even though in this example we only selected a single
element, D3 selections can match many (or zero) elements on a page
and operate on them all at once. Next, we called the function text
on our selection, which sets the text contained within the element
to whatever you pass in - “howdy” in our case. This leaves us with
the following HTML displayed on the page:

{% highlight HTML %}
<div id=“message”>howdy</div>
{% endhighlight %}

Great work so far! But D3 stands for Data Driven Documents, so before
we quit for the day, let’s make something a little more data driven.
In the JavaScript (JS) editor, change the code to:

{% highlight JavaScript %}
const greetings = ['Hello', 'Hola', 'Bonjour', 'Salaam'];
d3.select('#message')
    .append('ul')
    .selectAll('li')
    .data(greetings)
    .enter()
    .append('li').text(d => {
        return d;
    });
{% endhighlight %}

This example is a little more involved, so let’s step through it line
by line.

{% highlight JavaScript %}
const greetings = ['Hello', 'Hola', 'Bonjour', 'Salaam'];
{% endhighlight %}

This line declares an array of greetings in different languages. This is using
the const keyword from ES6, letting the browser know that greetings should not
be changed. If you haven’t made the move to ES6 syntax yet, feel free to use
“var” instead.

{% highlight JavaScript %}
d3.select('#message')
{% endhighlight %}

This is our selection. The root element we’re going to be working from.

{% highlight JavaScript %}
    .append('ul')
{% endhighlight %}

This line appends a unordered list element to the messages div.

{% highlight JavaScript %}
    .selectAll('li')
{% endhighlight %}

This selection gets all of the list elements under the ul tag we just
added. “But there aren’t any list elements there yet!” I can hear you
saying. And that’s right, this syntax is a little strange, but will
make more sense as you get comfortable with the library.

{% highlight JavaScript %}
    .data(greetings)
{% endhighlight %}

This is where we bind our data to the list elements we just selected.
Remember “Data Driven Documents”.

{% highlight JavaScript %}
    .enter()
{% endhighlight %}

This line sets up the next. It is telling D3 that when a new item
appears in the variable we passed into the data() function on line 5,
we’re going to perform the following chained operation.

{% highlight JavaScript %}
    .append('li').text(d => {
        return d;
    });
{% endhighlight %}

These lines should be explained together. Since this is chained to
the enter() function, it will be called when new items are found in
our greetings array. If you remember, our initial selection of list
elements from line 4 is empty, so when this runs, this bit of code
gets called for each element of our greetings array. We append a list
element and set the text of it to the name. You may think naming a
variable “d” is bad practice, but it is a common convention in D3 code.
A variable named d usually refers to a single element in an array of
data. In this case, it will be a string object containing a greeting
from our greetings array.

Great work! You should now have an unordered list of greetings
displayed below the Hello D3 heading on your page. The output of
the JavaScript you just typed in should look like:

{% highlight HTML %}
<div id=“message”>
    <ul>
        <li>Hello</li>
        <li>Hola</li>
        <li>Bonjour</li>
        <li>Salaam</li>
    </ul>
</div>
{% endhighlight %}

Don’t worry if this isn’t totally making sense just yet. D3 syntax
and conventions can be a little strange at first, but as you use it
more and more, these conventions will save you lots of time and prove
to be powerful tools for visualizing large amounts of data with a
small amount of code.

Today you took your first steps with D3.js. You edited code using
CodePen. You created a list of HTML elements driven by an array of
data. Tomorrow we’ll start using D3 to build visualizations, starting
with a bar chart.

## Homework
Every day, you’ll have a bit of homework to help solidify the lesson
and hone your new skills. Don’t worry, your QuickBits homework will be
short, sweet, and useful!

1. Take a look at D3 pens on CodePen by searching for the term “D3”. What
types of visualizations are out there? Take a look at the code for a few
of the most interesting ones. Does any of the code look familiar to what we
wrote today?

## Further Reading
* [https://d3js.org](https://d3js.org)
* [https://github.com/d3/d3-selection](https://github.com/d3/d3-selection)
* [https://github.com/d3/d3/wiki/Gallery](https://github.com/d3/d3/wiki/Gallery)
* [https://babeljs.io/learn-es2015/](https://babeljs.io/learn-es2015/)
