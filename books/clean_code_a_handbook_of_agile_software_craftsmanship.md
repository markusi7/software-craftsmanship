# Clean Code: A Handbook of Agile Software Craftsmanship

## Introduction

* Second, the smallest bit of sloppy construction, of the door that does not close tightly or the slightly crooked tile on the floor, or even the messy desk, completely dispels the charm of the larger whole. That is what clean code is about.

* Cleanliness is next to godliness.

* An ounce of prevention is worth a pound of cure.

* Quality is the result of a million selfless acts of care - not just of any great method that descends from the heavens.

## Chapter 1: Clean Code

* We will never be rid of code, because code represents the details of the requirements. At some level those details cannot be ignored or abstracted; they have to be specified. And specifying requirements in such detail that a machine can execute them is programming. Such a specification is code.

* Remember that code is really the language in which we ultimately express the requirements. We may create languages that are closer to the requirements. We may create tools that help us parse and assemble those requirements into formal structures. But we will never eliminate necessary precision—so there will always be code.

* But the fault, dear Dilbert, is not in our stars, but in ourselves. We are unprofessional. 
This may be a bitter pill to swallow. How could this mess be our fault? What about the requirements? What about the schedule? What about the stupid managers and the useless marketing types? Don’t they bear some of the blame? 
No. The managers and marketers look to us for the information they need to make promises and commitments; and even when they don’t look to us, we should not be shy about telling them what we think. The users look to us to validate the way the requirements will fit into the system. The project managers look to us to help work out the schedule. We are deeply complicit in the planning of the project and share a great deal of the responsibility for any failures; especially if those failures have to do with bad code!

* Indeed, the ratio of time spent reading vs. writing is well over 10:1. 
We are constantly reading old code as part of the effort to write new code. 
Because this ratio is so high, we want the reading of code to be easy, even if it makes the writing harder. Of course there’s no way to write code without reading it, so making it easy to read actually makes it easier to write.

## Chapter 2: Meaningful Names
 
### Use Intention-Revealing Names

* If a name requires a comment, then the name does not reveal its intent.

### Avoid Disinformation
### Make Meaningful Distinctions

* Noise words are redundant.

* Distinguish names in such a way that the reader knows what the differences offer.

### Use Pronounceable Names
### Use Searchable Names

* The length of a name should correspond to the size of its scope.

### Avoid Encodings

* HN was considered to be pretty important back in the Windows C API, when everything was an integer handle or a long pointer or a void pointer, or one of several implementations of “string” (with different uses and attributes). The compiler did not check types in those days, so the programmers needed a crutch to help them remember the types.

* The preceding I, so common in today’s legacy wads, is a distraction at best and too much information at worst. I don’t want my users knowing that I’m handing them an interface. I just want them to know that it’s a `ShapeFactory`. So if I must encode either the interface or the implementation, I choose the implementation. Calling it `ShapeFactoryImp`, or even the hideous `CShapeFactory`, is preferable to encoding the interface.

### Avoid Mental Mapping

* One difference between a smart programmer and a professional programmer is that the professional understands that clarity is king. Professionals use their powers for good and write code that others can understand.

### Class Names

* Classes and objects should have noun or noun phrase names like `Customer`, `WikiPage`, `Account`, and `AddressParser`.

* Avoid words like `Manager`, `Processor`, `Data`, or `Info` in the name of a class.

* A class name should not be a verb.

### Method Names

* Methods should have verb or verb phrase names like `postPayment`, `deletePage`, or `save`.
* Accessors, mutators, and predicates should be named for their value and prefixed with `get`, `set`, and `is` according to the Java Bean standard.

### Don’t Be Cute

* Say what you mean. Mean what you say.

### Pick One Word per Concept

* Pick one word for one abstract concept and stick with it. For instance, it’s confusing to have `fetch`, `retrieve` and `get` as equivalent methods of different classes.

* Likewise, it’s confusing to have a controller and a manager and a driver in the same code base. What is the essential difference between a DeviceManager and a Protocol - Controller? Why are both not controllers or both not managers? Are they both Drivers really? The name leads you to expect two objects that have very different type as well as having different classes.

### Don’t Pun
### Use Solution Domain Names
### Use Problem Domain Names
### Add Meaningful Context
### Don’t Add Gratuitous Context

## Chapter 3: Functions

### Small!!!

* The first rule of functions is that they should be small. The second rule of functions is that they should be smaller than that. 
This also implies that functions should not be large enough to hold nested structures. Therefore, the indent level of a function should not be greater than one or two.

### Do One Thing

* So, another way to know that a function is doing more than _one thing_ is if you can extract another function from it with a name that is not merely a restatement of its implementation.

* Functions that do one thing cannot be reasonably divided into sections.

### One Level of Abstraction per Function 

* We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions. I call this The Step-down Rule.

* To say this differently, we want to be able to read the program as though it were a set of TO paragraphs, each of which is describing the current level of abstraction and referencing subsequent TO paragraphs at the next level down.

### Switch Statements

* My general rule for switch statements is that they can be tolerated if they appear only once, are used to create polymorphic objects, and are hidden behind an inheritance relationship so that the rest of the system can’t see them. Of course every circumstance is unique, and there are times when I violate one or more parts of that rule.

### Use Descriptive Names

* A long descriptive name is better than a long descriptive comment. 

### Function arguments

* The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification—and then shouldn’t be used anyway. 
* When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own.

### Have no side effects

* Side effects are lies. Your function promises to do one thing, but it also does other hidden things. 
* In general output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object. 

### Command Query Separation

* Functions should either do something or answer something, but not both. Either your function should change the state of an object, or it should return some information about that object. 

### Prefer Exceptions to Returning Error Codes

* Try/catch blocks are ugly in their own right. They confuse the structure of the code and mix error processing with normal processing. So it is better to extract the bodies of the try and catch blocks out into functions of their own. 

### Don’t Repeat Yourself

* Duplication may be the root of all evil in software. 

### Structured Programming
### Conclusion

* But never forget that your real goal is to tell the story of the system, and that the functions you write need to fit cleanly together into a clear and precise language to help you with that telling.

## Chapter 4: Comments

* The proper use of comments is to compensate for our failure to express ourself in code. Note that I used the word failure. I meant it. Comments are always failures. We must have them because we cannot always figure out how to express ourselves without them, but their use is not a cause for celebration.

* Truth can only be found in one place: the code. Only the code can truly tell you what it does. It is the only source of truly accurate information. Therefore, though comments are sometimes necessary, we will expend significant energy to minimize them.

### Comments Do Not Make Up for Bad Code
### Explain Yourself In Code
### Good comments

* Legal Comments, Informative Comments, Explanation of Intent, Clarification, Warning of Consequences, TODO Comments, Amplification, Javadocs in Public APIs

### Bad Comments

* Mumbling, Redundant Comments, Misleading Comments, Mandated Comments, Journal Comments, Noice Comments, Scary Noice, Don’t Use a Comment When You Can Use a Function or a Variable, Position Markers, Closing Brace Comments, Attributions and Bylines, HTML Comments, Nonlocal Information, Too Much Information, Inobvious Connection, Function Headers, Javadoc in Nonpublic Code

* It is just plain silly to have a rule that says that every function must have a javadoc, or every variable must have a comment. Comments like this just clutter up the code, propagate lies, and lend to general confusion and disorganization.

* Replace the temptation to create noise with the determination to clean your code. You’ll find it makes you a better and happier programmer.

* Source code control systems are very good at remembering who added what, when. There is no need to pollute the code with little bylines. You might think that such comments would be useful in order to help others know who to talk to about the code. But the reality is that they tend to stay around for years and years, getting less and less accurate and relevant.

* As useful as javadocs are for public APIs, they are anathema to code that is not intended for public consumption. Generating javadoc pages for the classes and functions inside a system is not generally useful, and the extra formality of the javadoc comments amounts to little more than cruft and distraction.

## Chapter 5: Formatting

### The Purpose of Formatting

* Code formatting is important. It is too important to ignore and it is too important to treat religiously. Code formatting is about communication, and communication is the professional developer’s first order of business.

### Vertical Formatting

* Nearly all code is read left to right and top to bottom. Each line represents an expression or a clause, and each group of lines represents a complete thought. Those thoughts should be separated from each other with blank lines.

* Concepts that are closely related should be kept vertically close to each other. Clearly this rule doesn’t work for concepts that belong in separate files. But then closely related concepts should not be separated into different files unless you have a very good reason. Indeed, this is one of the reasons that protected variables should be avoided.

    * __VARIABLE DECLARATIONS__ -> Variables should be declared as close to their usage as possible. Because our functions are very short, local variables should appear a the top of each function.

    * __VARIABLE DECLARATIONS__: -> On the other hand, should be declared at the top of the class. This should not increase the vertical distance of these variables, because in a well-designed class, they are used by many, if not all, of the methods of the class. 

    * __DEPENDENT FUNCTIONS__ -> If one function calls another, they should be vertically close, and the caller should be above the callee, if at all possible. This gives the program a natural flow. If the convention is followed reliably, readers will be able to trust that function definitions will follow shortly after their use. 

    * __CONCEPTUAL AFFINITY__: Certain bits of code want to be near other bits. They have a certain conceptual affinity. The stronger that affinity, the less vertical distance there should be between them.

### Horizontal Formatting

* This suggests that we should strive to keep our lines short. The old Hollerith limit of 80 is a bit arbitrary, and I’m not opposed to lines edging out to 100 or even 120. But beyond that is probably just careless.

* Programmers rely heavily on this indentation scheme. They visually line up lines on the left to see what scope they appear in. This allows them to quickly hop over scopes, such as implementations of if or while statements, that are not relevant to their current situation. They scan the left for new method declarations, new variables, and even new classes. Without indentation, programs would be virtually unreadable by humans.

* Don’t break indentation for short if statements, short while loops, or short functions.

### Team Rules

* Remember, a good software system is composed of a set of documents that read nicely. They need to have a consistent and smooth style. The reader needs to be able to trust that the formatting gestures he or she has seen in one source file will mean the same thing in others. The last thing we want to do is add more complexity to the source code by writing it in a jumble of different individual styles.

## Chapter 6: Objects and Data Structures

### Data Abstractions

* Hiding implementation is not just a matter of putting a layer of functions between the variables. Hiding implementation is about abstractions! A class does not simply push its variables out through getters and setters. Rather it exposes abstract interfaces that allow its users to manipulate the essence of the data, without having to know its implementation.

* We do not want to expose the details of our data. Rather we want to express our data in abstract terms. This is not merely accomplished by using interfaces and/or getters and setters. Serious thought needs to be put into the best way to represent the data that an object contains. The worst option is to blithely add getters and setters.

### Data/Object Anti-Symmetry

* Objects hide their data behind abstractions and expose functions that operate on that data. Data structures expose their data and have no meaningful functions. Go back and read that again. Notice the complimentary nature of the two definitions. They are virtual opposites. This difference may seem trivial, but it has far-reaching implications. 

* Procedural code (code using data structures) makes it easy to add new functions without changing the existing data structures. OO code, on the other hand, makes it easy to add new classes without changing existing functions. 

* Procedural code makes it hard to add new data structures because all the functions must change. OO code makes it hard to add new functions because all the classes must change. 

### The Law of Demeter

* There is a well-known heuristic called the __Law of Demeter__ that says a module should not know about the innards of the objects it manipulates. 
* More precisely, the Law of Demeter says that a method f of a class C should only call the methods of these: C, an object created by f, an object passed as an argument to f, an object held in an instance variable of C 

* _Train Wrecks_: This kind of code is often called a train wreck because it look like a bunch of coupled train cars. Chains of calls like this are generally considered to be sloppy style and should be avoided. It is usually best to split them up.

* Whether this is a violation of Demeter depends on whether or not `ctxt` , `Options`, and `ScratchDir` are objects or data structures. If they are objects, then their internal structure should be hidden rather than exposed, and so knowledge of their innards is a clear violation of the Law of Demeter. On the other hand, if `ctxt`, `Options` and `ScratchDir` are just data structures with no behavior, then they naturally expose their internal structure, and so Demeter does not apply. 

* _Hybrid_: This confusion sometimes leads to unfortunate hybrid structures that are half object and half data structure. They have functions that do significant things, and they also have either public variables or public accessors and mutators that, for all intents and purposes, make the private variables public, tempting other external functions to use those variables the way a procedural program would use a data structure. 

### Data Transfer Objects

* The quintessential form of a data structure is a class with public variables and no functions. This is sometimes called a data transfer object, or DTO. DTOs are very useful structures, especially when communicating with databases or parsing messages from sockets, and so on. They often become the first in a series of translation stages that convert raw data in a database into objects in the application code. 

* __Active Record__ Active Records are special forms of DTOs. They are data structures with public (or bean-accessed) variables; but they typically have navigational methods like save and find. Typically these Active Records are direct translations from database tables, or other data sources. 

### Conclusion

* Objects expose behavior and hide data. This makes it easy to add new kinds of objects without changing existing behaviors. It also makes it hard to add new behaviors to existing objects. Data structures expose data and have no significant behavior. This makes it easy to add new behaviors to existing data structures but makes it hard to add new data structures to existing functions. 

* In any given system we will sometimes want the flexibility to add new data types, and so we prefer objects for that part of the system. Other times we will want the flexibility to add new behaviors, and so in that part of the system we prefer data types and procedures. Good software developers understand these issues without prejudice and choose the approach that is best for the job at hand. 

## Chapter 7: Error Handling

### Use Exceptions Rather Than Return Codes
### Write Your Try-Catch-Finally Statement First

* In a way, try blocks are like transactions. Your catch has to leave your program in a consistent state, no matter what happens in the try. For this reason it is good practice to start with a try-catch-finally statement when you are writing code that could throw exceptions. This helps you define what the user of that code should expect, no matter what goes wrong with the code that is executed in the try. 

* Try to write tests that force exceptions, and then add behavior to your handler to satisfy your tests. This will cause you to build the transaction scope of the try block first and will help you maintain the transaction nature of that scope. 

### Use Unchecked Exceptions

* The price of checked exceptions is an Open/Closed Principle violation. If you throw a checked exception from a method in your code and the catch is three levels above, you must declare that exception in the signature of each method between you and the catch. This means that a change at a low level of the software can force signature changes on many higher levels. The changed modules must be rebuilt and redeployed, even though nothing they care about changed. 

* Checked exceptions can sometimes be useful if you are writing a critical library: You must catch them. But in general application development the dependency costs outweigh the benefits. 

### Provide Context With Exceptions
### Define Exception Classes in Terms of a Caller’s Needs

* Wrappers like the one we defined for ACMEPort can be very useful. In fact, wrapping third-party APIs is a best practice. When you wrap a third-party API, you minimize your dependencies upon it: You can choose to move to a different library in the future without much penalty. Wrapping also makes it easier to mock out third-party calls when you are testing your own code. 

* One final advantage of wrapping is that you aren’t tied to a particular vendor’s API design choices. You can define an API that you feel comfortable with. In the preceding example, we defined a single exception type for port device failure and found that we could write much cleaner code. 

* Often a single exception class is fine for a particular area of code. The information sent with the exception can distinguish the errors. Use different classes only if there are times when you want to catch one exception and allow the other one to pass through. 

### Define the Normal Flow

* This is called the __SPECIAL CASE PATTERN__ [Fowler]. You create a class or configure an object so that it handles a special case for you. When you do, the client code doesn’t have to deal with exceptional behavior. That behavior is encapsulated in the special case object. 

### Don’t Return Null
### Don’t Pass Null
### Conclusion

* Clean code is readable, but it must also be robust. These are not conflicting goals. We can write robust clean code if we see error handling as a separate concern, something that is viewable independently of our main logic. To the degree that we are able to do that, we can reason about it independently, and we can make great strides in the maintainability of our code.

## Chapter 8: Boundaries

### Using Third-Party Code

* We are not suggesting that every use of Map be encapsulated in this form. Rather, we are advising you not to pass Maps (or any other interface at a boundary) around your system. If you use a boundary interface like Map, keep it inside the class, or close family of classes, where it is used. Avoid returning it from, or accepting it as an argument to, public APIs. 

### Exploring and Learning Boundaries

* Jim Newkirk calls such tests learning tests.
In learning tests we call the third-party API, as we expect to use it in our application. We’re essentially doing controlled experiments that check our understanding of that API. The tests focus on what we want out of the API. 

### Learning log4j
### Learning Tests Are Better Than Free
### Using Code That Does Not Yet Exist
### Clean Boundaries

* Interesting things happen at boundaries. Change is one of those things. Good software designs accommodate change without huge investments and rework. When we use code that is out of our control, special care must be taken to protect our investment and make sure future change is not too costly.

* Code at the boundaries needs clear separation and tests that define expectations. We should avoid letting too much of our code know about the third-party particulars. It’s better to depend on something you control than on something you don’t control, lest it end up controlling you.

 * We manage third-party boundaries by having very few places in the code that refer to them. We may wrap them as we did with Map, or we may use an ADAPTER to convert from our perfect interface to the provided interface. Either way our code speaks to us better, promotes internally consistent usage across the boundary, and has fewer maintenance points when the third-party code changes. 

## Chapter 9: Unit Tests

### The Three Laws of TDD

1. You may not write production code until you have written a failing unit test.
2. You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
3. You may not write more production code than is sufficient to pass the currently failing test.

### Keeping Tests Clean

* The moral of the story is simple: Test code is just as important as production code. It is not a second-class citizen. It requires thought, design, and care. It must be kept as clean as production code. 

* If you don’t keep your tests clean, you will lose them. And without them, you lose the very thing that keeps your production code flexible. Yes, you read that correctly. It is unit tests that keep our code flexible, maintainable, and reusable. The reason is simple. If you have tests, you do not fear making changes to the code! Without tests every change is a possible bug. No matter how flexible your architecture is, no matter how nicely partitioned your design, without tests you will be reluctant to make changes because of the fear that you will introduce undetected bugs. 

### Clean Tests

* What makes a clean test? Three things. Readability, readability, and readability. Readability is perhaps even more important in unit tests than it is in production code. What makes tests readable? The same thing that makes all code readable: clarity, simplicity, and density of expression. In a test you want to say a lot with as few expressions as possible. 

* The BUILD-OPERATE-CHECK pattern is made obvious by the structure of these tests. Each of the tests is clearly split into three parts. The first part builds up the test data, the second part operates on that test data, and the third part checks that the operation yielded the expected results. 

* That is the nature of the dual standard. There are things that you might never do in a production environment that are perfectly fine in a test environment. Usually they involve issues of memory or CPU efficiency. But they never involve issues of cleanliness.

### One Assert Per Test. 

* I think the single assert rule is a good guideline. I usually try to create a domain-specific testing language that supports it, as in Listing 9-5. But I am not afraid to put more than one assert in a test. I think the best thing we can say is that the number of asserts in a test ought to be minimized. 

* So it’s not the multiple asserts in each section of Listing 9-8 that causes the problem. Rather it is the fact that there is more than one concept being tested. So probably the best rule is that you should minimize the number of asserts per concept and test just one concept per test function. 

### F.I.R.S.T.
Fast, Independent, Repeatable, Self-Validating, Timely

### Conclusion

* Tests are as important to the health of a project as the production code is. Perhaps they are even more important, because tests preserve and enhance the flexibility, maintainability, and reusability of the production code. So keep your tests constantly clean. Work to make them expressive and succinct. Invent testing APIs that act as domain-specific language that helps you write the tests. 
If you let the tests rot, then your code will rot too. Keep your tests clean. 

## Chapter 10: Classes

###  Class Organization
### Classes Should Be Small!

* The name of a class should describe what responsibilities it fulfills. In fact, naming is probably the first way of helping determine class size. If we cannot derive a concise name for a class, then it’s likely too large. The more ambiguous the class name, the more likely it has too many responsibilities. For example, class names including weasel words like `Processor` or `Manager` or `Super` often hint at unfortunate aggregation of responsibilities. 

* The __Single Responsibility Principle (SRP)__ states that a class or module should have one, and only one, reason to change. This principle gives us both a definition of responsibility, and a guidelines for class size. Classes should have one responsibility — one reason to change. 

* So the question is: Do you want your tools organized into toolboxes with many small drawers each containing well-defined and well-labeled components? Or do you want a few drawers that you just toss everything into? 

* Classes should have a small number of instance variables. Each of the methods of a class should manipulate one or more of those variables. In general the more variables a method manipulates the more cohesive that method is to its class. A class in which each variable is used by each method is maximally cohesive. 

### Organizing for Change

* Our restructured SQL logic represents the best of all worlds. It supports the SRP. It also supports another key OO class design principle known as the __Open-Closed Principle__, or OCP. Classes should be open for extension but closed for modification. Our restructured SQL class is open to allow new functionality via subclassing, but we can make this change while keeping every other class closed. We simply drop our UpdateSql class in place. 

* We want to structure our systems so that we muck with as little as possible when we update them with new or changed features. In an ideal system, we incorporate new features by extending the system, not by making modifications to existing code. 

* By minimizing coupling in this way, our classes adhere to another class design principle known as the __Dependency Inversion Principle__  (DIP). In essence, the DIP says that our classes should depend upon abstractions, not on concrete details. 
Instead of being dependent upon the implementation details of the `TokyoStock` - Exchange class, our `Portfolio` class is now dependent upon the `StockExchange` interface. The `StockExchange` interface represents the abstract concept of asking for the current price of a symbol. This abstraction isolates all of the specific details of obtaining such a price, including from where that price is obtained. 

## Chapter 11: Systems

### How Would You Build a City?
### Separate Constructing a System from Using It

* Software systems should separate the startup process, when the application objects are constructed and the dependencies are _wired_ together, from the runtime logic that takes over after startup. 

* A powerful mechanism for separating construction from use is __Dependency Injection__ (DI), the application of __Inversion of Control __ (IoC) to dependency management. Inversion of Control moves secondary responsibilities from an object to other objects that are dedicated to the purpose, thereby supporting the Single Responsibility Principle. In the context of dependency management, an object should not take responsibility for instantiating dependencies itself. Instead, it should pass this responsibility to another _authoritative_ mechanism, thereby inverting the control. 

* It is a myth that we can get systems _right the first time_. Instead, we should implement only today’s stories, then refactor and expand the system to implement new stories tomorrow. This is the essence of iterative and incremental agility. Test-driven development, refactoring, and the clean code they produce make this work at the code level. 

### Scaling Up

* In principle, you can reason about your persistence strategy in a modular, encapsulated way. Yet, in practice, you have to spread essentially the same code that implements the persistence strategy across many objects. We use the term cross-cutting concerns for concerns like these. Again, the persistence framework might be modular and our domain logic, in isolation, might be modular. The problem is the fine-grained intersection of these domains. 

### Java Proxies
### Pure Java AOP Frameworks
### AspectJ Aspects
### Test Drive the System Architecture

* The power of separating concerns through aspect-like approaches can’t be overstated. If you can write your application’s domain logic using POJOs, decoupled from any architecture concerns at the code level, then it is possible to truly test drive your architecture. You can evolve it from simple to sophisticated, as needed, by adopting new technologies on demand. It is not necessary to do a Big Design Up Front (BDUF). In fact, BDUF is even harmful because it inhibits adapting to change, due to the psychological resistance to discarding prior effort and because of the way architecture choices influence subsequent thinking about the design. 

* Of course, this does not mean that we go into a project _rudderless_. We have some expectations of the general scope, goals, and schedule for the project, as well as the general structure of the resulting system. However, we must maintain the ability to change course in response to evolving circumstances. 

* An optimal system architecture consists of modularized domains of concern, each of which is implemented with Plain Old Java (or other) Objects. The different domains are integrated together with minimally invasive Aspects or Aspect-like tools. This architecture can be test-driven, just like the code. 

### Optimize Decision Making

* Modularity and separation of concerns make decentralized management and decision making possible. In a sufficiently large system, whether it is a city or a software project, no one person can make all the decisions. 

* We all know it is best to give responsibilities to the most qualified persons. We often forget that it is also best to postpone decisions until the last possible moment. This isn’t lazy or irresponsible; it lets us make informed choices with the best possible information. A premature decision is a decision made with suboptimal knowledge. We will have that much less customer feedback, mental reflection on the project, and experience with our implementation choices if we decide too soon. 

* The agility provided by a POJO system with modularized concerns allows us to make optimal, just-in-time decisions, based on the most recent knowledge. The complexity of these decisions is also reduced. 

### Use Standards Wisely, When They Add _Demonstrable_ Value
### Systems Need Domain-Specific Languages

* Building construction, like most domains, has developed a rich language with a vocabulary, idioms, and patterns that convey essential information clearly and concisely. In software, there has been renewed interest recently in creating Domain-Specific Languages (DSLs), which are separate, small scripting languages or APIs in standard languages that permit code to be written so that it reads like a structured form of prose that a domain expert might write.

* A good DSL minimizes the _communication gap_ between a domain concept and the code that implements it, just as agile practices optimize the communications within a team and with the project’s stakeholders. If you are implementing domain logic in the same language that a domain expert uses, there is less risk that you will incorrectly translate the domain into the implementation.

* DSLs, when used effectively, raise the abstraction level above code idioms and design patterns. They allow the developer to reveal the intent of the code at the appropriate level of abstraction.
Domain-Specific Languages allow all levels of abstraction and all domains in the applicttion to be expressed as POJOs, from high-level policy to low-level details.

### Conclusion

## Chapter 12: Emergence

### Getting Clean via Emergent Design

* According to Kent, a design is _simple_ if it follows these rules:
    * Runs all the tests
    * Contains no duplication 
    * Expresses the intent of the programmer
    * Minimizes the number of classes and methods 
* The rules are given in order of importance.

### Simple Design Rule 1: Runs All the Tests

* First and foremost, a design must produce a system that acts as intended. A system might have a perfect design on paper, but if there is no simple way to verify that the system actually works as intended, then all the paper effort is questionable.

* A system that is comprehensively tested and passes all of its tests all of the time is a testable system. That’s an obvious statement, but an important one. Systems that aren’t testable aren’t verifiable. Arguably, a system that cannot be verified should never be deployed.

* Fortunately, making our systems testable pushes us toward a design where our classes are small and single purpose. It’s just easier to test classes that conform to the SRP. The more tests we write, the more we’ll continue to push toward things that are simpler to test. So making sure our system is fully testable helps us create better designs.

* Tight coupling makes it difficult to write tests. So, similarly, the more tests we write, the more we use principles like DIP and tools like dependency injection, interfaces, and abstraction to minimize coupling. Our designs improve even more.

* Remarkably, following a simple and obvious rule that says we need to have tests and run them continuously impacts our system’s adherence to the primary OO goals of low coupling and high cohesion. Writing tests leads to better designs.

### Simple Design Rules 2-4: Refactoring
### No Duplication
### Expressive
### Minimal Classes and Methods
### Conclusion

## Chapter 13: Concurrency

### Why Concurrency?

* Concurrency is a decoupling strategy. It helps us decouple what gets done from when it gets done. 

    * Myths and Misconceptions

        * _Concurrency always improves performance._ -> Concurrency can sometimes improve performance, but only when there is a lot of wait time that can be shared between multiple threads or multiple processors. Neither situation is trivial.

        * _Design does not change when writing concurrent programs._ ->  In fact, the design of a concurrent algorithm can be remarkably different from the design of a single-threaded system. The decoupling of what from when usually has a huge effect on the structure of the system.

        * _Understanding concurrency issues is not important when working with a container such as a Web or EJB container_. -> In fact, you’d better know just what your container is doing and how to guard against the issues of concurrent update and deadlock described later in this Chapter. 

        * _Concurrency incurs some overhead, both in performance as well as writing additional code._

        * _Correct concurrency is complex, even for simple problems._

        * _Concurrency bugs aren’t usually repeatable, so they are often ignored as one-offs instead of the true defects they are._

        * _Concurrency often requires a fundamental change in design strategy._

### Concurrency Defense Principles

* Single Responsibility Principle
* Limit the Scope of Data
* Use Copies of Data
* Threads Should Be as Independent as Possible

### Know Your Library
### Know Your Execution Models

* Bound Resources, Mutual Exclusion, Starvation, Deadlock, Livelock

* Producer-Consumer, Readers-Writers, Dining Philosophers

### Beware Dependencies Between Synchronized Methods
### Keep Synchronized Sections Small
### Writing Correct Shut-Down Code Is Hard
### Testing Threaded Code

* Treat Spurious Failures as Candidate Threading Issues
* Get Your Nonthreaded Code Working First
* Make Your Threaded Code Pluggable
* Run With More Threads Than Processors
* Run on Different Platforms
* Instrument Your Code to Try and Force Failures

### Conclusion

* Concurrent code is difficult to get right. Code that is simple to follow can become nightmarish when multiple threads and shared data get into the mix. If you are faced with writing concurrent code, you need to write clean code with rigor or else face subtle and infrequent failures. 

## Chapter 14: Successive refinement

### Args Implementation

* If we have learned anything over the last couple of decades, it is that programming is a craft more than it is a science. To write clean code, you must first write dirty code and then clean it. 

### Args: The Rough Draft

* One of the best ways to ruin a program is to make massive changes to its structure in the name of improvement. Some programs never recover from such _improvements_. The problem is that it’s very hard to get the program working the same way it worked before the _improvement_.

* To avoid this, I use the discipline of Test-Driven Development (TDD). One of the central doctrines of this approach is to keep the system running at all times. In other words, using TDD, I am not allowed to make a change to the system that breaks that system. Every change I make must keep the system working as it worked before. 

### String Arguments

* Refactoring is a lot like solving a Rubik’s cube. There are lots of little steps required to achieve a large goal. Each step enables the next. 

* Much of good software design is simply about partitioning — creating appropriate places to put different kinds of code. This separation of concerns makes the code much simpler to understand and maintain. 

### Conclusion

* It is not enough for code to work. Code that works is often badly broken. Programmers who satisfy themselves with merely working code are behaving unprofessionally. They may fear that they don’t have time to improve the structure and design of their code, but I disagree. Nothing has a more profound and long-term degrading effect upon a development project than bad code. Bad schedules can be redone, bad requirements can be redefined. Bad team dynamics can be repaired. But bad code rots and ferments, becoming an inexorable weight that drags the team down. Time and time again I have seen teams grind to a crawl because, in their haste, they created a malignant morass of code that forever thereafter dominated their destiny.

* Of course bad code can be cleaned up. But it’s very expensive. As code rots, the modules insinuate themselves into each other, creating lots of hidden and tangled dependencies. Finding and breaking old dependencies is a long and arduous task.

* On the other hand, keeping code clean is relatively easy. If you made a mess in a module in the morning, it is easy to clean it up in the afternoon. Better yet, if you made a mess five minutes ago, it’s very easy to clean it up right now. 
So the solution is to continuously keep your code as clean and simple as it can be. Never let the rot get started. 

## Chapter 15: The JUnit Framework

### The JUnit Framework

* Unencapsulated conditionals
* Negatives are harder to understand than positives.
* Using consistent conventions.
* Hidden temporal coupling.
* Refactoring is an iterative process full of trial and error, inevitably converging on something that we feel is worthy of a professional.

### Conclusion

## Chapter 16: Refactoring SerialDate

* No, this is not an activity of nastiness or arrogance. What I am about to do is nothing more and nothing less than a professional review. It is something that we should all be comfortable doing. And it is something we should welcome when it is done for us. It is only through critiques like these that we will learn. Doctors do it. Pilots do it. Lawyers do it. And we programmers need to learn how to do it too. 

### First, Make It Work
### Then Make It Right

* This comment has four languages in it: Java, English, Javadoc and HTML.

* Redundant comments are just places to collect lies and misinformation.

* The dilemma is that a user of an abstract class needs information about its implementation.

* It is usually a bad idea to pass a flag as an argument to a function, especially when that flag simply selects the format of the output.

### Conclusion

## Chapter 17: Smells and Heuristics

### Comments

* **C1: _Inappropriate Information_** -> Information which could be better held in a different kind of system such as VCS.
* **C2: _Obsolete Comment_** -> It’s best not to write a comment that will become obsolete.
* **C3: _Redundant Comment_** -> Comments should say things that the code cannot say for itself.
* **C4: _Poorly Written Comment_** -> A comment worth writing is worth writing well.
* **C5: _Commented-Out Code_** -> Commented-out code is an abomination.

### Environment

* **E1: _Build Requires More Than One Step_** -> Building a project should be a single trivial operation.
* **E2: _Test Require More Than One Step_** -> You should be able to run all the tests with just one command.

### Functions

* **F1: _Too Many Arguments_** -> No arguments is best, followed by one, two, and three.
* **F2: _Output Arguments_** -> Output arguments are counterintuitive.
* **F3: _Flag Arguments_** -> Boolean arguments loudly declare that the functions does more than one thing.
* **F4: _Dead Function_** -> Keeping dead code around is wasteful.

### General

* **G1: _Multiple Languages In One Source File_**
* **G2: _Obvious Behavior Is Unimplemented_** -> Following POLA, any function or class should implement the behaviors that another programmer could reasonably expect.
* **G3: _Incorrect Behavaior at the Boundaries_** -> Don’t rely on your intuition. Look for every boundary condition and write a test for it.
* **G4: _Overriden Safeties_** -> Turning off failing tests and telling yourself you’ll get them to pass later is ad bad as pretending your credit cards are free money.
* **G5: _Code Duplication_** -> Find and eliminate duplication wherever you can.
* **G6: _Code at Wrong Level of Abstraction_** -> The point is that you cannot lie or fake your way out of a misplaced abstraction. Isolating abstractions is one of the hardest things that software developers do, and there is no quick fix when you get it wrong.
* **G7: _Base Classes Depending on Their Derivatives_**-> Base classes should know nothing about their derivatives. Sealed classes could be an exception to the rule.
* **G8: _Too Much Information_** -> Hide your data. Hide your utility functions. Hide your constants and your temporaries. Don’t create classes with lots of methods of lots of instance variables. Don’t create lots of protected variables and functions for your subclasses. Concentrate on keeping interfaces very tight and very small. Help keep coupling low by limiting information.
* **G9: _Dead Code_** -> When you find dead code, do the right thing. Give it a decent burial.
* **G10: _Vertical Separation_** -> Variables and function should be defined close to where they are used.
* **G11: _Inconsistency_** -> If you do something a certain way, do all similar things in the same way.
* **G12: _Clutter_**-> Keep your source files clean, well organized, and free of clutter.
* **G13: _Artificial Coupling_** -> Take the time to figure out where functions, constants, and variables ought to be declared.
* **G14: _Feature Envy_** -> The methods of a class should be interested in the variables and functions of the class they belong to, and not the variables and functions of other classes. When a method uses accessors and mutators of some other object to manipulate the data within that object, the it envies the scope of the class of that other object.
* **G15: _Selector Arguments_** -> Of course, selectors need no to be boolean. They can be enums, integers, or any other type of argument that is used to select the behavior of the function. In general it is better to have many functions than to pass some code into a function to select the behavior.
* **G16: _Obscured Intent_** -> We want code to be as expressive as possible. Run-on expressions, Hungarian notation and magic numbers all obscure the author’s intent.
* **G17: _Misplaced Responsibility_** -> Code should be placed where a reader would naturally expect it to be.
* **G18: _Inappropriate Static_** -> In general you should prefer nonstatic methods to static methods. When in doubt, make the function nonstatic. If you really want a function to be static, make sure that there is no chance that you’ll want it to behave polymorphically.
* **G19: _Use Explanatory Variables_** -> More explanatory variables are generally better than fewer. It is remarkable how an opaque module can suddenly become transparent simply by breaking the calculations up into well-named intermediate values.
* **G20: _Function Names Should Say What They Do_** -> If you have to look at the implementation (or documentation) of the function to know what it does, then you should work to find a better name or rearrange the functionality so that it can be placed in functions with better names.
* **G21: _Understand the Algorithm_** -> Before you consider yourself to be done with a function, make sure you understand how it works. It is not good enough that it passes all the tests. You must know that the solution is correct.
* **G22: _Make Logical Dependencies Physical_** -> If one module depends upon another, that dependency should be physical, not just logical. The dependent module should not make assumptions (in other words, logical dependencies) about the module it depends upon. Rather it should explicitly ask that module for all the information it depends upon. 
* **G23: _Prefer Polymorphism to If/Else or Switch/Case_** -> There may be no more than one switch statement for a given type of selection. The cases in that switch statement must create polymorphic objects that take the place of other such switch statements in the rest of the system. 
* **G24: _Follow Standard Conventions_** -> Every team should follow a coding standard based on common industry norms. 
* **G25: _Replace Magic Numbers with named Constants_** -> In general it is a bad idea to have raw numbers in your code. You should hide them behind well-named constants. The term “Magic Number” does not apply only to numbers. It applies to any token that has a value that is not self-describing. 
* **G26: _Be Precise_** -> When you make a decision in your code, make sure you make it precisely. Know why you have made it and how you will deal with any exceptions. Ambiguities and imprecision in code are either a result of disagreements or laziness. In either case they should be eliminated. 
* **G27: _Structure over Convention_** -> Enforce design decisions with structure over convention. Naming conventions are good, but they are inferior to structures that force compliance. 
* **G28: _Encapsulate Conditionals_** -> Extract functions that explain the intent of the conditionals.
* **G29: _Avoid Negative Conditionals_** -> So, when possible, conditionals should be expressed as positives.
* **G30: _Functions Should Do One Thing_** -> Functions of this kind do more than one thing, and should be converted into many smaller functions, each of which does one thing.
* **G31: _Hidden Temporal Couplings_** -> This exposes the temporal coupling by creating a bucket brigade. Each function produces a result that the next function needs, so there is no reasonable way to call them out of order. You might complain that this increases the complexity of the functions, and you’d be right. But that extra syntactic complexity exposes the true temporal complexity of the situation.
* **G22: _Don’t Be Arbitrary_** -> Have a reason for the way you structure your code, and make sure that reason is communicated by the structure of the code. If a structure appears arbitrary, others will feel empowered to change it.
* **G33: _Encapsulate Boundary Conditions_** -> Boundary conditions are hard to keep track of. Put the processing for them in one place. Don’t let them leak all over the code.
* **G34: _Functions Should Descend Only One Level of Abstraction_** -> The statements within a function should all be written at the same level of abstraction, which should be one level below the operation described by the name of the function.
* **G35: _Keep Configurable Data at High Levels_** -> The configuration constants reside at a very high level and are easy to change. They get passed down to the rest of the application. The lower levels of the application do not own the values of these constants.
* **G36: _Avoid Transitive Navigation_** -> This is sometimes called the Law of Demeter. The Pragmatic Programmers call it _Writing Shy Code_. In either case it comes down to making sure that modules know only about their immediate collaborators and do not know the navigation map of the whole system.

### Java

 * **J1: _Avoid Long Import Lists by Using Wildcards_** -> If you use two or more classes from a package, then import the whole package with `import package.*;`. Long lists of imports are daunting to the reader. We don’t want to clutter up the tops of our modules with 80 lines of imports. Rather we want the imports to be a concise statement about which packages we collaborate with. Specific imports are hard dependencies, whereas wildcard imports are not. If you specifically import a class, then that class must exist. But if you import a package with a wild- card, no particular classes need to exist. The import statement simply adds the package to the search path when hunting for names. So no true dependency is created by such imports, and they therefore serve to keep our modules less coupled. 
* **J2: _Don’t Inherit Constants_** -> This is a hideous practice! The constants are hidden at the top of the inheritance hierarchy. Ick! Don’t use inheritance as a way to cheat the scoping rules of the language. Use a static import instead. 
* **J3: _Constants versus Enums_** -> What’s more, study the syntax for enums carefully. They can have methods and fields. This makes them very powerful tools that allow much more expression and flexibility than ints. 

### Names

* **N1: _Choose Descriptive Names_** -> Don’t be too quick to choose a name. Make sure the name is descriptive. Remember that meanings tend to drift as software evolves, so frequently reevaluate the appropriateness of the names you choose. This is not just a “feel-good” recommendation. Names in software are 90 percent of what make software readable. You need to take the time to choose them wisely and keep them relevant. Names are too important to treat carelessly. 
* **N2: _Choose Names at the Appropriate Level of Abstraction_** -> Don’t pick names that communicate implementation; choose names the reflect the level of abstraction of the class or function you are working in. 
* **N3: _Use Standard Nomenclature Where Possible_** -> In short, the more you can use names that are overloaded with special meanings that are relevant to your project, the easier it will be for readers to know what your code is talking about.
* **N4: _Unambiguous Names_** -> Choose names that make the workings of a function or variable unambiguous.
* **N5: _Use Long Names for Long Scopes_** -> The length of a name should be related to the length of the scope. You can use very short 
variable names for tiny scopes, but for big scopes you should use longer names.
* **N6: _Avoid Encodings_** -> Again, today’s environments provide all that information without having to mangle the names. Keep your names free of Hungarian pollution.
* **N7: _Names Should Describe Side-Effects_** -> Names should describe everything that a function, variable, or class is or does. Don’t hide side effects with a name. Don’t use a simple verb to describe a function that does more than just that simple action.

### Tests

* **T1: _Insufficient Tests_** -> A test suite should test everything that could possibly break. The tests are insufficient so long as there are conditions that have not been explored by the tests or calculations that have not been validated. 
* **T2: _Use a Coverage Tool!_** -> Coverage tools reports gaps in your testing strategy. They make it easy to find modules, classes, and functions that are insufficiently tested. 
* **T3: _Don’t Skip Trivial Tests_**  -> They are easy to write and their documentary value is higher than the cost to produce them. 
* **T4: _An Ignored Test Is a Question about an Ambiguity_** -> Sometimes we are uncertain about a behavioral detail because the requirements are unclear. We can express our question about the requirements as a test that is commented out, or as a test that annotated with `@Ignore`. Which you choose depends upon whether the ambiguity is about something that would compile or not. 
* **T5: _Test Boundary Conditions_** -> Take special care to test boundary conditions. We often get the middle of an algorithm right but misjudge the boundaries. 
* **T6: _Exhaustively Test Near Bugs_** -> Bugs tend to congregate. When you find a bug in a function, it is wise to do an exhaustive test of that function. You’ll probably find that the bug was not alone. 
* **T7: _Patterns of Failure Are Revealing_** -> Sometimes you can diagnose a problem by finding patterns in the way the test cases fail. This is another argument for making the test cases as complete as possible. Complete test cases, ordered in a reasonable way, expose patterns. 
* **T8: _Test Coverage Patterns Can Be Revealing_** -> Looking at the code that is or is not executed by the passing tests gives clues to why the failing tests fail. 
* **T9: _Tests Should Be Fast_** -> A slow test is a test that won’t get run. When things get tight, it’s the slow tests that will be dropped from the suite. So do what you must to keep your tests fast. 

### Conclusion

* This list of heuristics and smells could hardly be said to be complete. Indeed, I’m not sure that such a list can ever be complete. But perhaps completeness should not be the goal, because what this list does do is imply a value system. 

* Indeed, that value system has been the goal, and the topic, of this book. Clean code is not written by following a set of rules. You don’t become a software craftsman by learning a list of heuristics. Professionalism and craftsmanship come from values that drive disciplines. 


