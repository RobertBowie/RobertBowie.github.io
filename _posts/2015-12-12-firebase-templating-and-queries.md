---
layout: post
title: Firebase Templating and Queries
---

<div class="message">
  Recently my team and I have been using <a href="https://www.firebase.com/">Firebase</a> as the data storage solution for a teaching platform we are developing.  This post will discuss the pitfalls found in the way we tried to structure our data and the eventual shallow approach that we landed on.
</div>



Firebase is an awesome tool that can greatly enhance your capability to develop and deploy webapps.  That being said, figuring out how to best use Firebase can be rather daunting.  The project that I have been working on has the following general requirements for data storage.

* We will be storing lessons that the user will need to access by section.
* We will need to be able to pull up any given lesson by its relative position within the overall curriculum.
* We want to be able to access any element (picture, text, code snippet etc.) within a section individually for responsive design.

Considering the above, we initially tried to go with a more deeply nested data structure.  Firebase allows you to query a node in their object-like storage and get back that node sorted by the provided key and its children like so
{% highlight js %}
var ref = new Firebase("https://example.firebaseio.com/lessons");
ref.orderByChild("section").on("value", function(snapshot) {
  snapshot.forEach(function(data) {
    console.log(data.val());
  });
});
{% endhighlight %}
if we construct our template...