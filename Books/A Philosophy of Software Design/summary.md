# Introduction

All programming requires is a creative mind and the ability to organize your thoughts. The gratest limitation in writing software is our ability to understand the systems that we are creating.

Approaches to eliminate complexity
- make code simple and more obvious
- encapsulate complexity, so that programmers can work on a system without beging exposed to all of its complexity at once --> **Modular Design**

**Definition:** **Compexity** is anthing related to the structure of a software system that makes it hard to understand and modify the system.

Isolating complexity in one place where it will never be seen is almost as good as eliminating the complexity entirely.

**Symptoms**
- A seemingly simple change requires code modifications in many different places.
- Cognitive Load
- Unknown Unknowns: It is not obvious which pieces of code must be modified to complete a task, or what information a developer must have to carry out the task successfully.

**Definition:** A **unknown Unknown** means that there is something you need to know, but there is no way for you to find out what it is, or even whether there is an issue.

Causes of Complexity
- Dependencies (a dependency exists when a given piece of code cannot be understood and modified in isolation)
- Obscurities (an obscurity occurs when important information is not obvious)

# Designing Modules

Modules should be deep. Developers need to face a small fraction of the overall complexity at any given time.

A software system is decomposed into a collection of modules that are relatively independent. Modules can take many forms, such as classes, subsystems, or services. The goal of modular design is to minmize the dependencies between modules. A module has two parts: an interface and an implementation. Theinterface describes what the module does but not how it does it. A developer should not understand the implementations of modules other than the one he or she is working in.

# What's in an interface?

It contains two kinds of information: formal and informal. The formal parts of an interface are specified explicitly in the code. Informal information can only be described using comments (e.g. behaviour of an function). 

Abstraction can help you to make it easier for us to think about and manipulate complex things. The interface presents a simplified view of the module's functionality. An abstraction can go wrong in two ways.
- It can include details that are not really important
- It omits details that really are important

Modules that provide powerful functionality yet have simple interfaces are called **deep**. A **shallow** module is on whose interface is complicated relative to the functionality it provides.

# Classitis

A conventional wisdom in programming is that classes should be small, not deep. "Any method longer than N lines should be divided into multiple methods". This results in large numbers of shallow classes and methods, which add to overall system complexity.

# Conclusion
By separating the interface of a module from its implementation, we can hide the complexity of the implementation from the rest of the system.

# Information Hiding
One of the most important techniques for achieving deep modules is **information hiding**.

The opposite is information leakage. One common case is temporal decomposition: The structure of a system corresponds to the time order in which operations will occur (execution order is reflected in the code structure).

Information leakage occurs when the same knowledge is used in multiple places, such as two different classes that both understand the format of a particular type of file (e.g. a reader and writer functionality belong to the same class). 

When designing modules, focus on the knowledge that's needed to perform each task, not the order in which the tasks occur.

Best Practice Example: get Methods implement data type conversion, e.g. getParameter/getIntParameter

Try to design the private methods within a class so that each method encapsulates some information or capability and hides it from the rest of the class. If you can reduce the number of places where a variable is used, you will eliminate dependencies within the class and reduce its complexity.

# General-Purpose Modules are Deeper
Eliminating special cases can also make code more efficient. The module's functionality should reflect your current needs, but its interface should not. Push specialization upwards **and** downwards. Specialized code should be cleaned separated from the general-purpose code. This can be done by pushing the spezialed code either up or down in the software stack.

Upwards: The top-level classes of an application, which provide specific features, will necessarily be specialized for those features.
Downwards: Example: In order to prevent specialized device characteristics from leaking into the main operating system code, operating system define an interface with general-purpose operations that any secondary storage device must implement.

# Different Layer, different Abstraction

If a system contains adjacent layers with simular abstractions, this is a red flag that suggests a problem with the class decomposition.

Red Flag: A pass-through method is one that die nothing except pass its arguments to another method, usually with the same API as the pass-through method. This typically indicates that there is not a clean division of responsibility between the classes.

Methods with the same signature are not always bad. A dispatcher method is a method that uses its arguments to select one of several other methods to invoke.

# Pull Complexity downwards
It is more important for a module that it has a simple interface rather than having a simple implementation.

# Better together or better apart?
This question applies to a levels in a system, such as functions, methods, classes, and services. Subdividing creates additional complexity that was not present before
- number of components increase
- additional code to manage the components
- Subdivision creates separation
- Subdivision can result in duplication

Few indications that two pieces of code are related
- they share information
- they are used together
- they overlap conceptually

# Define Errors out of Existince
Reduce the number of places where exceptions must be handled. The first approach is to move forward and complete the work in progress in spite of the exception. The second approach is to abort the operation in progress and report the exception upwards.

# Design it twice
You will end up with a much better result if you consider multiple options for each major design decision: design it twice. Try to pick approaches that are radically different from each other. When people are growing up, smart people discover that their first quick idea about any problem is sufficient for a good gradde. This tends to result in bad work habits. This also improves your design skills.

# Comments
If users must read the code of a method in order to use it, then there is no abstraction. If you want to use abstractions to hide complexity, comments are essential. The overall idea behind comments is to capture information that was in the mind of the designer but could not be represented in the code. One of the purposes of comments is to make it unnecessary to read the code. Developers end up effectively retyping the documentation for a method every time they invoke it. Comments should descripe things that are not obvious from the code.
Developers should be able to understand the abstraction provided by a module without reading any code other than its ecternally visible declarations.

Conventions serves two purposes. First, they ensure consistency and seconds, the help to ensure that you actually write comments.

Comment categories:
- Interface Comment
- Data Structure Comment (next to the declaration of a field)
- Implementation Comment (Comment inside the code of a method; are often unnecessary)
- Cross-Module Comment (Comment describing dependencies that cross module boundaries)

If the information in a comment is already obvious from the code next to the comment, then the comment is not helpful.
Lower-level comments add precision: Comments augment the code by providing information at a different level of detail. 
- What is the unit for this variable?
- Are the boundary conditions inclusive or exclusive?
- If a null value is permitted, what does it imply?
- If a variable refers to a resource that must eventually be freed or closed, who is responsible for freeing or closing it?

Higher-level comments enhance intuition. One of the most important roles for comments is to define abstractions. If you want code that presents good abstractions, you must document those abstractions with comments. If interface comments must also describe the implementation, then the class or method is shallow. The main goal of implementation comments is to help readers understand what the code is doing (not how).

The biggest challenge with cross-module documentation is finding a place to put it where it will naturally be discovered by developers.

If a variable or method name is broad enough to refer to many things, then it does not convey much information to the developer and the underlying entity is more likely to be misused. If it is hard to find a name, then it is a hint that the underlying object may not have a clean design. Every word is a name should provide useful information. It is not recommended that the type information is included in the name. The Class name is also not useful. 
Delayed comments are bad comments. For a new class, write the class interface comments first. Comments should be simple and yet complete. If you find it difficult to write such a comments, that is a hint that there may be a problem with the design of the thing you are describing.
Early Comments are fun comments: These comments record and test the quality of the design decisions. Writing comments first will mean that the abstraction will be more stable before you start writing code. This will probably save time during coding. In contrast, if you write the code first, the abstractions will probably evolve as you code, which will require more code revisions than the comments-first approach.

# Modify existing code
When developers go into exiting code, they do not think strategically. They think "What is the smalled possible change I can make that does what I want?". As a result, the system design gets just a bit worse, and the problems accumulate with each step in teh system's evolution. Ideally, when you have finished with each change, the system will have the structure it would have had if you had to designed it from the start with that change in mind. Even if your change does not require refactoring, you should still be on the lookout for design imperfections that you can fix while you are in the code. If you are not making the design better, you are probably making it worse.

When you change existing code, there is a good chance that the changes will invalidate some of the existing comments. The best way to ensure that comments get updated is to position them close to the code they describe. The farther a comment is from the code it describes, the more abstract it should be. When writing a commit message, ask yourself whether developers will need to use the information in the future. If documentation is duplicated, it is more difficult to find and update all the relevant copies. Do not redocument one module's design decision in another module. Don't put comments before a method call that explains what happens in the called method. If information is already documented someplace outside your program, do not repeat the documentation in your program.: just reference it. Check the diffs: Pre-commit scans will detect several other problems, such as accidentally leaving debugging code in the system or failing to fix TODO items. 

It is easier to notice that someone else's code is nonobvious than to see problems with your own code. The best way to determine the obviousness of the code is through code reviews.

Generic Containers: You a new class. Sofware should be designed for ease of reading, not ease of writing.

Developing incrementally is genrally a good idea, but the increments of development should be abstractions, not features. The problem with test-driven development is that it focuses attention on getting specific features working, rather than finding the best design.

Design it all at once ( or at least enough to provide a reasonably comprehensive set of core functions). Zhis is more likely to produce a clean design whose pieces fit together well.

One place where it makes sense to write the test first is when fixing bugs. 
