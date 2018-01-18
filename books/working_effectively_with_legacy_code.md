# Working Effectively With Legacy Code

## Foreword by Robert C. Martin

But the joy I felt soon became tempered by the realization that software systems almost always degrade into a mess. What starts as a clean crystalline design in the minds of the programmers rots, over time, like a piece of bad meat. The nice little system we built last year turns into a horrible morass of tangled functions and variables next year. 
Why does this happen? Why do systems rot? Why can’t they stay clean? 
Sometimes we blame our customers. Sometimes we accuse them of changing the requirements. We comfort ourselves with the belief that if the customers had just been happy with what they said they needed, the design would have been fine. It’s the customer’s fault for changing the requirements on us. 
Well, here’s a news flash: *Requirements change*. Designs that cannot tolerate changing requirements are poor designs to begin with. It is the goal of every competent software developer to create designs that tolerate change. 
This seems to be an intractably hard problem to solve. So hard, in fact, that nearly every system ever produced suffers from slow, debilitating rot. The rot is so pervasive that we’ve come up with a special name for rotten programs. We call them: **Legacy Code**. 

Prevention is imperfect. Even the most disciplined development team, knowing the best principles, using the best patterns, and following the best practices will create messes from time to time. The rot still accumulates. It’s not enough to try to prevent the rot — you have to be able to reverse it. 

## Preface

Code without tests is bad code. It doesn’t matter how well written it is; it doesn’t matter how pretty or object-oriented or well-encapsulated it is. With tests, we can change the behavior of our code quickly and verifiably. Without them, we really don’t know if our code is getting better or worse. 

Teams take serious chances when they try to make large changes without tests. It is like doing aerial gymnastics without a net. It requires incredible skill and a clear understanding of what can happen at every step. 

## Introduction

# Part I: The Mechanics of Change

## Chapter 1: Changing Software

### Four Reasons to Change Software

For simplicity’s sake, let’s look at four primary reasons to change software.
1. Adding a feature 
2. Fixing a bug
3. Improving the design
4. Optimizing resource usage 

### Adding Features and Fixing Bugs

Behavior is the most important thing about software. It is what users depend on. Users like it when we add behavior (provided it is what they really wanted), but if we change or remove behavior they depend on (introduce bugs), they stop trusting us.

It seems nearly impossible to add behavior without changing it to some degree. 

### Improving Design

The act of improving design without changing its behavior is called refactoring. 

Refactoring differs from general cleanup in that we aren’t just doing low-risk things such as reformatting source code, or invasive and risky things such as rewriting chunks of it. Instead, we are making a series of small structural modifications, supported by tests to make the code easier to change. The key thing about refactoring from a change point of view is that there aren’t supposed to be any functional changes when you refactor (although behavior can change somewhat because the structural changes that you make can alter performance, for better or worse). 

### Optimization

### Putting It All Together

Preserving existing behavior is one of the largest challenges in software development. Even when we are changing primary features, we often have very large areas of behavior that we have to preserve. 

 . | Adding a Feature | Fixing a Bug | Refactoring | Optimizing
 -- | -- | -- | -- | --
 Structure | Changes | Changes | Changes | --
 New Functionality | Changes | -- | -- | --
 Functionality | -- | Changes | -- | --
 Resource Usage | -- | --| -- | Changes

To mitigate risk, we have to ask three questions: 
1. What changes do we have to make?
2. How will we know that we’ve done them correctly?
3. How will we know that we haven’t broken anything? 

## Chapter 2: Working with Feedback

Changes in a system can be made in two primary ways. I like to call them **Edit and Pray** and **Cover and Modify**. Unfortunately, *Edit and Pray* is pretty much the industry standard. When you use *Edit and Pray*, you carefully plan the changes you are going to make, you make sure that you understand the code you are going to modify, and then you start to make the changes. When you’re done, you run the system to see if the change was enabled, and then you poke around further to make sure that you didn’t break anything. The poking around is essential. When you make your changes, you are hoping and praying that you’ll get them right, and you take extra time when you are done to make sure that you did. 
Superficially, *Edit and Pray* seems like “working with care,” a very professional thing to do. The “care” that you take is right there at the forefront, and you expend extra care when the changes are very invasive because much more can go wrong.

 But safety isn’t solely a function of care. I don’t think any of us would choose a surgeon who operated with a butter knife just because he worked with care. Effective software change, like effective surgery, really involves deeper skills. Working with care doesn’t do much for you if you don’t use the right tools and techniques. 

*Cover and Modify* is a different way of making changes. The idea behind it is that it is possible to work with a *safety net* when we change software. The safety net we use isn’t something that we put underneath our tables to catch us if we fall out of our chairs. Instead, it’s kind of like a cloak that we put over code we are working on to make sure that bad changes don’t leak out and infect the rest of our software. Covering software means covering it with tests. When we have a good set of tests around a piece of code, we can make changes and find out very quickly whether the effects were good or bad. We still apply the same care, but with the feedback we get, we are able to make changes more carefully. 

When we have tests that detect change, it is like having a vise around our code. The behavior of the code is fixed in place. When we make changes, we can know that we are changing only one piece of behavior at a time. In short, we’re in control of our work. 

Unit testing is one of the most important components in legacy code work. System-level regression tests are great, but small, localized tests are invaluable. They can give you feedback as you develop and allow you to refactor with much more safety. 

### What Is Unit Testing?

Large test problems: Error localization, Execution Time, Coverage

Here are qualities of good unit tests: 
1. They run fast. 
2. They help us localize problems. 

A unit test that takes 1/10th of a second to run is a slow unit test. 

Unit tests run fast. If they don’t run fast, they aren’t unit tests.

Other kinds of tests often masquerade as unit tests. A test is not a unit test if: 		
1. It talks to a database. 
2. It communicates across a network. 
3. It touches the file system. 
4. You have to do special things to your environment (such as editing configuration files) to run it.

Tests that do these things aren’t bad. Often they are worth writing, and you generally will write them in unit test harnesses. However, it is important to be able to separate them from true unit tests so that you can keep a set of tests that you can run fast whenever you make changes. 

### Higher-Level Testing

Unit tests are great, but there is a place for higher-level tests, tests that cover scenarios and interactions in an application. Higher-level tests can be used to pin down behavior for a set of classes at a time. When you are able to do that, often you can write tests for the individual classes more easily. 

### Test Coverings

Dependency is one of the most critical problems in software development. Much legacy code work involves breaking dependencies so that changes can be easier.

*The Legacy Code Dilemma*: When we change code, we should have tests in place. To put tests in place, we often have to change.

When you break dependencies in legacy code, you often have to suspend your sense of aesthetics a bit. Some dependencies break cleanly; others end up looking less than ideal from a design point of view. They are like the incision points in surgery: There might be a scar left in your code after your work, but everything beneath it can get better. 
If later you can cover code around the point where you broke the dependencies, you can heal that scar, too. 

### The Legacy Code Change Algorithm

1. Identify change points
2. Find test points
3. Break dependencies
4. Write tests
5. Make changes and refactor

## Chapter 3: Sensing and Separation

Generally, when we want to get tests in place, there are two reasons to break dependencies: *sensing* and *separation*. 

1. **Sensing** — We break dependencies to sense when we can’t access values our code computes. 
2. **Separation** — We break dependencies to separate when we can’t even get a piece of code into a test harness to run. 

### Faking Collaborators

A **fake object** is an object that impersonates some collaborator of your class when it is being tested. 

Sometimes when people see the use of fake objects, they say, “That’s not really testing.” After all, this test doesn’t show us what really gets displayed on the real screen. Suppose that some part of the cash register display software isn’t working properly; this test would never show it. Well, that’s true, but that doesn’t mean that this isn’t a real test. Even if we could devise a test that really showed us exactly which pixels were set on a real cash register display, does that mean that the software would work with all hardware? No, it doesn’t — but that doesn’t mean that that isn’t a test, either. When we write tests, we have to divide and conquer. This test tells us how `Sale` objects affect displays, that’s all. But that isn’t trivial. If we discover a bug, running this test might help us see that the problem isn’t in `Sale`. If we can use information like that to help us localize errors, we can save an incredible amount of time. 

When we write tests for individual units, we end up with small, well-understood pieces. This can make it easier to reason about our code. 

**Mock objects** are fakes that perform assertions internally.

## Chapter 4: The Seam Model

### A Huge Sheet of Text

Superficially, that is all true, but what about modularity? We are often told it is better to write programs that are made of small reusable pieces, but how often are small pieces reused independently? Not very often. Reuse is tough. Even when pieces of software look independent, they often depend upon each other in subtle ways. 

### Seams

A **seam** is a place where you can alter behavior in your program without editing in that place. 

One of the biggest challenges in getting legacy code under test is breaking dependencies. When we are lucky, the dependencies that we have are small and localized; but in pathological cases, they are numerous and spread out throughout a code base. The seam view of software helps us see the opportunities that are already in the code base. If we can replace behavior at seams, we can selectively exclude dependencies in our tests. We can also run other code where those dependencies were if we want to sense conditions in the code and write tests against those conditions. Often this work can help us get just enough tests in place to support more aggressive work. 

### Seam types

**Preprocessing Seams**, **Link Seams**, **Object Seams**

Every seam has an enabling point, a place where you can make the decision to use one behavior or another.

If you use link seams, make sure that the difference between test and production environments is obvious.

Isn’t this all rather indirect? If we don’t like a dependency, why don’t we just go into the code and change it? Sometimes that works, but in particularly nasty legacy code, often the best approach is to do what you can to modify the code as little as possible when you are getting tests in place. If you know the seams that your language offers and how to use them, you can often get tests in place more safely than you could otherwise. 

It is important to choose the right type of seam when you want to get pieces of code under test. In general, *object seams* are the best choice in object-oriented languages. *Preprocessing seams* and *link seams* can be useful at times but they are not as explicit as *object seams*. In addition, tests that depend upon them can be hard to maintain. I like to reserve *preprocessing seams* and *link seams* for cases where dependencies are pervasive and there are no better alternatives. 
When you get used to seeing code in terms of seams, it is easier to see how to test things and to see how to structure new code to make testing easier. 

## Chapter 5: Tools

### Automated Refactoring Tools

**refactoring** (n.). A change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its existing behavior. 

### Mock Objects

### Unit-Testing Harnesses

In fairness to tool vendors, testing is a tough problem, and people are often seduced by the idea that they can test through a GUI or web interface without having to do anything special to their application. It can be done, but it is usually more work than anyone on a team is prepared to admit. In addition, a user interface often isn’t the best place to write tests. UIs are often volatile and too far from the functionality being tested. When UI-based tests fail, it can be hard to figure out why. Regardless, people often spend considerable money trying to do all of their testing with those sorts of tools. 

### General Test Harnesses

# Part II: Changing Software

## Chapter 6: I Don’t Have Much Time and I Have to Change It

Remember, code is your house, and you have to live in it. 

### Sprout Method

Temporaries aren’t necessarily bad, but sometimes they attract new code. If the next change that we have to make involves work with all non-duplicated entries before they are added, well, there is only one place in the code that a variable like that exists: right in this method. It will be tempting to just put that code in the method also. 

That was an example of **Sprout Method**. Here are the steps that you actually take: 
1. Identify where you need to make your code change. 
2. If the change can be formulated as a single sequence of statements in one place in a method, write down a call for a new method that will do the work involved and then comment it out. (I like to do this before I even write the method so that I can get a sense of what the method call will look like in context.) 
3. Determine what local variables you need from the source method, and make them arguments to the call.
4. Determine whether the sprouted method will need to return values to source method. If so, change the call so that its return value is assigned to a variable. 
5. Develop the sprout method using *test-driven development*. 
6. Remove the comment in the source method to enable the call. 

I recommend using *Sprout Method* whenever you can see the code that you are adding as a distinct piece of work or you can’t get tests around a method yet. It is far preferable to adding code inline. 

### Sprout Class

Here are the steps for **Sprout Class**:
1. Identify where you need to make your code change. 
2. If the change can be formulated as a single sequence of statements in one place in a method, think of a good name for a class that could do that work. Afterward, write code that would create an object of that class in that place, and call a method in it that will do the work that you need to do; then comment those lines out. 
3. Determine what local variables you need from the source method, and make them arguments to the classes’ constructor. 
4. Determine whether the sprouted class will need to return values to the source method. If so, provide a method in the class that will supply those values, and add a call in the source method to receive those values. 
5. Develop the sprout class test first.
6. Remove the comment in the source method to enable the object creation and calls. 

### Wrap Method

When you group things together just because they have to happen at the same time, the relationship between them isn’t very strong. Later you might find that you have to do one of those things without the other, but at that point they might have grown together. 

Here are the steps for the first version of the **Wrap Method**: 
1. Identify a method you need to change. 
2. If the change can be formulated as a single sequence of statements in one place, rename the method and then create a new method with the same name and signature as the old method. Remember to *Preserve Signatures* as you do this. 
3. Place a call to the old method in the new method.
4. Develop a method for the new feature, test first (see *test-driven development*), and call it from the new method.

In the second version, when we don’t care to use the same name as the old method, the steps look like this:
1. Identify a method you need to change. 
2. If the change can be formulated as a single sequence of statements in one place, develop a new method for it using *test-driven development*. 
3. Create another method that calls the new method and the old method. 

### Wrap Class

Navigating through code that contains decorators that decorate other decorators is a lot like peeling away the layers of an onion. It is necessary work, but it does make your eyes water. 

Here are the steps for **Wrap Class**:
1. Identify a method where you need to make a change. 
2. If the change can be formulated as a single sequence of statements in one place, create a class that accepts the class you are going to wrap as a constructor argument. If you have trouble creating a class that wraps the original class in a test harness, you might have to use Extract Implementer or Extract Interface on the wrapped class so that you can instantiate your wrapper. 
3. Create a method on that class, using test-driven development, that does the new work. Write another method that calls the new method and the old method on the wrapped class. 
4. Instantiate the wrapper class in your code in the place where you need to enable the new behavior.

At that point, when you feel the difference between good code and bad code in your gut, you are a changed person. You might even find yourself wanting to refactor far in excess of what you need to get the job done, just to make your life easier. 

### Summary

## Chapter 7: It Takes Forever to Make a Change

### Understanding

Systems that are broken up into small, well-named, understandable pieces enable faster work. 

### Lag Time

**Lag time** is the amount of time that passes between a change that you make and the moment that you get real feedback about the change. 

It seems ridiculously inefficient, right? Yet, when you think about it, that is exactly the way most of us work right now when we develop software. We make some changes, start a build, and then find out what happened later. Unfortunately, we don’t have software that knows how to navigate around obstacles in the build, things such as test failures. What we try to do instead is bundle a bunch of changes and make them all at once so that we don’t have to build too often. If our changes are good, we move along, albeit as slow as the Mars rover. If we hit an obstacle, we go even slower. 

People who program in interpreted languages can often get near-instantaneous feedback when they work. For the rest of us, who work in compiled languages, the main impediment is dependency, the need to compile something that we don’t care about just because we want to compile something else. 

### Breaking Dependencies

When your code depends on an interface, that dependency is usually very minor and unobtrusive. Your code doesn’t have to change unless the interface changes, and interfaces typically change far less often than the code behind them. When you have an interface, you can edit classes that implement that interface or add new classes that implement the interface, all without impacting code that uses the interface. 
For this reason, it is better to depend on interfaces or abstract classes than it is to depend on concrete classes. When you depend on less volatile things, you minimize the chance that particular changes will trigger massive recompilation. 

When you introduce more interfaces and packages into your design to break dependencies, the amount of time it takes to rebuild the entire system goes up slightly. There are more files to compile. But the average time for a make, a build based on what needs to be recompiled, can go down dramatically. 

When you start to optimize your average build time, you end up with areas of code that are very easy to work with. It might be a bit of a pain to get a small set of classes compiling separately and under test, but the important thing to remember is that you have to do it only once for that set of classes; afterward, you get to reap the benefits forever. 

### Summary

## Chapter 8: How Do I Add a Feature?

We can use the techniques described there (sprouting and wrapping) to add to code without tests, but there are some hazards aside from the obvious ones. For one thing, when we sprout or wrap, we don’t significantly modify the existing code, so it isn’t going to get any better for a while. Duplication is another hazard. If the code that we add duplicates code that exists in the untested areas, it might just lie there and fester. Worse, we might not realize that we are going to have duplication until we get far along making our changes. The last hazards are fear and resignation: fear that we can’t change a particular piece of code and make it easier to work with, and resignation because whole areas of the code just aren’t getting any better. Fear gets in the way of good decision making. The sprouts and wraps left in the code are little reminders of it. 

### Test-Driven Development (TDD)

The most powerful feature-addition technique I know of is **test-driven development (TDD)**.

*Test-driven development* uses a little algorithm that goes like this: 
1. Write a failing test case. 
2. Get it to compile.
3. Make it pass.
4. Remove duplication.
5. Repeat. 

One of the most valuable things about TDD is that it lets us concentrate on one thing at a time. We are either writing code or refactoring; we are never doing both at once. 
That separation is particularly valuable in legacy code because it lets us write new code independently of old code. 
After we have written some new code, we can refactor to remove any duplication between it and the old code. 

### Programming by Difference

There are many powerful refactorings, but Rename Class is the most powerful. It changes the way people see code and lets them notice possibilities that they might not have considered before. 

Objects of subclasses should be substitutable for objects of their superclasses throughout our code. If they aren’t we could have silent errors in our code. 

The **LSP** implies that clients of a class should be able to use objects of a subclass without having to know that they are objects of a subclass. There aren’t any mechanical ways to completely avoid LSP violations. Whether a class is LSP conformant depends upon the clients that it has and what they expect. However, some rules of thumb help: 
1. Whenever possible, avoid overriding concrete methods. 
2. If you do, see if you can call the method you are overriding in the overriding method. 

I call this sort of hierarchy a normalized hierarchy. In a normalized hierarchy, no class has more than one implementation of a method. In other words, none of the classes has a method that overrides a concrete method it inherited from a superclass. When you ask the question “How does this class do X?” you can answer it by going to class X and looking. Either the method is there or it is abstract and implemented in one of the subclasses. In a normalized hierarchy you don’t have to worry about subclasses overriding behavior they inherited from their superclasses. 

*Programming by Difference* lets us introduce variations quickly in systems. When we do, we can use our tests to pin down the new behavior and move to more appropriate structures when we need to. Tests can make the move very rapid. 

### Summary

## Chapter 9: I Can’t Get This Class into a Test Harness

Here are the four most common problems we encounter: 
1. Objects of the class can’t be created easily. 
2. The test harness won’t easily build with the class in it.
3. The constructor we need to use has bad side effects.
4. Significant work happens in the constructor, and we need to sense it. 

### The Case of the Irritating Parameter

The best way to see if you will have trouble instantiating a class in a test harness is to just try to do it. Write a test case and attempt to create an object in it. The compiler will tell you what you need to make it really work. 

In this case, the best way to make a fake object is to use *Extract Interface* on the `RGHConnection` class. If you have a tool with refactoring support, chances are good that it supports *Extract Interface*. If you don’t have a tool that supports *Extract Interface*, remember that it is easy enough to do by hand.

Test code doesn’t have to live up to the same standards as production code. In general, I don’t mind breaking encapsulation by making variables public if it makes it easier to write tests. However, test code should be clean. It should be easy to understand and change. 

The way people react to lines of code like that often says a lot about the kind of system they work on. 

When you are writing tests and an object requires a parameter that is hard to construct, consider just passing null instead. If the parameter is used in the course of your test execution, the code will throw an exception and the test harness will catch the exception. If you need behavior that really requires an object, you can construct it and pass it as a parameter at that point. 

The important thing to remember is this: Don’t pass null in production code unless you have no other choice. 

The **Null Object Pattern** is a way of avoiding the use of null in programs.

We could just decide to throw an exception so that we don’t have to return anything, but that would force clients to deal with the error explicitly. We could also return `null`, but then clients would have to check for null explicitly.
There is a third alternative. Does the previous code really care whether there is an employee to pay? Does it have to? What if we had a class called `NullEmployee`? An instance of `NullEmployee` has no name and no address, and when you tell it to pay, it just does nothing. 
Null objects can be useful in contexts like this; they can shield clients from explicit error checking. As nice as null objects are, you have to be cautious when you use them.
Null objects are useful specifically when a client doesn’t have to care whether an operation is successful. In many cases, we can finesse our design so that this is the case.

*Pass Null* and *Extract Interface* are two ways of approaching irritating parameters. But another alternative can be used at times. If the problematic dependency in a parameter isn’t hard-coded into its constructor, we can use *Subclass and Override Method* to get rid of the dependency. That could be possible in this case. If the constructor of `RGHConnection` uses its connect method to form a connection, we could break the dependency by overriding `connect()` in a testing subclass. *Subclass and Override Method* can be a very useful way of breaking dependencies, but we have to be sure that we aren’t altering the behavior we want to test when we use it. 

### The Case of the Hidden Dependency

Some classes are deceptive. We look at them, we find a constructor that we want to use, and we try to call it. Then, bang! We run into an obstacle. One of the most common obstacles is **hidden dependency**; the constructor uses some resource that we just can’t access nicely in our test harness.

One of the techniques we can use is *Parameterize Constructor*. With this technique, we externalize a dependency that we have in a constructor by passing it into the constructor.

*Parameterize Constructor* is a very convenient way to externalize constructor dependencies, but people don’t think of it very often. One of the stumbling blocks is that people often assume that all clients of the class will have to be changed to pass the new parameter, but that isn’t true. We can handle it like this. First we extract the body of the constructor into a new method that we can call initialize. Unlike most method extractions, this one is pretty safe to attempt without tests because we can *Preserve Signatures* as we do it.
Now we can supply a constructor that has the original signature. Tests can call the constructor parameterized by `mail_service`, and clients can call this one. They don’t need to know that anything has changed. 

Dependencies hidden in constructors can be tackled with many techniques. Often we can use *Extract and Override Getter*, *Extract and Override Factory Method*, and *Supersede Instance Variable*, but I like to use Parameterize Constructor as often as I can. When an object is created in a constructor and it doesn’t have any construction dependencies itself, Parameterize Constructor is a very easy technique to apply. 

### The Case of the Construction Blob

Functions in derived classes often assume that they can use variables from their base class. Until the constructor of the base class is completely finished, there is a chance that an overridden function that it calls can access an uninitialized variable.

I don’t like to use *Supersede Instance Variable* unless I can’t avoid it. The potential for resource-management problems is too great. However, I do use it in C++ at times. Often I’d like to use Extract and Override Factory Method, and we can’t do that in C++ constructors. For that reason, I use *Supersede Instance Variable* occasionally. 

### The Case of the Irritating Global Dependency

For years in the software industry, people have bemoaned the fact that there aren’t more reusable components on the market. It’s getting better over time; there are plenty of commercial and open-source frameworks, but in general, many of them are not really things that we use; they are things that use our code. Frameworks often manage the lifecycle of an application, and we write code to fill in the holes. We can see this in all sorts of frameworks, from ASP.NET to Java Struts. Even the xUnit frameworks behave this way. We write test classes; xUnit calls them and displays their results. 
Frameworks solve many problems, and they do give us a boost when we start projects, but this isn’t the kind of reuse that people really expected early on in software development. Old-style reuse happens when we find some class or set of classes that we want to use in our application and we just do it. We just add them to a project and use them. It would be nice to be able to do this routinely, but frankly, I think we are kidding ourselves even thinking about that sort of reuse if we can’t pull a random class out of an average application and compile it independently in a test harness without doing a lot of work (grumble, grumble). 

We know that an account object can affect things that we pass into the `Account` constructor, but we aren’t passing anything in. `Account` objects can also affect objects that we pass as parameters to methods, but in this case, we aren’t passing anything in that can be changed — it’s just an `int`. Here we are assigning the return value of `getBalance` to a variable, and that is really the only value that should be affected by this set of statements. 
When we use global variables, this situation is turned upside down. We can look at the use of a class such as `Account` and not have a clue whether it is accessing or modifying variables declared someplace else in the program. Needless to say, this can make it harder to understand programs. 

Why do we want only one instance of a class in a system? The answer varies depending on the system, but here are some of the most common answers: 
1. We are modeling the real world, and there is only one of these things in the real world. 
2. If two of these things are created, we could have a serious problem. 
3. If someone creates two of these things, we’ll be using too many resources. 

The name for this whole refactoring is *Introduce Static Setter*. This is a technique that we can use to get tests in place despite extensive global dependencies. Unfortunately, it doesn’t do much to get past the global dependencies. If you choose to tackle that problem, you can do so by using *Parameterize Method* and *Parameterize Constructor*. With those refactorings, you trade a global reference for either a temporary variable in a method or a field in an object. The downside to *Parameterize Method* is that you can end up with many additional methods that distract people when they try to understand the classes. The downside to *Parameterize Constructor* is that each object that currently uses the global ends up with an additional field. The field will have to be passed to its constructor, so the class that creates the object needs to have access to the instance also. If too many objects need this additional field, it can substantially impact the amount of memory used by the application, but often that indicates other design problems. 

### The Case of the Horrible Include Dependencies

One part of C++’s C legacy that is especially problematic is its way of letting one part of a program know about another part. In Java and C#, if a class in one file needs to use a class in another file, we use an import or using statement to make its definition available. The compiler looks for that class and checks to see if it has been compiled already. If it hasn’t, it compiles it. If it has been compiled, the compiler reads a brief snippet of information from the compiled file, getting only as much information as it needs to make sure that all of the methods the original class needs are on that class. 
C++ compilers generally don’t have this optimization. In C++, if a class needs to know about another class, the declaration of the class (in another file) is textually included in the file that needs to use it. This can be a much slower process. The compiler has to reparse the declaration and build up an internal representation every time it sees that declaration. Worse, the include mechanism is prone to abuse. A file can include a file that includes a file, and so on. On projects in which people haven’t avoided this, it’s not uncommon to find small files that end up transitively including tens of thousands of lines of code. People wonder why their builds take so long, but because the includes are spread around the system, it is hard to point at any one particular file and understand why it is taking so long to compile. 

### The Case of the Onion Parameter

If we discover that we need more objects to create `Schedulers` and `MeetingResolvers`, we’re liable to pull our hair out. The only thing that keeps us from total despair is the fact that there has to be at least one class that doesn’t require objects of another class as arguments. If there isn’t, there is no way the system could ever have compiled. 
The way to handle this situation is to take a close look at what we want to do. We need to write tests, but what do we really need from the parameters passed into the constructor? If we don’t need anything from them in the tests, we can *Pass Null*. If we just need some rudimentary behavior, we can use *Extract Interface* or *Extract Implementer* on the most immediate dependency and use the interface to create a fake object. In this case, the most immediate dependency of `SchedulingTaskPane` is `SchedulingTask`. If we can create a fake `SchedulingTask`, we can create a `SchedulingTaskPane`. 

In any language where we can create interfaces or classes that act like interfaces, we can systematically use them to break dependencies. 

### The Case of the Aliased Parameter

Interfaces are great for breaking dependencies, but when we get to the point that we have nearly a one-to-one relationship between classes and interfaces, the design gets cluttered.

In many languages, we can create classes “on the fly” like this in methods. Although I don’t like to do it often in production code, it is very convenient when we are testing. We can make special cases very easily. 
*Subclass and Override Method* helps us break dependencies on parameters, but sometimes the factoring of methods in a class isn’t ideal for it. We were lucky that the dependencies we didn’t like were isolated in that validate method. In worse cases, they are intermingled with logic that we need, and we have to extract methods first. If we have a refactoring tool, that can be easy. 

## Chapter 10: I Can’t Run This Method in a Test Harness

Instantiating a class is often only the first part of the battle. The second part is writing tests for the methods we need to change. Sometimes we can do this without instantiating the class at all. If the method doesn’t use much instance data, we can use *Expose Static Method* to get access to the code. If the method is pretty long and difficult to deal with, we can use *Break Out Method Object* to move the code to a class that we can instantiate more easily. 
Fortunately, in most cases, the amount of work that we have to do to write tests for methods isn’t as drastic. Here are some of the problems that we can run into.

* The method might not be accessible to the test. It could be private or have some other accessibility problem. 
* It might be hard to call the method because it is hard to construct the parameters we need to call it. 
* The method might have bad side effects (modifying a database, launching a cruise missile, and so on), so it is impossible to run in a test harness. 
* We might need to sense through some object that the method uses. 

### The Case of the Hidden Method

So, how do we write a test for a private method? This has to be one of the most common testing-related questions. Fortunately, there is a very direct answer for this question: If we need to test a private method, we should make it public. If making it public bothers us, in most cases, it means that our class is doing too much and we ought to fix it. Let’s look at the cases. Why would making a private method public bother us? Here are some reasons: 
1. The method is just a utility; it isn’t something clients would care about. 
2. If clients use the method, they could adversely affect results from other methods on the class. 
The first reason isn’t very severe. An extra public method in a class’s interface is forgivable, although we should try to figure out whether it would be better to put the method on another class. The second reason is a bit more serious, but fortunately there is a remedy: The private methods can be moved to a new class. They can be public on that class and our class can create an internal instance of it. That makes the methods testable and the design better.

The fact remains: Good design is testable, and design that isn’t testable is bad. 

In many OO languages newer than C++, we can use reflection and special permissions to access private variables at runtime. Although that can be handy, it is a bit of a cheat, really. It is very helpful when we want to break dependencies, but I don’t like to keep tests that access private variables around in projects. That sort of subterfuge really prevents a team from noticing just how bad the code is getting. It might sound kind of sadistic, but the pain that we feel working in a legacy code base can be an incredible impetus to change. We can take the sneaky way out, but unless we deal with the root causes, overly responsible classes and tangled dependencies, we are just delaying the bill. When everyone discovers just how bad the code has gotten, the costs to make it better will have gotten too ridiculous. 

### The Case of the “Helpful” Language Feature

Seriously, it is easy to believe that *sealed* and *final* are a wrong-headed mistake, that they should never have been added to programming languages. But the real fault lies with us. When we depend directly on libraries that are out of our control, we are just asking for trouble. 
Some day, mainstream programming languages might provide special access permissions for tests, but in the meantime, it is good to use mechanisms such as sealed and final sparingly. And when we need to use library classes that use them, it’s a good idea to isolate them behind some wrapper so that we have some wiggle room when we make our changes.

### The Case of the Undetectable Side Effect

Now we can extract the code that uses that frame into a set of methods. What should we name the methods? To get ideas for names, we should take a look at what each piece of code does from the perspective of this class, or what it calculates for this class. In addition, we should not use names that deal with the display components. We can use display components in the code that we extract, but the names should hide that fact. With these things in mind, we can create either a command method or a query method for each chunk of code. 

**Command/Query Separation** is a design principle first described by Bertrand Meyer. Simply put, it is this: A method should be a command or a query, but not both. A command is a method that can modify the state of the object but that doesn’t return a value. A query is a method that returns a value but that does not modify the object.

Why is this principle important? There are a number of reasons, but the most primary is communication. If a method is a query, we shouldn’t have to look at its body to discover whether we can use it several times in a row without causing some side effect.

The steps we took in this example are very common. When we have a refactoring tool, we can easily extract methods on a class and then start to identify groups of methods that can be moved to new classes. A good refactoring tool will only allow you to do an automated extract method refactoring when it is safe. However, that just makes the editing that we do between uses of the tool the most hazardous part of the work. Remember that it is okay to extract methods with poor names or poor structure to get tests in place. Safety first. After the tests are in place, you can make the code much cleaner.

## Chapter 11: I Need to Make a Change. What Methods Should I Test?

### Reasoning About Effects

If your code is well structured, most of the methods in your software have simple effect structures. In fact, one measure of goodness in software is that rather complicated effects on the outside world are the sum of a much simpler set of effects in the code. Almost anything that you can do to make the effect sketch simpler for a piece of code makes it more understandable and maintainable. 

In programs that aren’t written very well, we often find it very difficult to figure out why the results we are looking at are what they are. When we are at that point, we have a debugging problem and we have to reason backward from the problem to its source. When we are working with legacy code, we often have to ask a different question: If we make a particular change, how could it possibly affect the rest of the results of the program? 
This involves reasoning forward from points of change. When you get a good handle on this sort of reasoning, you have the beginnings of a technique for finding good places to write tests. 

### Reasoning Forward

When you are sketching effects, make sure that you have found all of the clients of the class you are examining. If your class has a superclass or subclasses, there might be other clients that you haven’t considered.

We need to find places to test, and the first step is figuring out where change can be detected: what the effects of the change are. When we know where we can detect effects, we can pick and choose among them when we write our tests. 

### Effect Propagation

Effects can also propagate in silent, sneaky ways. If we have an object that accepts some object as a parameter, it can modify its state, and the change is reflected back into the rest of the application.

Effects propagate in code in three basic ways:
1. Return values that are used by a caller
2. Modification of objects passed as parameters that are used later
3. Modification of static or global data that is used later

Some languages provide additional mechanisms. For instance, in aspect-oriented languages, programmers can write constructs called aspects that affect the behavior of code in other areas of the system. 

### Tools for Effect Reasoning

The most important tool that we have in our arsenal is knowledge of our programming language. In every language, there are little “firewalls,” things that prevent effect propagation. If we know what they are, we know that we don’t have to look past them. 

Know your language.

### Learning from Effect Analysis

Try to analyze effects in code whenever you get a chance. Sometimes you will notice that as you get very familiar with a code base, you feel that you don’t have to look for certain things. When you feel that way, you’ve found some “basic goodness” in your code base. In the best code, there aren’t many “gotchas.” Some “rules” embodied in the code base, whether they are explicitly stated or not, prevent you from having to be paranoid as you look for possible effects. The best way to find these rules is to think of a way that a piece of software could have an effect on another, a way that you’ve never seen in the code base. Then say to yourself, “But, no, that would be stupid.” When your code base has a lot of rules like that, it is far easier to deal with. In bad code, people don’t know what the “rules” are, or the “rules” are littered with exceptions.

In general, programming gets easier as we narrow effects in a program. We need to know less to understand a piece of code. At the extreme, we end up with functional programming in languages such as Scheme and Haskell. Programs can actually be very easy to understand in those languages, but those languages aren’t in widespread use. Regardless, in OO languages, restricting effects can make testing much easier, and there aren’t any hurdles to doing it.

### Simplifying Effect Sketches

When we remove tiny pieces of duplication, we often end up getting effect sketches with a smaller set of endpoints. This often translates into easier testing decisions. 

One of the often-mentioned benefits of object orientation is **encapsulation**. Many times when I show people the dependency-breaking techniques in this book, they point out that many of them break encapsulation. That’s true. Many of them do. 

Encapsulation is important, but the reason why it is important is more important. Encapsulation helps us reason about our code. In well-encapsulated code, there are fewer paths to follow as you try to understand it. For instance, if we add another parameter to a constructor to break a dependency as we do in the *Parameterize Constructor* refactoring, we have one more path to follow when we are reasoning about effects. Breaking encapsulation can make reasoning about our code harder, but it can make it easier if we end up with good explanatory tests afterward. When we have test cases for a class, we can use them to reason about our code more directly. We can also write new tests for any questions that we might have about the behavior of the code. 

Encapsulation and test coverage aren’t always at odds, but when they are, I bias toward test coverage. Often it can help me get more encapsulation later. 

Encapsulation isn’t an end in itself; it is a tool for understanding. 

When we need to find out where to write our tests, it’s important to know what can be affected by the changes we are making. We have to reason about effects. We can do this sort of reasoning informally or in a more rigorous way with little sketches, but it pays to practice it. In particularly tangled code, it is one of the only skills we can depend upon in the process of getting tests in place.

## Chapter 12: I Need to Make Many Changes in One Area. Do I Have to Break Dependencies for All the Classes Involved?

Often it pays to test “one level back,” to find a place where we can write tests for several changes at once. We can write tests at a single public method for changes in a number of private methods, or we can write tests at the interface of one object for a collaboration of several objects that it holds. When we do this, we can test the changes we are making, but we also give ourselves some “cover” for more refactoring in the area. The structure of code below the tests can change radically as long as the tests pin down their behavior.

Higher-level tests can be useful in refactoring. Often people prefer them to finely grained tests at each class because they think that change is harder when lots of little tests are written against an interface that has to change. In fact, changes are often easier than you would expect because you can make changes to the tests and then make changes to the code, moving the structure along in small safe increments. 
While higher-level tests are an important tool, they shouldn’t be a substitute for unit tests. Instead, they should be a first step toward getting unit tests in place.

### Interception Points

An **interception point** is simply a point in your program where you can detect the effects of a particular change. In some applications, finding them is tougher than it is in others. If you have an application whose pieces are glued together without many natural seams, finding a decent *interception point* can be a big deal. Often it requires some effect reasoning and a lot of dependency breaking. How do we start? 
The best way to start is to identify the places where you need to make changes and start tracing effects outward from those change points. Each place where you can detect effects is an *interception point*, but it might not be the best *interception point*. You have to make judgment calls throughout the process. 

In general, it is a good idea to pick *interception points* that are very close to your change points, for a couple of reasons. The first reason is safety. Every step between a change point and an interception point is like a step in a logical argument. Essentially, we are saying, “We can test here because this affects this and that affects this other thing, which affects this thing that we are testing.” The more steps you have in the argument, the harder it is know that you have it right. Sometimes the only way you can be sure is by writing tests at the interception point and then going back to the change point to alter the code a little bit and see if the test fails. Sometimes you have to fall back on that technique, but you shouldn’t have to do it all the time. Another reason why more distant interception points are worse is that it is often harder to set up tests at them. This isn’t always true; it depends on the code. What can make it harder is, again, the number of steps between the change and the interception point. Often you have to “play computer” in your mind to know that a test covers some distant piece of functionality. 

In most cases, the best *interception point* we can have for a change is a public method on the class we’re changing. These interception points are easy to find and easy to use, but sometimes they aren’t the best choice. 

The term I use for a place like this in a design is **pinch point**. A *pinch point* is a narrowing in an *effect sketch*, a place where it is possible to write tests to cover a wide set of changes. If you can find a *pinch point* in a design, it can make your work a lot easier. 

The key thing to remember about *pinch points*, though, is that they are determined by change points. A set of changes to a class might have a good pinch point even if the class has multiple clients.

A *pinch point* is a narrowing in an effect sketch, a place where tests against a couple of methods can detect changes in many methods. 

Consider finding *pinch points* for only one or two changes at a time. If you can’t find a pinch point at all, just try to write tests for individual changes as close as you can. 

### Judging Design with Pinch Points

What is a *pinch point*, really? A pinch point is a natural encapsulation boundary. When you find a *pinch point*, you’ve found a narrow funnel for all of the effects of a large piece of code. If the method `BillingStatement.makeStatement` is a *pinch point* for a bunch of invoices and items, we know where to look when the statement isn’t what we expect. The problem then has to be because of the `BillingStatement` class or the invoices and items. Likewise, we don’t need to know about invoices and items to call `makeStatement`. This is pretty much the definition of encapsulation: We don’t have to care about the internals, but when we do, we don’t have to look at the externals to understand them. Often when I look for *pinch points*, I start to notice how responsibilities can be reallocated across classes to give better encapsulation.

Sometimes when you have a large class, you can use effect sketches to discover how to break the class into pieces. 

This isn’t the only way to figure out how to separate responsibilities in a class; sometimes the names will give you a hint, as they do in this case (we have two methods with the word `Token` in their names). This can help you see a large class in a different way, and that could lead to some good class extractions. 

As an exercise, create an effect sketch for changes in a large class and forget about the names of the bubbles. Just look at how they are grouped. Are there any natural encapsulation boundaries? If there are, look at the bubbles inside a boundary. Think about the name that you would use for that cluster of methods and variables: It could become the name of a new class. Think about whether changing any of the names would help.

When you do this, do it with your teammates. The discussions that you have about naming have benefits far beyond the work that you are currently doing. They help you and your team develop a common view of what the system is and what it can become. 

### Pinch Point Traps

When you start to notice that your tests are too large, you should break down the class that you are testing, to make smaller independent pieces that can be tested more easily. At times, you will have to fake out collaborators because the job of a unit test isn’t to see how a cluster of objects behaves together, but rather how a single object behaves. We can test that more easily through a fake object.
When we are writing tests for existing code, the tables are turned. Sometimes it pays to carve off a piece of an application and build it up with tests. When we have those tests in place, we can more easily write narrower unit tests for each of the classes we are touching as we do our work. Eventually, the tests at the pinch point can go away. 

## Chapter 13: I Need to Make Many a Change, but I Don’t Know What Tests to Write

Automated tests are a very important tool, but not for bug finding — not directly, at least. In general, automated tests should specify a goal that we’d like to fulfill or attempt to preserve behavior that is already there. In the natural flow of development, tests that specify become tests that preserve. You will find bugs, but usually not the first time that a test is run. You find bugs in later runs when you change behavior that you didn’t expect to.

### Characterization Tests

In nearly every legacy system, what the system does is more important than what it is supposed to do.

The tests that we need when we want to preserve behavior are what I call **characterization tests**. A *characterization test* is a test that characterizes the actual behavior of a piece of code. There’s no “Well, it should do this” or “I think it does that.” The tests document the actual current behavior of the system. 

Here is a little algorithm for writing characterization tests:
1. Use a piece of code in a test harness. 
2. Write an assertion that you know will fail.
3. Let the failure tell you what the behavior is.
4. Change the test so that it expects the behavior that the code produces.
5. Repeat. 

There is something fundamentally weird about doing this if you are used to thinking about these tests as, well, tests. If we are just putting the values that the software produces into the tests, are our tests really testing anything at all? 
What if the software has a bug? The expected values that we’re putting in our tests could just simply be wrong. 

This problem goes away if we think of our tests in a different way. They aren’t really tests written as a gold standard that the software must live up to. We aren’t trying to find bugs right now. We are trying to put in a mechanism to find bugs later, bugs that show up as differences from the system’s current behavior. When we adopt this perspective, our view of our tests is different: They don’t have any moral authority; they just sit there documenting what pieces of the system really do. When we can see what the pieces do, we can use that knowledge along with our knowledge of what the system is supposed to do to make changes. Frankly, it’s very important to have that knowledge of what the system actually does someplace. We can usually figure out what behavior we need to add by talking to other people or doing some calculations, but short of the tests, there is no other way to know what a system actually does except by “playing computer” in our minds, reading code and trying to reason through what the values will be at particular times. Some people do that faster than others, but regardless of how fast we can do it, it’s pretty tedious and wasteful to have to do it over and over again. 

Characterization tests record the actual behavior of a piece of code. If we find something unexpected when we write them, it pays to get some clarification. It could be a bug. That doesn’t mean that we don’t include the test in our test suite; instead, we should mark it as suspicious and find out what the effect would be of fixing it.

Before you use a method in a legacy system, check to see if there are tests for it. If there aren’t, write them. When you do this consistently, you use tests as a medium of communication. People can look at them and get a sense of what they can and cannot expect from the method. The act of making a class testable in itself tends to increase code quality. People can find out what works and how; they can change it, correct bugs, and move forward. 

### Characterizing Classes

1. Look for tangled pieces of logic. If you don’t understand an area of code, consider introducing a *sensing variable* to characterize it. Use sensing variables to make sure you execute particular areas of the code. 
2. As you discover the responsibilities of a class or method, stop to make a list of the things that can go wrong. See if you can formulate tests that trigger them. 
3. Think about the inputs you are supplying under test. What happens at extreme values? 
4. Should any conditions be true at all times during the lifetime of the class? Often these are called invariants. Attempt to write tests to verify them. Often you might have to refactor to discover these conditions. If you do, the refactorings often lead to new insight about how the code should be. 

### Targeted Testing

When you write a test for a branch, ask yourself whether there is any other way that the test could pass, aside from executing that branch. If you are not sure, use a *sensing variable* or the debugger to find out whether the test is hitting it.

When we refactor, we generally have to check for two things: Does the behavior exist after the refactoring, and is it connected correctly? 
Many characterization tests look like “sunny day” tests. They don’t test many special conditions; they just verify that particular behaviors are present. From their presence, we can infer that refactorings that we’ve done to move or extract code have preserved behavior. 

### A Heuristic for Writing Characterization Tests

1. Write tests for the area where you will make your changes. Write as many cases as you feel you need to understand the behavior of the code. 
2. After doing this, take a look at the specific things you are going to change, and attempt to write tests for those. 
3. If you are attempting to extract or move some functionality, write tests that verify the existence and connection of those behaviors on a case-by- case basis. Verify that you are exercising the code that you are going to move and that it is connected properly. Exercise conversions. 

## Chapter 14: Dependencies on Libraries Are Killing Me

Avoid littering direct calls to library classes in your code. You might think that you’ll never change them, but that can become a self-fulfilling prophecy. 

Library designers who use language features to enforce design constraints are often making a mistake. They forget that good code runs in production and test environments. Constraints for the former can make working in the latter nearly impossible. 

A related problem is the *restricted override dilemma*. In some OO languages, all methods are virtual. In others, they are virtual by default, but they can be made non-virtual. In others, you have to explicitly make them virtual. From a design perspective, there is some value in making some methods non-virtual. At times, various people in the industry have recommended making as many methods non-virtual as possible. Sometimes the reasons they give are good, but it is hard to deny that this practice makes it hard to introduce sensing and separation in code bases. It is also hard to deny that people often write very good code in Smalltalk, where that practice is impossible; in Java, where people generally don’t do it; and even in C++, where plenty of code has been written without it. You can do very well just pretending that a public method is non-virtual in production code. If you do that, you can override it selectively in test and get the best of both worlds. 

Sometimes using a coding convention is just as good as using a restrictive language feature. Think about what your tests need. 

## Chapter 15: My Application is All API Calls

There are many different things to consider when choosing to integrate code we can’t change. We have to know how stable it is, whether it is sufficient, and how easy it is to use. And, when we do finally decide to use someone else’s code, we’re often left with another problem. We end up with applications that look like they are nothing but repeated calls to someone else’s library. How do we make changes in code like that? 

Systems that are littered with library calls are harder to deal with than homegrown systems, in many respects. The first reason is that it is often hard to see how to make the structure better because all you can see are the API calls. Anything that would’ve been a hint at a design just isn’t there. The second reason that API-intensive systems are difficult is that we don’t own the API. If we did, we could rename interfaces, classes, and methods to make things clearer for us, or add methods to classes to make them available to different parts of the code. 

When we **Skin and Wrap** the API, we make interfaces that mirror the API as close as possible and then create wrappers around library classes. To minimize our chances of making mistakes, we can *Preserve Signatures* as we work. One advantage to skinning and wrapping an API is that we can end up having no dependencies on the underlying API code. Our wrappers can delegate to the real API in production code and we can use fakes during test. 

In **Responsibility-Based Extraction**, we identify responsibilities in the code and start extracting methods for them. 

How do we choose between *Skin and Wrap the API* and *Responsibility-Based Extraction*? Here are the trade-offs: 

*Skin and Wrap the API* is good in these circumstances: 
* The API is relatively small. 
* You want to completely separate out dependencies on a third-party library. 
* You don’t have tests, and you can’t write them because you can’t test through the API. 

When we skin and wrap an API, we have the chance to get all of our code under test except for a thin layer of delegation from the wrapper to the real API classes.

*Responsibility-Based Extraction* is good in these circumstances: 
* The API is more complicated. 
* You have a tool that provides a safe extract method support, or you feel confident that you can do the extractions safely by hand.

Balancing the advantages and disadvantages of these techniques is kind of tricky. *Skin and Wrap the API* is more work, but it can be very useful when we want to isolate ourselves from third-party libraries, and that need comes up often. See Chapter 14, *Dependencies on Libraries Are Killing Me*, for details. When we use *Responsibility-Based Extraction*, we might end up extracting some of our own logic with the API code just so that we can extract a method with a higher-level name. If we do, our code can depend on higher-level interfaces rather than low-level API calls, but we might not be able to get the code we’ve extracted under test. 
Many teams use both techniques: a thin wrapper for testing and a higher- level wrapper to present a better interface to their application.

### Chapter 16: I Don’t Understand the Code Well Enough to Change It

Stepping into unfamiliar code, especially legacy code, can be scary. Over time, some people become relatively immune to the fear. They develop confidence from confronting and slaying monsters in code over and over again, but it is tough not to be afraid. Everyone runs into demons that they can’t slay from time to time. If you dwell on it before you start to look at the code, that makes it worse. You never know whether a change is going to be simple or a weeklong hair-pulling exercise that leaves you cursing the system, your situation, and nearly everything around you. If we understood everything we need to know to make our changes, things would go smoother. How can we get that understanding? 

### Notes/Sketching

When reading through code gets confusing, it pays to start drawing pictures and making notes. Write down the name of the last important thing that you saw, and then write down the name of the next one. If you see a relationship between them, draw a line. These sketches don’t have to be full-blown UML diagrams or function call graphs using some special notation — although, if things get more confusing, you might want to get more formal or neater to organize your thoughts. Sketching things out often helps us see things in a different way. It’s also a great way of maintaining our mental state when we are trying to understand something particularly complex. 

The really great thing about sketching parts of a design as you are trying to understand them is that it is informal and infectious. If you find this technique useful, you don’t have to push for your team to make it part of its process. All you have to do is this: Wait until you are working with someone trying to understand some code, and then make a little sketch of what you are looking at as you try to explain it. If your partner is really engaged in learning that part of the system too, he or she will look at the sketch and go back and forth with you as you figure out the code. 

### Listing Markup

* Separating Responsibilities
* Understanding Method Structure
* Extract Methods
* Understand the Effects of a Change

### Scratch Refactoring

How do you know that you aren’t breaking anything when you do all of this refatoring to understand the code? The fact is, you can work in a way in which you don’t need to care — and it’s pretty easy to do. Check out the code from your version-control system. Forget about writing tests. Extract methods, move variables, refactor it whatever way you want to get a better understanding of it — just don’t check it in again. Throw that code away. This is called **Scratch refactoring**.

### Delete Unused Code

Sometimes people feel that deleting code is wasteful. After all, someone spent time writing that code—maybe it can be used in the future. Well, that is what version-control systems are for. That code will be in earlier versions. You can always look for if you ever decide that you need it. 

## Chapter 17: My Application Has No Structure

Long-lived applications tend to sprawl. They might have started out with a well-thought-out architecture, but over the years, under schedule pressure, they can get to the point at which nobody really understands the complete structure. People can work for years on a project and not have any idea where new features are intended to go; they just know the hacks that have been placed in the system recently. When they add new features, they go to the “hack points” because those are the areas that they know best. 
There is no easy remedy for this sort of thing, and the urgency of the situation varies widely. In some cases, programmers run up against a wall. It’s difficult to add new features, and that brings the entire organization into crisis mode. People are charged with the task of figuring out whether it would be better to rearchitect or rewrite the system. In other organizations, the system limps along for years. Yes, it takes longer than it should to add new features, but that is just considered the price of doing business. Nobody knows how much better it could be or how much money is being lost because of poor structure. 
When teams aren’t aware of their architecture, it tends to degrade. What gets in the way of this awareness? 

* The system can be so complex that it takes a long time to get the big picture. 
* The system can be so complex that there is no big picture. 
* The team is in a very reactive mode, dealing with emergency after emergency so much that they lose sight of the big picture.

Traditionally, many organizations have used the role of architect to solve these problems. Architects are usually charged with the task of working out the big picture and making decisions that preserve the big picture for the team. That can work, but there is one strong caveat. An architect has to be out in the team, working with the members day to day, or else the code diverges from the big picture. There are two ways this can happen: Someone could be doing something inappropriate in the code or the big picture itself could need to be modified. In some of the worst situations I’ve encountered with teams, the architect of a group has a completely different view of the system than the programmers. Often this happens because the architect has other responsibilities and can’t get into the code or can’t communicate with the rest of the team often enough to really know what is there. As a result, communication breaks down across the organization. 
The brutal truth is that architecture is too important to be left exclusively to a few people. It’s fine to have an architect, but the key way to keep an architecture intact is to make sure that everyone on the team knows what it is and has a stake in it. Every person who is touching the code should know the architecture, and everyone else who touches the code should be able to benefit from what that person has learned. When everyone is working off of the same set of ideas, the overall system intelligence of the team is amplified. If you have, say, a team of 20 and only 3 people know the architecture in detail, either those 3 have to do a lot to keep the other 17 people on track or the other 17 people just make mistakes caused by unfamiliarity with the big picture. 

### Telling the Story of the System

When I work with teams, I often use a technique that I call “telling the story of the system.” To do it well, you need at least two people. One person starts off by asking another, “What is the architecture of the system?” Then the other person tries to explain the architecture of the system using only a few concepts, maybe as few as two or three. If you are the person explaining, you have to pretend that the other person knows nothing about the system. In only a few sentences, you have to explain what the pieces of the design are and how they interact. After you say those few sentences, you have articulated what you feel are the most essential things about the system. Next, you pick the next most important things to say about the system. You keep going until you’ve said just about everything important about the core design of the system. 

### Naked CRC

**CRC** stands for **Class, Responsibility, and Collaborations**. You mark up each card with a class name, its responsibilities, and a list of its collaborators (other classes that this class communicates with). If you think that a responsibility doesn’t belong on a particular class, cross it out and write it on another class card, or create another class card altogether.

### Conversation Scrutiny

Listen to conversations about your design. Are the concepts you’re using in conversation the same as the concepts in the code? I wouldn’t expect them all to be. Software has to satisfy stronger constraints than just being easy to talk about, but if there isn’t a strong overlap between conversation and code, it’s important to ask why. The answer is usually a mixture of two things: The code hasn’t been allowed to adapt to the team’s understanding, or the team needs to understand it differently. In any case, being very tuned to the concepts people naturally use to describe the design is powerful. When people talk about design, they are trying to make other people understand them. Put some of that understanding in the code.

## Chapter 18: My Test Code Is in the Way

### Class Naming Conventions

The key thing to remember is that ergonomics is important. It’s important to consider how easy it will be to navigate back and forth between your classes and your tests. 

### Test Location

An alternative is to keep the production code and the test code in the same location but to use scripts or build settings to remove the test code from the deployment. If you use good naming conventions for your classes, this can work out fine. 

## Chapter 19: My Project Is Not Object Oriented. How Do I Make Safe Changes?

### Easy Case

### A Hard Case

Although macro preprocessors are easily misused, they are actually very useful in this context. File inclusion and macro replacement can help us get past dependencies in the thorniest code. As long as we restrict rampant usage of macros to code that runs under test, we don’t have to be too concerned that we’ll misuse macros in ways that will affect the production code. 
C is one of the few mainstream languages that have a macro preprocessor. In general, to break dependencies in other procedural languages, we have to use the *link seam* and attempt to get larger areas of code under test.

### Adding New Behavior

### Taking Advantage of Object Orientation

In object-oriented languages, we have *object seams* available. They have some nice properties: 
* They are easy to notice in the code. 
* They can be used to break code down into smaller, more understandable pieces. 
* They provide more flexibility. Seams that you introduce for testing might be useful when you have to extend your software. 

### It’s All Object Oriented

Procedural code doesn’t present us with as many options as object-oriented code does, but we can make headway in procedural legacy code. The particular seams that a procedural language presents critically affect the ease of the work. If the procedural language you are using has an object-oriented successor, I recommend moving toward it. *Object seams* are good for far more than getting tests in place. Link and preprocessing seams are great for getting code under test, but they really don’t do much to improve design beyond that. 

## Chapter 20: This Class Is Too Big and I Don’t Want It To Get Any Bigger

Many of the features that people add to systems are little tweaks. They require the addition of a little code and maybe a few more methods. It’s tempting to just make these changes to an existing class. Chances are, the code that you need to add must use data from some existing class, and the easiest thing is to just add code to it. Unfortunately, this easy way of making changes can lead to some serious trouble. When we keep adding code to existing classes, we end up with long methods and large classes. Our software turns into a swamp, and it takes more time to understand how to add new features or even just understand how old features work. 

What are the problems with big classes? The first is confusion. When you have 50 or 60 methods on a class, it’s often hard to get a sense of what you have to change and whether it is going to affect anything else. In the worst cases, big classes have an incredible number of instance variables, and it is hard to know what the effects are of changing a variable. Another problem is task scheduling. When a class has 20 or so responsibilities, chances are, you’ll have an incredible number of reasons to change it. In the same iteration, you might have several programmers who have to do different things to the class. If they are working concurrently, this can lead to some serious thrashing, particularly because of the third problem: Big classes are a pain to test.

Encapsulation is a good thing, right? Well, don’t ask testers about that; they are liable to bite your head off. Classes that are too big often hide too much. Encapsulation is great when it helps us reason about our code and when we know that certain things can be changed only under certain circumstances. However, when we encapsulate too much, the stuff inside rots and festers. There isn’t any easy way to sense the effects of change, so people fall back on *Edit and Pray* programming. At that point, either changes take far too long or the bug count increases. You have to pay for the lack of clarity somehow. 

**Single-Responsibility Principle (SRP)**:
Every class should have a single responsibility: It should have a single purpose in the system, and there should be only one reason to change it. 

### Seeing Responsibilities

Learning to see responsibilities is a key design skill, and it takes practice. It might seem odd to talk about a design skill in this context of working with legacy code, but there really is little difference between discovering responsibilities in existing code and formulating them for code that you haven’t written yet. The key thing is to be able to see responsibilities and learn how to separate them well. If anything, legacy code offers far more possibilities for the application of design skill than new features do. It is easier to talk about design tradeoffs when you can see the code that will be affected, and it is also easier to see whether structure is appropriate in a given context because the context is real and right in front of us. 

**Heuristic #1: Group Methods**

Look for similar method names. Write down all of the methods on a class, along with their access types (public, private, and so on), and try to find ones that seem to go together. 

**Heuristic #2: Look at Hidden Methods**

Pay attention to private and protected methods. If a class has many of them, it often indicates that there is another class in the class dying to get out. 

**Heuristic #3: Look for Decisions That Can Change**

Look for decisions — not decisions that you are making in the code, but decisions that you’ve already made. Is there some way of doing something (talking to a database, talking to another set of objects, and so on) that seems hard-coded? Can you imagine it changing? 

**Heuristic #4: Look for Internal Relationships** 

Look for relationships between instance variables and methods. Are certain instance variables used by some methods and not others? 

In *feature sketches*, arrows point in the direction of a method or variable that is used by another method or variable. In *effect sketches*, the arrow points toward methods or variables that are impacted by other methods and variables. 
These are two different, completely legitimate ways of looking at interactions in a system. *Feature sketches* are great for mapping the internal structure of classes. *Effect sketches* are great for reasoning forward from a point of change. 

*Feature sketches* are a great tool for finding separate responsibilities in classes. We can try to group the features and figure out what classes we can extract based upon the names. But in addition to helping us find responsibilities, feature sketches allow us to see the dependency structure inside classes, and that can often be just as important as responsibility when we are deciding what to extract.

**Heuristic #5: Look for the Primary Responsibility**

Try to describe the responsibility of the class in a single sentence.

There are two ways to violate the *Single Responsibility Principle*. It can be violated at the interface level and at the implementation level. SRP is violated at the interface level when a class presents an interface that makes it appear that it is responsible for a very large number of things.

The SRP violation that we care most about is violation at the implementation level. Plainly put, we care whether the class really does all of that stuff or whether it just delegates to a couple of other classes. If it delegates, we don’t have a large monolithic class; we just have a class that is a facade, a front end for a bunch of little classes and that can be easier to manage. 

**Interface Segregation Principle (ISP)**:
When a class is large, rarely do all of its clients use all of its methods. Often we can see different groupings of methods that particular clients use. If we create an interface for each of these groupings and have the large class implement those interfaces, each client can see the big class through that particular interface. This helps us hide information and also decreases dependency in the system. The clients no longer have to recompile whenever the large class does. 

**Heuristic #6: When All Else Fails, Do Some Scratch Refactoring**

If you are having a lot of trouble seeing responsibilities in a class, do some scratch refactoring.

**Heuristic #7: Focus on the Current Work**

Pay attention to what you have to do right now. If you are providing a different way of doing anything, you might have identified a responsibility that you should extract and then allow substitution for.

### Other Techniques

The heuristics for identifying responsibilities can really help you dig in and find new abstractions in old classes, but they are just tricks. The way to really get better at identification is to read more. Read books about design patterns. More important, read other people’s code. Look at open-source projects, and just take some time to browse and see how other people do things. Pay attention to how classes are named and the correspondence between class names and the names of methods. Over time, you’ll get better at identifying hidden responsibilities, and you’ll just start to see them when you browse unfamiliar code. 

### Moving Forward

There are a couple of things that can go wrong when you extract classes without tests. The most subtle bugs that we can inject are bugs related to inheritance. Moving a method from one class to another is pretty safe. You can *Lean on the Compiler* to aid your work, but in most languages all bets are off if you attempt to move a method that overrides another method. If you do, callers of the method on the original class will now call a method with the same name from a base class. A similar situation can occur with variables. A variable in a subclass can hide a variable with the same name in a superclass. Moving it just makes the one that was hidden visible. 
To get past these problems, we don’t move the original methods at all. We create new methods by extracting the bodies of the old ones. The prefix is just a mechanical way of generating a new name and making sure that it doesn’t clash with other names before the move. Instance variables are a little trickier: We have that manual step of searching for uses of variables before we use them. It is possible to make mistakes with this. Be very careful, and do it with a partner. 

### After Extract Class

Extracting classes from a big class is often a good first step. In practice, the biggest danger for teams doing this is getting overambitious. You might have done a *Scratch refactoring* or developed some other view of what the system should look like. But remember, the structure you have in your application works. It supports the functionality; it just might not be tuned toward moving forward. Sometimes the best thing that you can do is formulate a view of how a large class is going to look after refactoring and then just forget about it. You did it to discover what is possible. To move forward, you have to be sensitive to what is there and move that not necessarily toward the ideal design, but at least in a better direction.

## Chapter 21: I’m Changing the Same Code All Over The Place

### First Steps

My first reaction when I am confronted by duplication is to step back and get a sense of the full scope of it. When I do that, I start thinking about what kind of classes I’ll end up with and what the extracted bits of duplication will look like. Then I realize that I’m really over-thinking it. Removing small pieces of duplication helps, and it makes it easier to see larger areas of duplication later.

When two methods look roughly the same, extract the differences to other methods. When you do that, you can often make them exactly the same and get rid of one.

Abbreviations in class and method names are problematic. They can be okay when they are used consistently, but in general, I don’t like to use them. 

When you remove duplication across classes, you end up with very small focused methods. Each of them does something that no other method does, and that gives us an incredible advantage: orthogonality.
Orthogonality is a fancy word for independence. If you want to change existing behavior in your code and there is exactly one place you have to go to make that change, you’ve got orthogonality. 

One of the startling things that you discover when you start removing duplication zealously is that designs emerge. You don’t have to plan most of the knobs in your application; they just happen. 

Duplication removal is a powerful way of distilling a design. It not only makes a design more flexible, but it also makes change faster and easier. 

The **open/closed** principle is a principle that was first articulated by Bertrand Meyer. The idea behind it is that code should be open for extension but closed to modification. What does that mean? It means that when we have good design, we just don’t have to change code much to add new features. 

## Chapter 22: I’m Need to Change a Monster Method and I Can’t Write Tests For It

Long methods are a pain, but monster methods are worse. A **monster method** is a method that is so long and so complex that you really don’t feel comfortable touching it. Monster methods can be hundreds or thousands of lines long, with enough scattered indentation to make navigation nearly impossible. When you have monster methods you’re tempted to print them on a couple of yards of continuous-feed paper and lay them out in a hallway so that you and your coworkers can figure them out.

### Varieties of Monsters

* Bulleted Methods

A **bulleted method** is a method with nearly no indentation. It is just a sequence of code chunks that reminds you of a bulleted list. Some of the code in the chunks might be indented, but the method itself isn’t dominated by indentation. 

* Snarled Methods

A **snarled method** is a method dominated by a single large, indented section. 

### Tackling Monsters with Automated Refactoring Support

When doing automated refactoring without tests, use the tool exclusively. After a series of automated refactorings, you can often get tests in place that you can use to verify any manual edits that you make.

The key thing to remember when you use an automated tool to extract methods is that you can do a lot of coarse work safely and handle the details after you get other tests in place. Don’t be too concerned about methods that seem like they don’t fit the class. Often they point toward the need to extract a new class later.

### The Manual Refactoring Challenge

Monster methods make testing, refactoring, and feature addition very difficult. If you are able to create instances of the class housing the method in a test harness, you can attempt to devise some set of test cases that will give you confidence as you break down the method. If the logic in the method is particularly complex, this can be a nightmare. 

* Introduce sensing variable

We might not want to add features to production code when we’re refactoring it, but that doesn’t mean that we can’t add any code. Sometimes it helps to add a variable to a class and use it to sense conditions in the method that we want to refactor. When we’ve done the refactoring that we need to do, we can get rid of that variable, and our code will be in a clean state. This is called **Introduce Sensing Variable**. 

Sensing variables are a key tool for teasing apart monster methods. You can use them to do some refactoring deep inside snarled methods, but you can also use them to progressively de-snarl methods. 

* Extract What You Know

Another strategy that we can use when we are working with monster methods is to start small and find little pieces of code that we can extract confidently without tests, and then add tests to cover them. 

The **coupling count** is the number of values that pass into and out of the method you are extracting. 

* Gleaning Dependencies

Sometimes there is code in a monster method that is kind of secondary to the method’s main purpose. It is necessary, but it isn’t terribly complex, and if you accidentally break it, it will be obvious. But although all of that is true, you simply cannot take a chance on breaking the main logic of the method. In cases like these, you can use a technique called gleaning dependencies. You write tests for the logic that you need to preserve. Afterward, you extract things that the tests do not cover. When you do this, you can at least have confidence that you are preserving the important behavior. 

**Gleaning Dependencies** is particularly powerful when critical behavior is tangled with other behavior. When you have solid tests for the critical behavior, you can do a lot of editing that technically isn’t all covered by tests, but it helps you to preserve key behavior. 

* Break Out a Method Object

This technique was first described by Ward Cunningham, and it epitomizes the idea of an invented abstraction. When you break out a method object, you create a class whose only responsibility is to do the work of your monster method. The parameters of the method become parameters to a constructor on the new class, and the code of the monster method can go into a method named run or execute on the new class. When the code has been moved to the new class, we’re in a great position to refactor. We can turn the temporary variables in the method into instance variables and sense through them as we break down the method.

### Strategy

* Skeletonize Methods
* Find Sequences
* Extract to the Current Class First

When you start to extract methods from a monster method, you’ll probably notice that some of the chunks of code that you are extracting really belong in other classes. One strong indication is the name you’re tempted to use. If you look at a piece of code and you are tempted to use the name of one of the variables you are using in it, chances are good that the code belongs on the class of that variable. 

* Extract Small Pieces

This is a far better strategy than trying to break up a method into large chunks from the beginning. Too often that isn’t as easy as it looks; it isn’t as safe. It’s easier to miss the details, and the details are what make the code work. 

* Be Prepared to Redo Extractions

There are many ways to slice a pie and many ways to break down a monster method. After you make some extractions, you’ll usually find better ways to accommodate new features more easily. Sometimes the best way to move forward is to undo an extraction or two and re-extract. When you do this, it doesn’t mean that the first extractions were wasted effort. They gave you something very important: insight into old design and into a better way of moving forward. 

## Chapter 23: How Do I Know That I’m Not Breaking Anything?

Code is a strange sort of building material. Most materials that you can make things from, such as metal, wood, and plastic, fatigue. They break when you use them over time. Code is different. If you leave it alone, it never breaks. Short of the stray cosmic ray flipping a bit on your storage media, the only way it gets a fault is for someone to edit it. Run a machine made of metal over and over again, and it will eventually break. Run the same code over and over again, and, well, it will just run over and over again. 

### Hyperaware Editing

**Hyperaware editing** is a flow state, a state in which you can just shut out the world and work sensitively with the code.

### Single-Goal Editing

At this point in my career, I think I’m a much better programmer than I used to be, even though I know less about the details of each language I work in. Judgment is a key programming skill, and we can get into trouble when we try to act like super-smart programmers. 

“Programming is the art of doing one thing at a time.”

When you are programming, it is pretty easy to pick off too big of a chunk at a time. If you do, you end up thrashing and just trying things out to make things work rather than working very deliberately and really knowing what your code does.

### Preserve Signatures

When you are breaking dependencies for test, you have to apply extra care. One thing that I do is *Preserve Signatures* whenever I can. When you avoid changing signatures at all, you can cut/copy and paste entire method signatures from place to place and minimize any chances of errors.

### Lean on the Compiler

The primary purpose of a compiler is to translate source code into some other form, but in statically typed languages, you can do much more with a compiler. You can take advantage of its type checking and use it to identify changes you need to make. I call this practice leaning on the compiler. 

It’s easy to make a mistake and have no idea that you’ve broken the software. A second set of eyes definitely helps. Let’s face it, working in legacy code is surgery, and doctors never operate alone. 

## Chapter 24: We Feel Overwhelmed. It Isn’t Going to Get Any Better

The key to thriving in legacy code is finding what motivates you. Although many of us programmers are solitary creatures, there really isn’t much that can replace working in a good environment with people you respect who know how to have fun at work. I’ve made some of my best friends at work and, to this day, they are the people I talk to when I’ve learned something new or fun while programming. 

If morale is low on your team, and it’s low because of code quality, here’s something that you can try: Pick the ugliest most obnoxious set of classes in the project, and get them under test. When you’ve tackled the worst problem as a team, you’ll feel in control of your situation. I’ve seen it again and again. 

As you start to take control of your code base, you’ll start to develop oases of good code. Work can really be enjoyable in them.

# Part III: Dependency-Breaking Techniques

## Chapter 25: Dependency-Breaking Techniques

### Adapt Parameter

Use *Adapt Parameter* when you can’t use *Extract Interface* on a parameter’s class or when a parameter is difficult to fake.

Move toward interfaces that communicate responsibilities rather than implementation details. This makes code easier to read and easier to maintain.

Superficially, this might look like we’re making things pretty for pretty’s sake, but one pervasive problem in legacy code bases is that there often aren’t any layers of abstraction; the most important code in the system often sits intermingled with low-level API calls. We’ve already seen how this can make testing difficult, but the problems go beyond testing. Code is harder to understand when it is littered with wide interfaces containing dozens of unused methods. When you create narrow abstractions targeted toward what you need, your code communicates better and you are left with a better seam. 

*Adapt Parameter* is one case in which we don’t *Preserve Signatures*. Use extra care. 

Safety first. Once you have tests in place, you can make invasive changes much more confidently. 

To use *Adapt Parameter*, perform the following steps: 
1. Create the new interface that you will use in the method. Make it as simple and communicative as possible, but try not to create an interface that will require more than trivial changes in the method.
2. Create a production implementer for the new interface.
3. Create a fake implementer for the interface.
4. Write a simple test case, passing the fake to the method.
5. Make the changes you need to in the method to use the new parameter.
6. 6. Run your test to verify that you are able to test the method using the fake. 

### Break Out Method Object

*Break Out Method Object* has several variations. In the simplest case, the original method doesn’t use any instance variables or methods from the original class. We don’t need to pass it a reference to the original class. 
In other cases, the method only uses data from the original class. At times, it makes sense to put this data into a new data-holding class and pass it as an argument to the method object. 
The case that I show in this section is the worst case; we need to use methods on the original class, so we use *Extract Interface* and start to build up some abstraction between the method object and the original class. 

You can use these steps to do *Break out Method Object* safely without tests: 
1. Create a class that will house the method code. 
2. Create a constructor for the class and *Preserve Signatures* to give it an exact copy of the arguments used by the method. If the method uses an instance data or methods from the original class, add a reference to the original class as the first argument to the constructor. 
3. For each argument in the constructor, declare an instance variable and give it exactly the same type as the variable. *Preserve Signatures* by copying all the arguments directly into the class and formatting them as instance variable declarations. Assign all of the arguments to the instance variables in the constructor.
4. Create an empty execution method on the new class. Often this method is called `run()`. We used the name draw in the example.
5. Copy the body of the old method into the execution method and compile to *Lean on the Compiler*. 
6. The error messages from the compiler should indicate where the method is still using methods or variables from the old class. In each of these cases, do what it takes to get the method to compile. In some cases, this is as simple as changing a call to use the reference to the original class. In other cases, you might have to make methods public on the original class or introduce getters so that you don’t have to make instance variables public. 
7. After the new class compiles, go back to the original method and change it so that it creates an instance of the new class and delegates its work to it. 
8. If needed, use *Extract Interface* to break the dependency on the original class. 

### Definition Completion

In some languages, we can declare a type in one place and define it in another. The languages in which this capability is most apparent are C and C++. In both of them, we can declare a function or method in one place and define it someplace else, usually in an implementation file. When we have this capability, we can use it to break dependencies. 

To use *Definition Completion* in C++, follow these steps: 
1. Identify a class with definitions you’d like to replace. 
2. Verify that the method definitions are in a source file, not a header. 
3. Include the header in the test source file of the class you are testing. 
4. Verify that the source files for the class are not part of the build. 
5. Build to find missing methods. 
6. Add method definitions to the test source file until you have a complete build. 

### Encapsulate Global References

When you are trying to test code that has problematic dependencies on globals, you essentially have three choices. You can try to make the globals act differently under test, you can link to different globals, or you can encapsulate the globals so that you can decouple things further. 

If several globals are always used or are modified near each other, they belong in the same class. 

When naming a class, think about the methods that will eventually reside on it. The name should be good, but it doesn’t have to be perfect. Remember that you can always rename the class later. 

The class name that you find might already be in use. If so, consider whether you can rename whatever is using that name.

Referencing a member of a class rather than a simple global is only the first step. Afterward, consider whether you should use *Introduce Static Setter*, or parameterize the code using *Parameterize Constructor* or *Parameterize Method*. 

When you use *Encapsulate Global References*, start with data or small methods. More substantial methods can be moved to the new class when more tests are in place. 

To *Encapsulate Global References*, follow these steps: 
1. Identify the globals that you want to encapsulate. 
2. Create a class that you want to reference them from. 
3. Copy the globals into the class. If some of them are variables, handle their initialization in the class.
4. Comment out the original declarations of the globals. 
5. Declare a global instance of the new class. 
6. *Lean on the Compiler* to find all the unresolved references to the old globals. 
7. Precede each unresolved reference with the name of the global instance of the new class. 
8. In places where you want to use fakes, use *Introduce Static Setter*, *Parameterize Constructor*, *Parameterize Method* or *Replace Global Reference with Getter*. 

### Expose Static Method

Working with classes that can’t be instantiated in a test harness is pretty tricky. Here is a technique that I use in some cases. If you have a method that doesn’t use instance data or methods, you can turn it into a static method. When it is static, you can get it under test without having to instantiate the class. 

When you are breaking dependencies without tests, *Preserve Signatures* of methods whenever possible. If you cut/copy and paste whole method signatures, you have less of a chance of introducing errors. 

Encapsulation is a great thing for classes, but the static area of a class isn’t really part of the class. In fact, in some languages, it is part of another class, sometimes known as the metaclass of the class. 
When a method is static, you know that it doesn’t access any of the private data of the class; it is just a utility method. If you make the method public, you can write tests for it. Those tests will support you if you choose to move the method to another class later. 

Static methods and data really do act as if they are part of a different class. Static data lives for the life of a program, not the life of an instance, and statics are accessible without an instance. 
The static portions of a class can be seen as a “staging area” for things that don’t quite belong to the class. If you see a method that doesn’t use any instance data, it is a good idea to make it static to make it noticeable until you figure out what class it really belongs on. 

To *Expose Static Method*, follow these steps:
1. Write a test that accesses the method that you want to expose as a public static method of the class. 
2. Extract the body of the method to a static method. Remember to *Preserve Signatures*. You’ll have to use a different name for the method. Often you can use the names of parameters to help you come up with a new method name.
3. Compile. 
4. If there are errors related to accessing instance data or methods, take a look at those features and see if they can be made static also. If they can, make them static so that the system will compile. 

### Extract and Override Call

*Extract and Override Call* is a very useful refactoring; I use it very often. It is an ideal way to break dependencies on global variables and static methods. In general, I tend to use it unless there are many different calls against the same global. If there are, I often use *Replace Global Reference with Getter* instead. 

To *Extract and Override Call*, follow these steps:
1. Identify the call that you want to extract. Find the declaration of its method. Copy its method signature so that you can *Preserve Signatures*.
2. Create a new method on the current class. Give it the signature you’ve copied. 
3. Copy the call to the new method and replace the call with a call to the new method. 

### Extract and Override Factory Method

Object creation in constructors can be vexing when you want to get a class under test. Sometimes the work that is happening in those objects shouldn’t happen in a test harness. At other times, you just want to get a sensing object in place, but you can’t because that object’s creation is hard-coded in a constructor. 

Hard-coded initialization work in constructors can be very hard to work around in testing. 

To *Extract and Override Factory Method*, follow these steps:
1. Identify an object creation in a constructor. 
2. Extract all of the work involved in the creation into a factory method. 
3. Create a testing subclass and override the factory method in it to avoid dependencies on problematic types under test.

### Extract and Override Getter

The gist of this refactoring is to introduce a getter for the instance variable that you want to replace with a fake object. You then refactor to use the getter every place in the class. You can then subclass and override the getter to provide alternate objects under test. 

A **lazy getter** is a method that looks like a normal getter to all of its callers. The key difference is that lazy getters create the object they are supposed to return the first time they are called. 
Lazy getters are also used in the *Singleton Design Pattern*.

When you use *Extract and Override Getter*, you have to be very conscious of object lifetime issues, particularly in a non-garbage-collected language such as C++. Make sure that you delete the testing instance in a way that is consistent with how the code deletes the production instance. 

To *Extract and Override Getter*, follow these steps: 
1. Identify the object you need a getter for. 
2. Extract all of the logic needed to create the object into a getter. 
3. Replace all uses of the object with calls to the getter, and initialize the reference that holds the object to null in all constructors.
4. Add the first-time logic to the getter so that the object is constructed and assigned to the reference whenever the reference is null. 
5. Subclass the class and override the getter to provide an alternative object for testing. 

### Extract Implementer

*Extract Interface* is a handy technique, but one part of it is hard: naming. 

One thing that I usually stop short of is putting an `I` prefix on the name of the class to make a name for the new interface, unless it is already the convention in the code base. There is nothing worse than working in an unfamiliar area of code in which half the type names start with I and half don’t. Half of the time that you type the name of a type, you’ll be wrong. You’ll either have missed the needed I or not. 

Naming is a key part of design. If you choose good names, you reinforce understanding in a system and make it easier to work with. If you choose poor names, you undermine understanding and make life hellish for the programmers who follow you. 

In this refactoring, we’re replacing the creation of objects of one concrete class with objects of another, so we aren’t really making our overall dependency situation better. However, it’s good to take a look at those areas of object creation and try to figure out whether a factory can be used to reduce dependencies further. 

To *Extract Implementer*, follow these steps: 
1. Make a copy of the source class’s declaration. Give it a different name. It’s useful to have a naming convention for classes you’ve extracted. I often use the prefix Production to indicate that the new class is the production code implementer of an interface. 
2. Turn the source class into an interface by deleting all non-public methods and all variables. 
3. Make all of the remaining public methods abstract.
4. Examine all imports or file inclusions in the interface file, and see if they are necessary. Often you can remove many of them. You can *Lean on the Compiler* to detect these. Just delete each in turn, and recompile to see if it is needed. 
5. Make your production class implement the new interface.
6. Compile the production class to make sure that all method signatures in the interface are implemented.
7. Compile the rest of the system to find all of the places where instances of the source class were created. Replace these with creations of the new production class.
8. Recompile and test.

### Extract Interface

In many languages, *Extract Interface* is a one of the safest dependency-breaking techniques. If you get a step wrong, the compiler tells you immediately, so there is very little chance of introducing a bug. The gist of it is that you create an interface for a class with declarations for all of the methods that you want to use in some context. When you’ve done that, you can implement the interface to sense or separate, passing a fake object into the class you want to test. 

When interfaces were first introduced in languages, some people started naming interfaces by placing an I before the name of the class they were gleaned from. For instance, if you had an `Account` class and you wanted an interface, you could give it the name `IAccount`. The advantage to this sort of naming is that you don’t really have to think about the name when you do the extraction. Naming is as simple as adding a prefix. The disadvantage is that you end up with a lot of code that has to know whether it is dealing with an interface. Ideally, it shouldn’t care one way or another. You also end up with a code base in which some names have I prefixes and some don’t. Removing the `I` if you want to go back to a regular class ends up being a pervasive change. If you don’t make the change, the name stays in the code as a subtle lie.

When you are developing new classes, the easiest thing to do is create simple class names, even for big abstractions. For instance, if we are writing an accounting package, we can start with a class that is just called `Account`. Then we can start to write tests to add new functionality. At some point, you might want `Account` to be an interface. If you do, you can create a subclass underneath it, push down all of the data and methods, and make `Account` an interface. When you do that, you don’t have to go through your code renaming the type of every reference to `Account`.
In cases such as the IPaydayTransactionI example, in which we already have a nice name for an interface (`ITransactionLog`), we can do the same thing. The downside is that pushing down data and methods to a new subclass takes a lot of steps. But when the risk is small enough, I use it sometimes. This technique is called *Extract Implementer*.
If I don’t have many tests and I want to extract an interface to get more in place, I often try to come up with a new name for the interface. Sometimes it takes a little while to think of one. If you don’t have tools that will rename classes for you, it pays to try to solidify the name that you want to use before the number of places that use it grows too large.

When you extract an interface, you don’t have to extract all of the public methods on the class you are extracting from. *Lean on the Compiler* to find the ones that are being used. 

To *Extract Interface*, follow these steps:
1. Create a new interface with the name you’d like to use. Don’t add any methods to it yet. 
2. Make the class that you are extracting from implement the interface. This can’t break anything because the interface doesn’t have any methods. But it is good to compile and run your test just to verify that. 
3. Change the place where you want to use the object so that it uses the interface rather than the original class.
4. Compile the system and introduce a new method declaration on the interface for each method use that the compiler reports as an error. 

### Introduce Instance Delegator

If you have static methods in your project, chances are good that you won’t run into any trouble with them unless they contain something that is difficult to depend on in a test. (The technical term for this is *static cling*). In these cases, you might wish that you could use an *object seam* to substitute in some other behavior when the static methods are called.

This technique is straightforward enough with many static methods, but when you start to do it with utility classes, you might start to feel uncomfortable. A class with 5 or 10 static methods and only one or two instance methods does look weird. It looks even weirder when they are just simple methods delegating to static methods. But when you use this technique, you can get an object seam in place easily and substitute different behaviors under test. Over time, you might get to the point that every call to the utility class comes through the delegating methods. At that time, you can move the bodies of the static methods into the instance methods and delete the static methods. 

To *Introduce Instance Delegator*, follow these steps:
1. Identify a static method that is problematic to use in a test. 
2. Create an instance method for the method on the class. Remember to *Preserve Signatures*. Make the instance method delegate to the static method. 
3. Find places where the static methods are used in the class you have under test. Use *Parameterize Method* or another dependency-breaking technique to supply an instance to the location where the static method call was made. 

### Introduce Static Setter

The *Singleton Design Pattern* is a pattern that many people use to make sure that there can only be one instance of a particular class in a program. There are three properties that most singletons share: 
1. The constructors of a singleton class are usually made private. 
2. A static member of the class holds the only instance of the class that will ever be created in the program.
3. A static method is used to provide access to the instance. Usually this method is named instance.

Although singletons do prevent people from making more than one instance of a class in production code, they also prevent people from making more than one instance of a class in a test harness. 

Replacing singletons is just a little more work. Add a static setter to the singleton to replace the instance, and then make the constructor protected. You can then subclass the singleton, create a fresh object, and pass it to the setter. 

Using a setter method and a protected constructor on a singleton is mildly invasive, but it does help you get tests in place. Could people misuse the public constructor and make more than one singleton in the production system? Yes, but in my opinion, if it is important to have only one instance of an object in a system, the best way to handle it is to make sure everyone on the team understands that constraint. 

At this point, I’m imagining you with my mind’s eye. You are sitting there disgusted at the carnage that I am wreaking on the system just to be able to get some tests in place. And you are right: These patterns can uglify parts of a system considerably. Surgery is never pretty, particularly at the beginning. What can you do to get the system back to a decent state? 

To *Introduce Static Setter*, follow these steps:
1. Decrease the protection of the constructor so that you can make a fake by subclassing the singleton.
2. Add a static setter to the singleton class. The setter should accept a reference to the singleton class. Make sure that the setter destroys the singleton instance properly before setting the new object.
3. If you need access to private or protected methods in the singleton to set it up properly for testing, consider subclassing it or extracting an interface and making the singleton hold its instance as reference whose type is the type of the interface.

### Link Substitution

Object orientation gives us wonderful opportunities to substitute one object for another. If two classes implement the same interface or have the same superclass, you can substitute one for another pretty easily. Unfortunately, people working in procedural languages such as C don’t have that option.

*Link Substitution* can also be used in Java. Create classes with the same names and methods, and change your classpath so that calls resolve to them rather than the classes with bad dependencies. 

To use *Link Substitution*, follow these steps:
1. Identify the functions or classes that you want to fake. 
2. Produce alternative definitions for them. 
3. Adjust your build so that the alternative definitions are included rather than the production versions. 

### Parametrize Constructor

In languages that allow default arguments, there is a simpler way of doing *Parameterize Constructor*. We can simply add a default argument to the existing constructor.

To *Parameterize Constructor*, follow these steps: 
1. Identify the constructor that you want to parameterize and make a copy of it. 
2. Add a parameter to the constructor for the object whose creation you are going to replace. Remove the object creation and add an assignment from the parameter to the instance variable for the object. 
3. If you can call a constructor from a constructor in your language, remove the body of the old constructor and replace it with a call to the old constructor. Add a new expression to the call of the new constructor in the old constructor. If you can’t call a constructor from another constructor in your language, you may have to extract any duplication among the constructors to a new method. 

### Parametrize Method

In C++, Java, C#, and many other languages, you can have two methods with the same name on a class, as long as the signatures are different. In the example, we take advantage of this and use the same name for the new parameterized method and the original method. Although this saves some work, at times it can be confusing. An alternative is to use the type of the parameter in the name of the new method. For instance, in this case, we could keep `run()` as the name of the original method but call the new method `runWithTestResult(TestResult)`. 

To *Parameterize Method*, follow these steps:
1. Identify the method that you want to replace and make a copy of it. 
2. Add a parameter to the method for the object whose creation you are going to replace. Remove the object creation and add an assignment from the parameter to the variable that holds the object. 
3. Delete the body of the copied method and make a call to the parameterized method, using the object creation expression for the original object.

### Primitivize Parameter

In general, the best way to make a change to a class is to create an instance in a test harness, write a test for the change you want to make, and then make the change to satisfy the test. 

*Primitivize Parameter* leaves code in a rather poor state. Overall, it is better to add the new code to the original class or to use *Sprout Class* to build up some new abstractions that can serve as a base for further work. The only time I use *Primitivize Parameter* is when I feel confident that I will take the time to bring the class under test later. At that point, the function can be folded into the class as a real method. 

To *Primitivize Parameter*, follow these steps: 
1. Develop a free function that does the work you would need to do on the class. In the process, develop an intermediate representation that you can use to do the work.

### Pull Up Feature

From a design point of view, it is less than ideal. We’ve spread a set of features across two classes just to make it easier to test. The spread can be confusing if the relationship among the features in each of the classes isn’t very strong, and that is the case here. We have `Scheduler`, which is responsible for updating scheduling items, and `SchedulingServices`, which is responsible for a variety of things, including getting the default times for items and calculating the dead time. A better factoring would be to have `Scheduler` delegate to some validator object that knows how to talk to the database, but if that step looks too risky to do immediately or there are other bad dependencies, pulling up features is a good first step. If you *Preserve Signatures* and *Lean on the Compiler*, it is far less risky. We can move toward delegation later when more tests are in place. 

To do *Pull Up Feature*, follow these steps:
1. Identify the methods that you want to pull up. 
2. Create an abstract superclass for the class that contains the methods. 
3. Copy the methods to the superclass and compile. 
4. Copy each missing reference that the compiler alerts you about to the new superclass. Remember to *Preserve Signatures* as you do this, to reduce the chance of errors. 
5. When both classes compile successfully, create a subclass for the abstract class and add whatever methods you need to be able to set it up in your tests. 

You might be wondering why we make the superclass abstract. I like to make it abstract so that the code is easier to understand. It is great to be able to look at the code in an application and know that every concrete class is being used. If you search the code and find concrete classes that are not being instantiated anyplace, they could appear to be “dead code.” 

### Push Down Dependency

When you use *Push Down Dependency*, you make your current class abstract. Then you create a subclass that will be your new production class, and you push down all the problematic dependencies into that class. At that point you can subclass your original class to make its methods available for testing.

To *Push Down Dependency*, follow these steps:
1. Attempt to build the class that has dependency problems in your test harness. 
2. Identify which dependencies create problems in the build. 
3. Create a new subclass with a name that communicates the specific environment of those dependencies. 
4. Copy the instance variables and methods that contain the bad dependencies into the new subclass, taking care to preserve signatures. Make methods protected and abstract in your original class, and make your original class abstract. 
5. Create a testing subclass and change your test so that you attempt to instantiate it.
6. Build your tests to verify that you can instantiate the new class. 

### Replace Function with Function Pointer

When you need to break dependencies in procedural languages, you don’t have as many options as you would in object-oriented languages. You can’t use *Encapsulate Global References* or *Subclass and Override Method*. All of those options are closed. You can use *Link Substitution* or *Definition Completion*, but often they are overkill for smaller bouts of dependency breaking. *Replace Function with Function Pointer* is one alternative in languages that support function pointers. The most well-known language with this support is C. 

*Replace Function with Function Pointer* is a good way to break dependencies. One of the nice things about it is that it happens completely at compile time, so it has minimal impact on your build system. 

To use *Replace Function with Function Pointer*, do the following:
1. Find the declarations of the functions you want to replace. 
2. Create function pointers with the same names before each function declaration. 
3. Rename the original function declarations so that their names are not the same as the function pointers you’ve just declared. 
4. Initialize the pointers to the addresses of the old functions in a C file. 
5. Run a build to find the bodies of the old functions. Rename them to the new function names. 

### Replace Global Reference with Getter

To *Replace Global Reference* with Getter, do the following: 
1. Identify the global reference that you want to replace. 
2. Write a getter for the global reference. Make sure that the access protection of the method is loose enough for you to be able to override the getter in a subclass.
3. Replace references to the global with calls to the getter. 
4. Create a testing subclass and override the getter. 

### Subclass and Override Method

*Subclass and Override Method* is a core technique for breaking dependencies in object-oriented programs. In fact, many of the other dependency-breaking techniques in this chapter are variations on it. 
The central idea of *Subclass and Override Method* is that you can use inheritance in the context of a test to nullify behavior that you don’t care about or get access to behavior that you do care about. 

For me, programming is predominately visual. I see all sorts of pictures in my mind when I work, and they help me decide among alternatives. It is a shame that none of these pictures are really UML, but they help me nonetheless.
One image that comes to me often is what I call a paper view. I look at a method and start to see all of the ways that I can group statements and expressions. For just about any little snippet in a method that I can identify, I realize that if I can extract it to a method, I can replace it with something else during testing. It is as if I placed a piece of translucent paper on top of the one with the code. The new sheet can have a different piece of code for the snippet that I want to replace. The stack of paper is what I test, and the methods that I see through the top sheet are the ones that can be executed when I test. 

To *Subclass and Override Method*, do the following: 
1. Identify the dependencies that you want to separate or the place where you want to sense. Try to find the smallest set of methods that you can override to achieve your goals. 
2. Make each method overridable. The way to do this varies among programming languages. In C++, the methods have to be made virtual if they aren’t already. In Java, the methods need to be made non-final. In many .NET languages, you explicitly have to make the method overridable also. 
3. If your language requires it, adjust the visibility of the methods that you will override to so that they can be overridden in a subclass. In Java and C#, methods must at least have protected visibility to be overridden in subclasses. In C++, methods can remain private and still be overridden in subclasses. 
4. Create a subclass that overrides the methods. Verify that you are able to build it in your test harness.

### Supersede Instance Variable

When we override a virtual function in C++, we are replacing the behavior of that function in derived classes just like we’d expect, but with one exception. When a call is made to a virtual function in a constructor, the language doesn’t allow the override. 

For instance, overridden methods can be called from constructors in Java, but I don’t recommend doing it in production code. 

Generally, it is poor practice to provide setters that change the base objects that an object uses. Those setters allow clients to drastically change the behavior of an object during its lifetime. When someone can make those changes, you have to know the history of that object to understand what happens when you call one of its methods. When you don’t have setters, code is easier to understand. 

To *Supersede Instance Variable*, follow these steps: 
1. Identify the instance variable that you want to supersede. 
2. Create a method named `supersedeXXX`, where `XXX` is the name of the variable you want to supersede. 
3. In the method, write whatever code you need to so that you destroy the previous instance of the variable and set it to the new value. If the variable is a reference, verify that there aren’t any other references in the class to the object it points to. If there are, you might have additional work to do in the superceding method to make sure that replacing the object is safe and has the right effect.

### Template Redefinition

Here is a description of how to do `Template Redefinition` in C++. The steps might be different in other languages that support generics, but this description gives a flavor of the technique: 
1. Identify the features that you want to replace in the class you need to test. 
2. Turn the class into a template, parameterizing it by the variables that you need to replace and copying the method bodies up into the header. 
3. Give the template another name. One mechanical way of doing this is to suffix the original name with Impl. 
4. Add a `typedef` statement after the template definition, defining the template with its original arguments using the original class name. 
5. In the test file, include the template definition and instantiate the template on new types that will replace the ones you need to replace for test. 

### Text Redefinition

The Ruby interpreter interprets all lines in a Ruby file as executable statements. The class `Account` statement opens the definition of the `Account` class so that additional definitions can be added to it. The `def report_deposit(value)` statement starts the process of adding a definition to the open class. The Ruby interpreter doesn’t care whether there already is a definition of that method, if there is one; it just replaces it. 

To use *Text Redefinition* in Ruby, follow these steps:
1. Identify a class with definitions that you want to replace. 
2. Add a require clause with the name of the module that contains that class to the top of the test source file. 
3. Provide alternative definitions at the top of the test source file for each method that you want to replace. 

## Appendix: Refactoring

### Extract Method

In poorly maintained code bases, methods tend to grow larger. People add logic to existing methods, and they just continue to grow. As this happens, methods can end up doing two or three different distinct things for their callers. In pathological cases, they can end up doing tens or hundreds. Extract Method is the remedy in these cases. 

When you want to extract a method, the first thing that you need is a set of tests. If you have tests that thoroughly exercise a method, you can extract methods from it using these steps: 
1. Identify the code you want to extract, and comment it out.
2. Think of a name for the new method and create it as an empty method.
3. Place a call to the new method in the old method.
4. Copy the code that you want to extract into the new method 
5. *Lean On the Compiler* to find out what parameters you’ll have to pass and what values you’ll have to return. 
6. Adjust the method declaration to accommodate the parameters and return value (if any). 
7. Run your tests.
8. Delete the commented-out code. 

Although it isn’t strictly necessary, I like to comment out code that I am going to extract; that way, if I make a mistake and a test fails, I can easily go back to what I had, get the test to pass, and then try again. 

*Extract Method* is a core technique for working with legacy code. You can use it to extract duplication, separate responsibilities, and break down long methods. 

## Glossary

* **change point** A place in code where you need to make a change.

* **characterization test** A test written to document the current behavior of a piece of software and preserve it as you change its code. 
* **coupling count** The number of values that pass in and out of a method when it is called. If there is no return value, it is the number of parameters. If there is, it is the number of parameters plus one. Coupling count can be a very useful thing to compute for small methods you’d like to extract if you have to extract without tests.
* **effect sketch** A small hand-drawn sketch that shows what variables and method return values can be affected by a software change. Effect sketches can be useful when you are trying to decide where to write tests. 
* **fake object** An object that impersonates a collaborator of a class during testing. 
* **feature sketch** A small hand-drawn sketch that shows how methods in a class use other methods and instance variables. Feature sketches can be useful when you are trying to decide how to break apart a large class. 
* **free function** A function that is not part of any class. In C and other procedural languages, these are just called functions. In C++ they are called non-member functions. Free functions don’t exist in Java and C#
* **interception point** A place where a test can be written to sense some condition in a piece of software. 
* **link seam** A place where you can vary behavior by linking to a library. In compiled languages, you can replace production libraries, DLLs, assemblies, or JAR files with others during testing to get rid of dependencies or sense some condition that can happen in a test. 
* **mock object** A fake object that asserts conditions internally. 
* **object seam** A place where you can vary behavior by replacing one object with another. In object-oriented languages, you usually do this by subclassing a class in your production code and overriding various methods of the class. 
* **pinch point** A narrowing in an effect sketch that indicates an ideal place to test a cluster of features. 
**programming by difference** A way of using inheritance to add features in object-oriented systems. It can often be used as a way to get a new feature into the system quickly. The tests that you write to provoke the new feature can be used to refactor the code into a better state afterward. 
* **seam** A place where you can vary behavior in a software system without editing in that place. For instance, a call to a polymorphic function on an object is a seam because you can subclass the class of the object and have it behave differently.
* **test-driven development (TDD)** A development process that consists of writing failing test cases and satisfying them one at a time. As you do this, you refactor to keep the code as simple as possible. Code developed using TDD has test coverage, by default. 
* **test harness** A piece of software that enables unit testing.
* **testing subclass** A subclass made to allow access to a class for testing. 
* **unit test** A test that runs in less than 1/10th of a second and is small enough to help you localize problems when it fails. 

