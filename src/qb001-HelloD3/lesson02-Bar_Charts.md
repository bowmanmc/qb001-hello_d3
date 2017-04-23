---
layout: default
title: Day 2 - Bar Charts
permalink: /courses/qb001-HelloD3/lesson02.html
---

Welcome back to the Data Visualization with D3.js course by QuickBits!
Yesterday we dipped our toe in the pool, building an HTML list of greetings
with D3. Today we’re jumping into the deep end, building an SVG bar chart.
We’ve got a bit to get through today, so let’s get started!

Open up the D3 Bar Chart pen from
[http://codepen.io/QuickBits/pen/xgQWVp?editors=1010](http://codepen.io/QuickBits/pen/xgQWVp?editors=1010)
and take a quick look. In this example, we’ll be creating a bar chart of
monthly sales data for some fictional company. The JavaScript file has an
array named salesData that is populated with some monthly aggregate sales
data. Each item in this array has a month attribute as well as a numeric
amount attribute. This array is the data that will be driving our chart.

In D3.js, for the most part, you’ll be rendering charts using a web
technology called SVG. We’ll be going into SVG in more depth later, but
for now, think of it as a way to render graphics in the browser using
markup similar to HTML. Type the following into the JavaScript (JS) editor
below the salesData variable:

{% highlight JavaScript %}
let svg = d3.select('#chart').append('svg')
    .attr('height', 200)
    .attr('width', 350);
{% endhighlight %}

This bit of code should look familiar. Not that we’ve written exactly this
code before, but you used all of these functions yesterday. All we’re doing
here is appending an SVG element to the chart div element and then setting the
width and height of it. You should now see the outline of the SVG element in red
due to a border css property.

Now we're ready build an SVG using our salesData variable. Add the following
JavaScript:

{% highlight JavaScript %}
svg.selectAll('rect')
    .data(salesData)
    .enter().append('rect')
    .attr('width', 10)
    .attr('x', (d, i) => {
        return i * 10;
    })
    .attr('height', d => {
        return d.amount;
    })
    .attr('y', 0);
{% endhighlight %}

Oh no! Our bars are upside down! Why is that? Let's look at the attributes we
set on the rect elements and see if we can figure it out.

First we set the width of the rect element to 10. With the d3 attr function, you
can set an attribute using a value, like we did here with width, or send it a
function, like we did with x on the next line. When you send it a function, it
will be called with two variables named d and i by convention. The first
argument, d, is the current element of your data array. The second argument, i,
is the index of the element in your array. So in this case, we multiply i by
10, the width of the rect element. This offsets each one so they aren't drawn
over top of each other. Things look ok here...

The next attribute we set is the height of the rectangle. Here, we simply set
the height to the amount variable in the salesData item. The reason our chart
was rendered upside down has to do with the next line, the y attribute.

SVG draws with the 0,0 coordinate in the upper left of the box. So when we set
y to 0, it starts drawing from the top of the box and goes down d.amount. To
make our chart render right-side up, change the attr call for the y attribute
to the following:

{% highlight JavaScript %}
    .attr('y', d => {
        return 200 - d.amount;
    });
{% endhighlight %}

Ok, so how is that better? Because of way SVG coordinates work, the y
attribute refers to the *top* of the rect element and goes down *height*
amount, i.e., it is "drawing down". Since we want all of the bars in our
chart to align themselves on the bottom (at logical zero), we need to subtract
the height of the bar from the height of our box and position the rect in the
y direction there.

Hopefully this is all making sense. If not, go back over the the code line by
line and then use your browser dev tools to inspect each SVG rect element and look
at the position attributes. D3 doesn't really hide the math from you, so it
might take a couple of times through to really grok what's going on.

This is as simple as it gets, but there are a few things that aren't so great
about our chart. For one, all of the bars are squished up at the beginning
of our box. A second issue is that the bars are black and it's difficult to
tell where one ends and the other starts. Let's fix the width problem first.
Change your code to the following:

{% highlight JavaScript %}
const svgHeight = 200;
const svgWidth = 350;
let svg = d3.select('#chart').append('svg')
    .attr('height', svgHeight)
    .attr('width', svgWidth);

let barWidth = svgWidth / salesData.length;

svg.selectAll('rect')
    .data(salesData)
    .enter().append('rect')
    .attr('width', barWidth)
    .attr('x', (d, i) => {
        return i * barWidth;
    })
    .attr('height', d => {
        return d.amount;
    })
    .attr('y', d => {
        return svgHeight - d.amount;
    });
{% endhighlight %}

The trick here is that we declare the width and height of our entire chart at
the beginning (svgWidth and svgHeight) and then base everything off of that.
Try changing the svgWidth variable and see how the chart stretches to fill the
svg box.
