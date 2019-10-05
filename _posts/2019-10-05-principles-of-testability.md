---
title: "How to make your app testable?"
---
Due my experience developers usually think only about how easy it will be to develop this piece of software. 
And do not think how to test and support software afterwards. This approach usually leads to a lot of bugs found on 
testing stage and acceptance testing stage, which you may notice is not a best scenario.

And such a big amount of bugs exists not because they do not how to code, or they do not how to test. It exists because 
it takes much energy to test untestable software locally. Developers are lazy people, if they cannot run the scenario 
right inside laptop, they won't test it. Yep they will write unit tests, but as we know it is not enough. So to fix this
issue, your project should be able to run locally the whole process of business.

<b>1. Stub all external communication</b>

To achieve that goal, you should be able to run the app, right after you imported it from git repository. 

So all external calls, like communication thourgh REST with microservices, or making RPC calls, getting and posting messages using KAFKA, whatever else, it all should have stubs, preferable configurable. 

It requires a bit effort, for instance all external calls should be done via interfaces, to allow you make stubs for them. Using spring profiles you can choose implementation of such interfaces and it allows you easily make the app be ready for local development.

You may think, we will not catch integration bugs with this approach, but in order to catch them, we should define [contracts](https://nick318.github.io/2018/01/28/contracts-for-microservices). We should know exactly what we should send and what we will get as a response, if you do not have that information, anyway you will catch bugs only in a integration testing, which will take more effort than it could be.

<b>2. Make your architecture testable
</b>

If you are capable of choosing what architerture to make and libraries to use. Take in an account not only development advantages but also testing ones. If your project cannot be easily tested, it will lead to big amount of tech dept, cause it will be scary to refactor code, which is not testable. And quality of code will only decrease. Despite how good your architecture, if you cannot test it easily, you end up with "legacy" project. Your team will be dissatisfied to work for you, some bad dicisions which were made in the earlier stage, will affect you every day, and you won't have any choise to change it. 

Try to make it less couple and read about [cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)). 

<b>3. Follow test pyramid principal</b>

If you achieved two sections above, you are capable of writing different kind of tests, like unit, integration, end2end. Test pyramid described a bit [here](https://nick318.github.io/2019/01/04/a-few-donts-in-automation-testing). 

Once you wrote unit tests, do not hesitate to start writing context/integration tests. Make spring context configuration for tests, spring allows you to do any kind of tests. You can, say,  test dao layer using @DataJpaTest, it will start jpa repositories and clean the database after each test. You can make you own annotation to easily get proper test context to make writing test easily for all team members.

You can test several beans together, using external stubs describied in a first section and test the business flow. And on top of the pyramid lays end2end tests, there should be really [a few](https://nick318.github.io/2019/06/21/radical-automation-testing) ones. 

So imagine you onboard a new developer. One downloads code from vcs, opens readme file and clearly see  how to run the app. Ideally it should be as easy as click run button inside IDE with "local" profile. Try to make as less compromise here as possible. One can make adhoc testing, just clicking buttons and get first impression of the app. Then one can take a look at tests. Your tests should be executable documentation, names of the test should reflect bussiness part of the app. I prefer to use BDD style of naming, but it is not a mundatory. So after reading the test, one can run some of them, for example UI ones and understand the parts of the flow. This approafh works much better then reading 200 pages on confluence, believe me. 

Keep calm and test your code!

 