---
title: Git API v3 | developer.github.com
---

# Git DB API

The Git Database API gives you access to read and write raw Git objects
to your Git database on GitHub and to list and update your references
(branch heads and tags).

This basically allows you to reimplement a lot of Git functionality over
our API - by creating raw objects directly into the database and updating
branch references you could technically do just about anything that Git
can do without having Git installed.

![git db](http://progit.org/figures/ch9/18333fig0904-tn.png)

For more information on the Git object database, please read the 
<a href="http://progit.org/book/ch9-0.html">Git Internals</a> chapter of
the Pro Git book.

As an example, if you wanted to commit a change to a file in your
repository, you would:

* get the current commit object
* retrieve the tree it points to
* retrieve the content of the blob object that tree has for that particular file path
* change the content somehow and post a new blob object with that new content, getting a blob SHA back
* post a new tree object with that file path pointer replaced with your new blob SHA getting a tree SHA back
* create a new commit object with the current commit SHA as the parent and the new tree SHA, getting a commit SHA back
* update the reference of your branch to point to the new commit SHA

It might seem complex, but it's actually pretty simple when you understand
the model and it opens up a ton of things you could potentially do with the API.
