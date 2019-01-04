---
title: "A few dont's in automation testing."
---

##### 1. Do not invite separate person for writing automation tests.

Assume we have a typical story. A project with 5-10 devs, testers and 2-3 analytics.
In the codebase we have small amount of unit-tests, no integration and no end2end ones.
Bug tracker is full of issues. Sounds familiar, huh?<br> 
So a project manager decides to invite one person to write automation tests. This person will never be on time with a product 
functions. Let's imagine, 5 devs work a day, and then make a build with quite big amount of changes. And only after build was done, this person
could start to write automation tests. What does it mean for a project?<br>
* Bugs were already merged into master, and we should go through a channel of bug tracker which is not fast by the way.<br>
* After some iterations, it is clearly shown, that new bugs are not found by automation tests, just because tests have to be updated.
So, it will look like you have a new build, then you run automation tests, the majority of them are failed because of requirements changes.
Then this <b>one</b> particular person makes some updates, and when tests are up to day, developers made a new one build (ha-ha), and we should start from
	the beginning.<br>

Instead, write and run automation tests right in the manufacture, while you coding, so in order to do that, you should be skillful enough to be a developer. When you run tests during coding, you find possible bugs instantly, it saves a lot of time.

##### 2. Do not separate repositories for dev and automation tests.

It will cause problems with test pyramid layers. Take a look at:
![Test pyramid](https://martinfowler.com/articles/practical-test-pyramid/testPyramid.png "Test pyramid")

copyright https://martinfowler.com/articles/practical-test-pyramid.html

If you separate it, it will force you to write mostly in end2end manner. That will cause a lot of slow tests, and devs will hardly ever run them.
Instead, make your repo testable. Include all kind of tests right inside the repo. If it's a micro-service, alright, include unit, integration and [contracts](https://nick318.github.io/2018/01/28/contracts-for-microservices) tests.<br>
If it's UI layer, fine, make it testable! You should be able to run all kind of UI tests without any back-end servers, just use mock back-end and assure what your UI sends to back-end and how the incoming data is shown.

##### 3. Do not build super framework for manual testers.

If you ignored two steps before, and decided to make kind of a tool, with help of testers could write automation tests. I am afraid to disappoint you, but look what will happen next:<br>
* Be sure the quality of tool which was written by people who are not developers is dramatically low.<br>
* Instead of learning a programming language, testers will learn your tool, so you still should teach them. After leaving your project, such people will know nothing but your tool.<br>
* The speed of writing such tests, will be slow.<br>
* Having automation tests is not a replacement for manual testing, remember it.
