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

Upwards: The top-level classes of an application, which provide specific features, will necessarily be spezialized for those features.
Downwards: Example: In order to prevent specialized device characteristics from leaking into the main operating system code, operating system define an interface with general-purpose operations that any secondary storage device must implement.
