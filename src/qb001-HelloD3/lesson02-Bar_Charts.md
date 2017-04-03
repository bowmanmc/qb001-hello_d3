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
http://codepen.io/QuickBits/pen/xgQWVp?editors=1010
and take a quick look. In this example, we’ll be creating a bar chart of
monthly sales data for some fictional company. The JavaScript file has an
array named salesData that is populated with some monthly aggregate sales
data. Each item in this array has a month attribute as well as a numeric
amount attribute. This array is the data that will be driving our chart.

In D3.js, for the most part, we’ll be rendering our charts using a web
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
code before, but you’ve used all of these functions before. All we’re doing
here is appending an SVG element to the chart div element and setting the
width and height of it.
