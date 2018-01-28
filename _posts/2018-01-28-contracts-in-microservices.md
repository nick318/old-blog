---
layout: post
title:  "Why don't you use contracts for microservice?"
date: 2018-01-28
categories: testing development
---
Microservices become more and more popular nowadays. It's obvious choice to solve problem of complexity and gives
you opportunity to support different platforms. Point about complexity should be discussed because I see 
**people do not use benefits** of microservice.

Let us remind why microservices exist in out tech world. What was the problem before microservices? Well, that is 
something from what you may be a little bit shaking. It is called -  [_monolith_](https://en.wikipedia.org/wiki/Monolithic_application).
What was the problem with monolithic applications? Here are some of them: 
All logic inside one place - which can break some piece of functionality when you develop/fix another piece. 
It is hard to test - because in order to set up test conditions, you should likely use an end-user interface.

Therefore, microservices solve all that problems because you literally divide big monolith into small pieces. But what is wrong
with people? I've seen many times people develop software, using microservices and they still work in the way of monolithic
application. What I mean here. Suppose we have 2 teams of developers. Each team develops a microservice. People do not
declare contracts of usage that service. They may discuss something, ask questions directly, but unlikely someone will make
formal description what request and response will be in the particular situation. 

What is a contract in the context of microservice? It is a declaration of what inputs are acceptable and what outputs
will be for the inputs, considering state of application. Here is an example:<br>
```Login service
General description
path signUp
method post
arguments login, password
```
```
Case Successful sign up
response 200
```
```
Case user exist
response 500
response body "User already exist"
```

I simplified it to login service but in reality it can be complex logic with many conditions. What's wrong if you don't
have such documentation? It is first sign for me, that your team does not have test double for your service. And it will
be hard for me to develop one, because logic of your service spreads across some documents and I will spend dozen hours 
to catch it. And all that means I have to use your **real service** to develop and test mine. 

Using real service leads to many problems. First, your service definitely will contain bugs. It may break my possibility
to check something in my service. Because in the middle of customer scenario you have some trouble. Second, your
service may have other dependencies, which I should resolve! It leads to hard testing. Because now in order to test some
piece of functions, I need to set-up your service, set-up third-one which is your dependency and then set-up
 test conditions of all that hell. Does it looks different from monolithic applications? Not at all.

When you don't have contracts, it's hard to realize when and how your service is changed. Changes may mentioned
in the documentation and written in business language, but for me as a developer of another service it may say nothing. 
Then I should test my service using your service because I am not sure of behavior or I will ask you directly and will
waste time.

Does it make sense?


