---
title: "How do you make your app testable?"
---
From my experience developers usually think only about how easy it will be to develop a piece of software but not how to test and support the software afterwards. This approach usually leads to a lot of bugs found in the testing and acceptance testing stages, which you might realize is not an ideal scenario.

And such a large number of bugs exists not because they do not know how to code, or because they do not how to test it, but because it takes much energy to test untestable software locally. Developers are lazy people. If they cannot run a scenario right there on their own laptop, they won't test it at all. Yep, they will write unit tests, but as we know, that is not enough. So to fix this issue, your project should be able to run locally the whole process of business.

<b>1. Stub all external communication</b>

To achieve this goal, you should be able to run the app right after you’ve imported it from the git repository. 

So all external calls, like communication through REST with microservices, or making RPC calls, getting and posting messages using KAFKA, whatever else, it all should have stubs, preferably configurable. 

It requires a bit of effort, for instance all external calls should be done via interfaces, to allow you make stubs for them. Using spring profiles you can choose the implementation of such interfaces and it allows you to easily prepare the app for local development.

You may think we will not catch integration bugs with this approach but in order to catch them, we should define [contracts](https://nick318.github.io/2018/01/28/contracts-for-microservices). We should know exactly what we should send and what we will get as a response. But if you do not have that information, you will catch bugs only in integration testing, which will take more effort than might be necessary.

<b>2. Make your architecture testable
</b>

You are capable of choosing what architecture to make and libraries to use. Take into account not only the development advantages but also the testing ones. If your project cannot be easily tested, it will lead to a lot of work for the tech dept, because it will be intimidating for the refactor code, which is not testable. And the quality of code will only deteriorate. Despite how good your architecture is, if you cannot test it easily, you end up with a "legacy" project. Your team will be dissatisfied working for you, some bad decisions which were made in the earlier stages will affect you every day, and you won't have any choice to change them. 

Try to make it less coupled and read about [cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)).

<b>3. Follow the test pyramid principal</b>

If you achieved the two sections above, you are capable of writing different kind of tests, like unit, integration, end2end. The test pyramid is described [here](https://nick318.github.io/2019/01/04/a-few-donts-in-automation-testing). 

Once you write unit tests, do not hesitate to start writing context/integration tests. Make spring context configuration for tests. Spring allows you to do any kind of tests. You can, say, test the data layer using @DataJpaTest annotation. This will start the jpa repositories and clean the database after each test. You can make you own annotation to easily get a proper test context to make writing tests easier for all team members.

You can test several beans together, using external stubs described in the first section and test the business flow. And on top of the pyramid lay end2end tests. There should be really [a few](https://nick318.github.io/2019/06/21/radical-automation-testing) of these. 

So imagine you onboard a new developer. One downloads code from VCS, opens the readme file and clearly sees how to run the app. Ideally it should be as easy as clicking a button to run inside IDE with a "local" profile. Try to avoid compromise as much as possible here. One can do adhoc testing just by clicking buttons and getting a first impression of the app. Then one can take a look at tests. Your tests should be executable documentation, names of the tests should reflect the business part of the app. I prefer to use the BDD style of naming, but it is not mandatory. So after reading the test, one can run some of them, for example UI ones, and understand the parts of the flow. This approach works much better than reading 200 pages on confluence, believe me. 

Keep calm and test your code!