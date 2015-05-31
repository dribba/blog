---
# The title of the post.  Optional.  Extracted from the filename if not present.
title: MVC a deeper look

# Any tags for the post. Space separated.  Multi word tags can have their spaces escaped with +
tags: MVC web development pattern understanding
---

As a self-thought developer I had to, plenty of times, spend hours and hours reading about certain subject until I got that "Wow!" moment. When I first started doing web development the main pattern I kept coming across was MVC. 
We have all read about it, and understand the main idea of the pattern which is to separate the presentation layer from the business logic using controllers to mediate between them.

### Understanding the limits
One of the problems I came across lots, while either implementing or maintaining projects that used MVC, was to understand where the limits were, when code belongs to each of the layers, and one of the factor that made it difficult was that applications were too big to split into just three layers.

#### Classic MVC splitting
Most people will recommend to have most of your code on the model layer, this could be a great way to start but, problem is, that most examples about models show an object that is very close to a representation of a database row, this greatly confuses most developers thinking that the model layer should be "close to the database". This is probably the first place where things start going wrong, first of all, not all applications have or need a database, or if you put most of it in that single layer so "close to the database" you will find yourself with a 2000 lines of code file that's a maintenance nightmare, and to make it worse this is supposed to be the foundation of your application, a small mistake will cost a lot more than in any other area of the application.
The view layer is normally recommended to be as lean as possible, which could've made a lot of sense 10 years ago, but now, mostly in new web applications, we have many interactions with users just from the client itself, which obviously doesn't translate to presentation less code.
The standard for controllers is to do the rest, just tie the other two layers together, that normally doesn't result in maintainable code, even less when examples suggest to make web service calls from controllers(just because they're not database code or part of the view doesn't mean is a good place for them).

### Introducing Model-View-Controller-Component-Service-Repository
The name doesn't really matter, just think of the layers as:

* Model: All your application specific types/classes, like "Invoice", "Client", "ProductInformation". It doesn't matter if maps a database row as long as it has no database logic in it. Models shouldn't have a "save" method that you call to persist it to the database or anything alike. In JavaScript this would be a good place to put prototypes.

* View: View should still be lean, but not form code, lean form logic itself(unless is presentation logic), don't calculate or generate values unless is to avoid a AJAX call in case of JavaScript. When possible use models to represent view logic.

* Controller: Make it as thin as possible, the less logic and less code your controllers have the happier you'll be. Controllers are the point of entry of individual requests, which probably has very little of unique respect other entry points. The more logic you put on your controllers is the more you'll have to repeat it.

* Component: The layer between the controllers and the the source of data. Great place to put all the across-controllers logic. Most applications will perform service or database calls, the controller should be one that knows which one is, and the component should know how to handle it.

* Service: Will perform the calls to external services and handle the translation of service response to models or application specific objects.

* Repository: Will perform database calls and take care of persisting and retrieving data. Putting this logic here will make the application not only database agnostic, but also will make very simple the process of replacing a database with a service.


This is obviously not a one size fits all pattern, but it helps me designing the architecture of new applications.























