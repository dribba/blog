---
# The title of the post.  Optional.  Extracted from the filename if not present.
title: Testing AMD modules

# Any tags for the post. Space separated.  Multi word tags can have their spaces escaped with +
tags: JavaScript modules AMD testing TDD BDD Karma Jasmine
---

I have been working a lot in JavaScript unit testing lately, using Karma and Jasmine to be more specific.
One of the biggest challenges is to deal with AMD modules, and sometimes is even hard to find help because it depends on the project setup, but something is for sure, the default configuration that Karma builds in not enough for most cases.
I assume that you know what Unit Testing is and how to setup Karma+Jasmine, if not there's a lot of blog posts about it or even a [very short course](https://www.udacity.com/course/ud549 "Udacity - JavaScript Testing").


=== What do you get for free ===

The default settings that Karma generates for a Jasmine+RequireJS test suit will be, first of all the configuration for Karma itself, from where the most important piece we can take is:

```js
files: [
	'test-main.js',
	{pattern: 'js/**/*.js', included: false},
	{pattern: 'test/**/*Spec.js', included: false}
],
```