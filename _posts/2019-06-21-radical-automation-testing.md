---
title: "Radical automation testing"
---
In this blog post, I will explain my thoughts about automation testing as an activity. 
What kind of activity it is, is it a role, is it a job? 

Currently in Russia and other countries as well, we have a dedicated job title, called - test automation engineer.
Actually we can clarify it as - end 2 end (e2e in the following) engineer. Because almost always they try to write e2e automation tests.
From the side nothing looks bad, but devil is in the details.

My first point is - automation testing it is not a dedicated job, we should not hire such engineers.

Let's take a look at why I think so. Automation testing almost always cannot be divided from development activity, 
and writing only e2e tests is an attempt to make such a division.. But there are a lot of technical and non-technical 
reasons why does it fail.

<b>First</b>, end2end tests is really expensive [here is why](https://nick318.github.io/2019/01/04/a-few-donts-in-automation-testing).
One example of it, suppose you have one hundred test cases, will you cover them all only on e2e level? Or you prefer 
covering based on test pyramid layers. 

If you choose first option, then you will end up with writing and re-writing such
 tests, because you will never be on time, and there will not be any profit of you. 
If you choose second option, then will you write unit and integration tests? Will you read and analyze such written tests?
Why developer should write unit and integration tests, but delegates the most technically difficult type - e2e tests, to
 people who a few month ago did not what is a compiler.
 
 You may say: there are skillful automation engineers, who can write proper code, then here is a question to them, if you
 can write code, you understand how application works, why don't you write production code and cover it in the same time? 
 Why do you need such borders, when one guy writes features, another guy writes code to test them. It is not logical.
 If you follow best practises, there should be really a few e2e tests, it does not take long time. Why do you need a person, who
 always fight with your changes of application and spend all the time to maintain tests. 
 
 <b>Second</b>, if you write code and cover it in the same time, it forces you to think about use cases, and helps you to catch bugs 
 immediately, otherwise you will catch them in a few days/weeks.
 
 <b>Third</b>, in 2019 developer can write code and tests by him/herself. And I would say, developer will do it better.
 He/She knows all modules of application, what is a mocking, knows how to write code, and can write helpers for tests. Try to ask your developer to write some
  utilities for you automation tests, I want to see this reaction. Developers do not want to do anything which is not 
  connected to their job. And when they should write tests for their code, they understand all difficulties and try to 
  make their life easier.
 
 For me this title "automation engineer" became funny, I always imagine something like unit testing engineer, and especially 
 funny to imagine title - "Lead unit testing engineer". Why don't we have them? Some companies may take this piece of advice. (sarcasm detected)
 
 So one part of development activity becomes to a dedicated job if you violate all best practises. 
 
 