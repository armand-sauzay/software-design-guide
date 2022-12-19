# Software Design Guide
This repository aims at defining a set of practices to improve your code. Some
rules are general and some apply to specific programming languages. 

## General Code Principles
Here are a few principles that mostly are language agnostic and that can help improve your code:
- __Lint__
    - Find a set of rules to write code and try to abide by it or enforce it (through pre-commit for instance).
    - Include linting as part of your CI.
- __Test__
    - As a general rule try to write as much test code as actual code.
    - Include testing as part of your CI.
- __Release__
    - Your code should have releases and versioning. 
    - You can use semantic versioning.
- __Document__
    - Document your code.
- __Don't Repeat Yourself (DRY).__
    - It’s ok to write code once or twice (maybe). But more than this you should change the implementation
- __Premature abstraction is as dangerous as premature optimization__
    - Don't try to abstract too early. 
    - Don't try to optimize too early.
- __Focus on readability__
    - Non readable code translates to non-maintainable code, so it should not be long before it is useless.
    - Document your code.
    - Use descriptive and meaningful variable and function names
    - Limit nesting
        - "if you need more than 3 levels of indentation, you're screwed anyway, and should fix your program." - Linus Torvalds (in relation with 8 space indentation for the linux kernel style)
        - Use extraction: when a subpart of your code becomes too large, extract it and turn it into its own function.
        - Use inversion: limit conditions and put the "unhappy" first (for instance, an if statement for a failing clause and then the actual function without an else indentation)
- __Think about building blocks in your code__
    - Consider inputs, outputs and transformations. Times the number of operations you have in your code. 
    - Your code should be a sequence of blocks that you can then arrange.
    - Each of your block should have a 
    - Optimize each block. And then the overall workflow (unit tests, integration tests)
    - Each of your block should be cohesive: each module, class, or function has a single, well-defined purpose, and the code is organized in a way that makes it easy to understand and maintain.








