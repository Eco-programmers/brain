---
title: Automated unit test with catch2
date created: 2021-11-24
---
# Automated unit test with catch2

## What are unit tests? 

Unit tests are software tests at the  [lowest level](https://en.wikipedia.org/wiki/Software_testing#Testing_levels), small pieces of code that have a specific functionality -- "units". Usually, a function in the code is such a unit. 

Organizing code in small units of a single and specific functionality has several benefits:

- it is easier to read and understand
- it is obvious what part of the data is manipulated
- it is much easier to find bugs
- units can often be re-used in other contexts
- it makes code testable

*When you can write tests for your code, you know your code has a good structure.*

## Structure of a unit test

A unit test runs a piece of code with known data and compares the output to an expected output. The test then either returns true (test passed) or false (test failed).

A test suite runs all unit tests and gives a summary at the end which tests have failed and which have passed.

Unit testing gives confidence to the programmer that the code actually does what it is supposed to do. Equally important, unit tests also give confidence to users and reviewers that not only your code is correct, but also your conclusions you have drawn from the results of your model simulations. The more complex your code becomes, the more critical are tests.

## Debugging and unit test
When you are about to fix a bug in your program, it's a good practise to first write a test, that would have found the bug. Then fix the bug, and you can be sure if the bug is fixed.

## Catch2 
There are many test frameworks for many programming languages, for example, GoogleTest or QTest. I like, however, catch2 the best because it is easy to understand and straightforward to use.

## Catch2 and Qt Creator
A test suite is an independent computer program that has to be compiled and run. One possibility is therefore to start a new project in Qt Creator for the tests. I prefer to have both within the same project and use the sub-projects feature in Qt Creator. 

### To use sub-projects:
1. Create a Subdirs Project
File > New File or Project > Other Project > Subdirs Project > Choose
2. Add a sub-project
After creating the subdirs project, you are automatically asked to add a new sub-project. Either do that or click "cancel". You can always right-click on the project name and add a new sub-project:

![](attachments/Screenshot%20from%202019-12-19%2013-26-39.png)

You can also add an existing project as a sub-project. Just copy the folder with the project files (i.e. .pro, .cpp and .h) where you want them to be located and choose "Add Existing Projects". 

For catch2, add a sub-project:
Non-Qt Project > Plain C++ Application

### Setup catch2
Catch2 consists only of a single file *catch.hpp*. Just [download it](https://github.com/catchorg/Catch2/releases/download/v2.11.0/catch.hpp) and copy the file where the other files of your test sub-project are. Don't worry about the file ending .hpp. This is just another way to name header files. In the end, both are just text files, and you are free to re-name it to *catch.h*. This is how it looks in my file browser:

![](attachments/Screenshot%20from%202019-12-19%2013-45-24.jpg)

Then you need to add the catch.hpp file to your Qt project. In Qt Creator, right-click on the name of the test project > Add Existing Files and choose the catch.hpp file. Then open the main.cpp of your test project and replace all its contents with 

```C++
// WINDOWS:
....
```

```C++
// LINUX ONLY:
#define CATCH_CONFIG_MAIN  // This tells Catch to provide a main() - only do this in one cpp file
#include "catch.hpp"

//Exactly one source file must #define either CATCH_CONFIG_MAIN or CATCH_CONFIG_RUNNER before
//#include-ing Catch.
//In this file do not write any test cases!
//In most cases that means this file will just contain two lines (the #define and the #include).
```

Catch2 generates its own main() function and we do not need to worry about it at all.

### The first unit test

Assume you want to write a series of tests for the CookieBox class. First, you need to add the files with the code you want to be tested to the test project (do not copy the files, just add them). In our case, we need to add cookiebox.h and cookiebox.cpp. Then you need to add a new C++ source file *test-cookiebox.cpp* to the test project and include catch2 and the CookieBox class, for example:
```
// test-cookiebox.cpp

#include "catch.hpp"
#include "../Chapter7/cookiebox.h"
```

The unit tests in catch2 can be organized in *test cases* and *sections* to bundle tests that belong together. For the actual tests, catch2 uses so-called *assertion macros*. They are actually quite intuitive to use:
```
CHECK( cookiebox.getAmountOfCookies() == Approx(1.0) );
```
*CHECK()* is the macro and does what it says: it check whether the expression in the parentheses is true or false. *Approx()* handles the issue with floating-point comparisons by allowing for small deviances.
A list of all available macros in catch2 can be found [here](https://github.com/catchorg/Catch2/blob/master/docs/assertions.md#top).

The complete test-cookiebox.cpp file may the look like so:

```C++
// test-cookiebox.cpp

#include "catch.hpp"
#include "../Chapter7/cookiebox.h"


TEST_CASE( "Test the CookieBox class") {
    // cookie box parameters
    const double carryingCapacity = 1.0;
    const double growthRate = 0.05;
    const double initialAmountOfRessource = 1.0;
    CookieBox cookiebox(growthRate,carryingCapacity, initialAmountOfRessource);

    SECTION("Test if initialization is correct") {
        CHECK(cookiebox.getAmountOfCookies() == Approx(1.0));
    }

    SECTION("Test growth() function") {
        // nothing here, yet
    }
}
```
Now you can run your first unit test. First, select the appropriate sub-project:

![](attachments/Screenshot%20from%202019-12-19%2015-04-32.png)
Then compile & run.



---
References: 
Related: