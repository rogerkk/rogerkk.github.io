---
layout: post
title: Safari not firing focus/blur events on checkboxes
date: '2017-09-14 16:28:42 +0200'
categories: today-i-learned
---

While working on [legelisten.no](www.legelisten.no) I once wrote some javascript for handling HTML5 form validation. Today was the first time I added a checkbox to one of the forms using this code, and while testing the form I suddenly realized that the checkbox validation wasn't behaving correctly.

The reason? Safari did not fire the blur-event I was relying on when clicking the checkbox!

This is what my code looked like:

{% highlight javascript %}
form.find("input, select, textarea").on("blur focus keyup", function() {
  // Set/unset validation message
});
{% endhighlight %}

What I needed to do to get the checkbox validation working:

{% highlight javascript %}
form.find("input, select, textarea").not("input[type=checkbox]")
    .on("blur focus keyup", function() {
  // Set/unset validation message
});

form.find("input[type=checkbox]").on("click keyup", function() {
  // Set/unset validation message
});
{% endhighlight %}
