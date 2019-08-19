---
layout: post
title: Vertically Aligning Texts in Divs With Flexbox
category: HTML5
tags: [flexbox, vertical-align, codepen, html5]
---

I initially published this post on [Codepen](https://codepen.io/maevadevs/post/vertical-aligning-texts-in-divs-with-flexbox) but basically, this is how we do easy vertical alignement in the DOM using Flexbox.

---

## The Problem: We want to vertically align texts within a box, but HTML and CSS by themsleves cannot achieve this without much hassle and tinkering.

By default, CSS has always been good at handling text alignements over the horizontal axis of the DOM (think `text-align: center;`). However, it has always struggled to do the same over the vertical axis. Many iterations have been tried but they usually either fail to handle specific scenarios or simply too complex.

## The Solution: Embrace Flexbox!

Flexbox is like a sprinkle of magic that comes with CSS3 and fixes the long-lived problem of vertical axis of the DOM. Look at how simple this fix is now!

First, our HTML squeleton is a very simple setup.

{% highlight html %}
<!doctype html>

<html>
<head>
  <meta charset="utf-8">
  <title>Vertical Aligning with Flexbox</title>
</head>
<body>
  <div id="blue-container">
    <div id="div1" class="redbox"><span>I am centered in the middle</span></div>
    <div id="div2" class="redbox"><span>Cool! I am too!</span></div>
    <div id="div3" class="redbox"><span>And I am a longer text. See, I use the wrap effect appropriately.</span></div>
  </div>
</body>
</html>
{% endhighlight %}

Then comes the CSS where everything is setup. *The key for the alignement is `flex-direction: column` for the children `div`s. Also, `display: flex;` is required on the children to allow flexbox on the text.*

{% highlight css %}
/**
 * flex-direction: column; -- for the children divs
 * display: flex; -- Required on the children to allow flexbox on the text.
 */
div#blue-container {
  display: flex;              /* To allow horizontal centering of the children div */
  flex-direction: row;        /* Justify contents following the x-axis */
  justify-content: center;    /* Center content following flex-direction */

  /* Simple style enhancements */
  background: rgba(51, 102, 153, 1); /* Blue Div */
  height: 200px;
}
div.redbox {
  display: flex;            /* Required on the children to allow flexbox on the text */
  flex-direction: column;   /* NOTE: THIS IS THE KEY TO VERTICAL CENTERING OF TEXT */
  justify-content: center;  /* Center content following flex-direction: y-axis */
  text-align: center;       /* Center text horizontally */

  /* Simple style enhancements */
  height: inherit;          /* Full parent height */
  width: 100px;
  margin: 0px 3px;          /* No margin top-bottom. Only left-right. */
  padding: 0px 10px;        /* No padding top-bottom. Only left-right. */
  background: rgba(153, 51, 51, 1); /* Red div */
  color: white;             /* Text color */
  font-family: sans-serif;
  font-weight: 100;
  font-size: 15px;
}
{% endhighlight %}

## The End Result

<p class="codepen" data-height="306" data-theme-id="light" data-default-tab="result" data-user="maevadevs" data-slug-hash="YNzrGP" style="height: 306px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Vertical Aligning of Text in Divs with Flexbox">
  <span>See the Pen <a href="https://codepen.io/maevadevs/pen/YNzrGP/">
  Vertical Aligning of Text in Divs with Flexbox</a> by maevadevs (<a href="https://codepen.io/maevadevs">@maevadevs</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>


## Conclusion

In this minimalistic example, I demo how vertical centering with flexbox works. The most important piece is on the children element: *Make the direction of its flex into a column using `flex-direction: column;`.* After that is set, `justify-content: center;` will center the text along the y-axis. Voila!

By default, the text will automatically wrap. Check the comments on the CSS for more details.
