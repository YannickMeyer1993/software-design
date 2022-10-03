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

A software system is decomposed into a collection of modules that are relatively independent. Modules can take many forms, such as classes, subsystems, or services. The goal of modular design is to minmize the dependencies between modules.