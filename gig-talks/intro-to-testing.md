---
title: (gig) Introduction to testing
tags: testing, tdd, f.i.r.s.t, unit-testing, mocking, talk
description: Introduction to testing
slideOptions: 
    transition: 'fade'
    progress: true
    center: true
    hideAddressBar: true
    display: 'block'

---

## Introduction to Testing

<!-- Put the link to this slide here so people can follow -->
slide: http://bit.do/gig-tdd

![](https://i.imgur.com/Gy5QmEQ.png)

Note:
 I'm very excited to be talking about this subject with you. Testing, is one of my favorite, if not the favorite, aspect of programming.

---

## Agenda

* Intro to Test Driven Development (TDD)
* F.I.R.S.T principles
* Mocking
* Coverage
* Test types
* Questions

Note:
 This will be a different type of presentation, rather than how I usually present, this would be more hands-on

---

### Test Driven Development (TDD)

----

#### What is TDD^1^ :question:

A software development process that relies on the repetition of a very short development cycle: requirements are turned into very specific test cases, then the software is improved to pass the new tests, only.

----

#### Short history^2^

Credited to Kent Beck for “rediscovering” TDD in the 2003, a prototype of TDD dates back to the early days of computing in the 1960s. During the mainframe era, when programmers had limited time with the machine, a documented practice was to write the expected output before entering the punch cards into the computer. Then you could immediately see whether the results you got from the mainframe were correct by comparing the actual output with the expected documented output.

Note:
 In OOP languages, it would be nearly impossible to add tests after code is shipped, and refactoring is hard. This method would thus enable programmers to write the code in a testable manner to begin with.

----

### TDD Flow

* <div style="color: red;"> write test, and run it to show unimplemented code fails</div>
* <div style="color: green;">fix the code and re-run test to see it succeed</div>
* <div style="color: blue;">refactor to cover the next feature, and repeat above</div>

----

### TDD Flow - diagram

<style>
.flow-chart svg {
    height: 500px !important;
}
</style>
<!-- <style>
.flow-chart {
    background-color: transparent!important;
}
.flow-chart svg text, .flow-chart svg rect, .flow-chart svg path {
    stroke: white!important;
}
</style> -->

```flow
e=>end: Feature complete
op=>operation: Write unit test
op2=>operation: Run the test
op3=>operation: Refactor code
cond=>condition: Did test pass?
cond2=>condition: Is the feature complete?

op->op2->cond->cond2
op3->op2

cond(yes)->cond2
cond(no)->op3
cond2(yes)->e
cond2(no)->op
```

----

### TDD Flow - alt. diagram

![](https://i.imgur.com/Di9r5pM.png)

----

### Let's try it out!

<!-- .slide: data-background="https://media.giphy.com/media/ZOY9f0GIvbIYM/giphy.gif" -->

---

### F.I.R.S.T Principles^3^

* Fast
* Independent
* Repeatable
* Self-Validating
* Timely

----

#### Fast

* Tests should run fast
* You should run tests frequently

----

#### Independent

* Tests should not depend on each other
* Order should not matter

----

#### Repeatable

* Environment should not matter
* Avoid flaky or brittle tests

----

#### Self-Validating

* Tests should either pass or fail
* Manual assertion should be avoided

----

#### Timely

* Tests should be written before the code

---

## Mocking

----

### What is it :question: 

A tool to aid in isolating our tests.

----

### What should be mocked

- callables
- objects
- classes / interfaces
- global var / existing values

----

#### Basic example

Mocking in python with `mock.patch` is easy:

```python
with patch.object(DB, 'connect', return_value='OK') as mock_method:
    db_instance = DB()
    result = db_instance.connect(1, 2, 3)
    assert result == 'OK'

mock_method.assert_called_once_with(1, 2, 3)
```

----

#### Python's MagicMock

A `mock.MagicMock` is a special class that is used by default to replace "patched" objects.

It works by replacing magic methods such as `__str__` and `__call__` and by default returns a new `mock.MagicMock` when called, making call chaining easy!

----

####  Practice mocks

Let's try mocking some objects together? Shall we 🧐 ?

---

## Coverage

A tool to measure how much of our code is covered (executed) by tests.

----

### How to measure coverage :question: 

- html - example.html
- coverage.xml - cubertura format

----

#### What does it mean

- Why should we reach for higher coverage values?
- Adding tests iteratively and measuring progress via coverage

----

### Practice measuring coverage

---

## Testing is common

Let's take a break and look at some tests written in different languages.

---

## Test types

* Unit tests
    * Test the smallest unit of code for correctness
* Integration tests
    * Test multiple units -- test use case
* Functional tests
    * Test large part of the application end-to-end
* Performance tests
    * Benchmark a performance of specific function or component

----

## Practical

---

## CI Pipeline

1. What is it and why should we add a CI pipeline
2. What things to cover in the pipeline

----

#### What is it and why should we add a CI pipeline :question: 

---

### Thank you :tada:

We've reached the end, my friends! Can't wait to see the beautiful tests you will all write.

---

### References

|Refs      |
| -------  |
| ^1^ [wikipedia.org/tdd][1] |
| ^2^ [History of TDD][2] |
| ^3^ [Clean code: chapter 09][3]; [Agile in a flash: F.I.R.S.T][4] |

[1]: https://w.wiki/488
[2]: http://derekbarber.ca/blog/2012/03/27/why-test-driven-development/#History_of_TDD
[3]: https://learning.oreilly.com/library/view/clean-code/9780136083238/chapter09.html
[4]: http://agileinaflash.blogspot.com/2009/02/first.html

<!-- ---
You can find me on

- GitHub
- Twitter
- or email me
 -->
 
 