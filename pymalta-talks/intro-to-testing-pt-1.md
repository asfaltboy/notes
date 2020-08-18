---
title: (pymalta) Introduction to testing pt. 1
tags: talk, testing, tdd, f.i.r.s.t, unit-testing, mocking
description: Introduction to testing
slideOptions: 
    theme: 'white'
    transition: 'fade'
    progress: true
    center: true
    hideAddressBar: true
    display: 'block'

---

## Introduction to Testing (part 1)

slide: http://bit.do/pymalta-tdd

<style>span.qr img {width: 30%}</style>
<span class="qr">![](https://i.imgur.com/k9YxFQK.png)</span>

Note:
 I'm very excited to be talking about this subject with you. Testing, is one of my favorite, if not the favorite, aspect of programming.

[TOC]

---

## Agenda

* Intro to Test Driven Development (TDD)
* TDD Flow
* F.I.R.S.T principles
* Mocking
* Interlude
* Practical

Note:
 Refer to it as TDD from now on
 Get some background on the origins of TDD
 Follow a typical TDD flow
 Review best practices for TDD
 Quickly delve into Mocking in tests
 Take a short detour outside the world of python
 (I'm going to try to go through the slides
  quickly to leave more time for the practical part)

---

## Test Driven Development (TDD)

----

### What is TDD :question:

<span>
<!-- .element: class="fragment" data-fragment-index="1" -->A software development process that relies on the repetition of a very short development cycle:</span>
<span><!-- .element: class="fragment" data-fragment-index="2" -->requirements are turned into very specific test cases</span><span><!-- .element: class="fragment" data-fragment-index="3" -->, then the software is improved to pass the new tests.</span>

Note:
  Who here knows what TDD is?
  Who here practices TDD daily?

----

### Short history

<span>
<!-- .element: class="fragment" data-fragment-index="1" -->Credited to Kent Beck for “rediscovering” TDD in the 2003, a prototype of TDD dates back to the early days of computing in the 1960s.
</span>

<style>img.mainframe {width: 45%; height: 45%}</style>
<span><!-- .element: class="fragment" data-fragment-index="2" --><img src="https://upload.wikimedia.org/wikipedia/commons/d/d2/IBM_526_Printing_Summary_Punch.JPG" alt="" class="mainframe"></span>
<!-- ![](https://i.imgur.com/ygfFErI.jpg) -->

----

### Short history

<span><!-- .element: class="fragment" data-fragment-index="1" -->During the mainframe era, when programmers had limited time with the machine, a documented practice was to write the expected output before entering the punch cards into the computer.</span>

<span><!-- .element: class="fragment" data-fragment-index="2" -->Then you could immediately see whether the results you got from the mainframe were correct by comparing the actual output with the expected documented output.
</span>

----

### Short history

{%youtube KG2M4ttzBnY %}

Note:
  I won't play the whole video here
  But this video is a cool interview about the days of punch cards
  I invite you to watch it later, link is in the slides
  
  Anyway, I can see that this all sounds a bit ... detached

---

<img src="https://media.giphy.com/media/ZgqJGwh2tLj5C/giphy.gif"/>

Note:

  Let's bring it back home

----

## Why write tests :question:

* <div><!-- .element: class="fragment" data-fragment-index="1" -->write tests, so that we can assert that our code runs correctly</div>
* <div><!-- .element: class="fragment" data-fragment-index="2" -->on every change, we re-run our tests to ensure nothing breaks</div>
* <div><!-- .element: class="fragment" data-fragment-index="3" -->particularly after some time passes <span><!-- .element: class="fragment" data-fragment-index="4" -->, making the code easier to maintain</span></div>

Note:

  We're not in punch-card era anymore, so why should write tests?

----

## The TDD Flow

* <div style="color: red;"><!-- .element: class="fragment" data-fragment-index="1" -->write test, and run it to show unimplemented code fails</div>
* <div style="color: green;"><!-- .element: class="fragment" data-fragment-index="2" -->fix the code and re-run test to see it pass</div>
* <div style="color: blue;"><!-- .element: class="fragment" data-fragment-index="3" -->rerun all tests & refactor adjacent code</div>
* <!-- .element: class="fragment" data-fragment-index="4" -->and then repeat above...

Note:
 Let us have a look at how this looks in practice

---

### Test specifications

#### <div><!-- .element: class="fragment" data-fragment-index="1" -->Feature requirements </div>
<div><!-- .element: class="fragment" data-fragment-index="2" -->

- Implement a "simple number class"
- The number should have an "add" method
- The number should have an "multiply" method
- The number should raise an exception if initialized with invalid type
</div>

Note:

  Where to we start? Let's consult the TDD flow again

---

#### TDD Flow - diagram

<style>
.flow-chart svg {
    height: 550px !important;
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
st=>start: Start
e=>end: Feature complete
op=>operation: Write unit test
op2=>operation: Run the test
op3=>operation: Refactor code
cond=>condition: Did test pass?
cond2=>condition: Is the feature complete?

st->op->op2->cond->cond2
op3->op2

cond(yes)->cond2
cond(no)->op3
cond2(yes)->e
cond2(no)->op
```

Note:

  Let's look at an example of a failing test

----

```python
def test_simple_number_add():
    simple_number = SimpleNumber(2)
    assert simple_number.add(2) == 4
```

----

```python
def test_simple_number_add():
    simple_number = SimpleNumber(2)
    assert simple_number.add(2) == 4
```

```python
$ pytest test_simple_number.py
F
=========================== FAILURES ============================
____________________ test_simple_number_add _____________________

    def test_simple_number_add():
>       simple_number = SimpleNumber(2)
E       NameError: global name 'SimpleNumber' is not defined

test_simple_number.py:4: NameError
```

----

```python
class SimpleNumber:
    pass

def test_simple_number_add():
    simple_number = SimpleNumber(2)
    assert simple_number.add(2) == 4
```

----

```python
class SimpleNumber:
    pass

def test_simple_number_add():
    simple_number = SimpleNumber(2)
    assert simple_number.add(2) == 4
```

```python
$ pytest test_simple_number.py
F                                                         [100%]
=========================== FAILURES ============================
____________________ test_simple_number_add _____________________

    def test_simple_number_add():
>       simple_number = SimpleNumber(2)
E       TypeError: this constructor takes no arguments

test_simple_number.py:6: TypeError
1 failed in 0.03 seconds
```

----

```python
class SimpleNumber:
    def __init__(self, number):
        self.x = number

def test_simple_number_add():
    simple_number = SimpleNumber(2)
    assert simple_number.add(2) == 4
```

----

```python
class SimpleNumber:
    def __init__(self, number):
        self.x = number

def test_simple_number_add():
    simple_number = SimpleNumber(2)
    assert simple_number.add(2) == 4
```

```python
$ pytest test_simple_number.py -q
F                                                                                 [100%]
======================================= FAILURES ========================================
________________________________ test_simple_number_add _________________________________

    def test_simple_number_add():
        simple_number = SimpleNumber(2)
>       assert simple_number.add(2) == 4
E       AttributeError: SimpleNumber instance has no attribute 'add'

test_simple_number.py:7: AttributeError
```

----

```python
class SimpleNumber:
    def __init__(self, number):
        self.x = number

    def add(self, y):
        return self.x + y

def test_simple_number_add():
    simple_number = SimpleNumber(2)
    assert simple_number.add(2) == 4
```

----

```python
class SimpleNumber:
    def __init__(self, number):
        self.x = number

    def add(self, y):
        return self.x + y

def test_simple_number_add():
    simple_number = SimpleNumber(2)
    assert simple_number.add(2) == 4
```

```python
$ pytest test_simple_number.py -q
.                                                                                 [100%]
1 passed in 0.05 seconds
```

----

### What's next :question: 

- [ ] add failing test for multiply method
- [ ] implement the multiply method until test passes
- [ ] :repeat: rerun all tests
- [ ] add failing test that expects an exception to be raised if class initalized with a value other than a number
- [ ] implement the type validation in class constructor
- [ ] :repeat: rerun all tests

Note:
  If this all still sounds vague to you, you may complete this class using TDD in the upcoming practical session
  So to recap, let's have a look at another flow-chart

----

### TDD Flow - alt. diagram

![](https://i.imgur.com/Di9r5pM.png)

Note:

  Pause, and get everyone attention, make sure there's no questions

  To help us work with this flow, let's take a look

---

## F.I.R.S.T Principles

* Fast
* Independent
* Repeatable
* Self-Validating
* Timely

Note:
  at some best practices
  originally written in early 2k by Brett Schuchert & Tim Ottinger
  during the object-mentor blog days, and later
  popularised by Uncle bob in "clean code" book (references in the end)
  
  intuitive set of guidelines

----

### Fast

* Tests should run fast
* You should run tests frequently

Note:
  Slow running tests cannot be an excuse to not run or write tests

----

### Independent

* Tests should not depend on each other
* Order should not matter

Note:
  Single test cases should not depend on one another
  And running them in different order shouldn't change the outcome

----

### Repeatable

* Environment should not matter
* Avoid flaky or brittle tests

Note:
  If you run your tests in your local machine and in the cloud, it should not matter
  Beware of writing tests that are susceptable to environmental changes, such as network dependency, etc

----

### Self-Validating

* Tests should either pass or fail
* Manual assertion should be avoided


Note:
  There should be no ambiguity as to the test result
  You should not need to look up logs to assert the result of the test

----

### Timely

* Tests should be written before the code

Note:

  Write your code, test first. Without this, your code may become hard to test, and you'll tend to do it less

  Pause, and get everyone attention, make sure there's no questions

  Has anyone here ever watch "the simpsons"


---

## Mocking

![](https://media.giphy.com/media/3orieLHXgpfkKO9Iju/giphy.gif)

----

### What is mocking :question:

<span><!-- .element: class="fragment" data-fragment-index="1" -->A tool to aid in isolating our tests.</span>

<span><!-- .element: class="fragment" data-fragment-index="2" -->To make them: FAST, INDEPENDENT & REPEATABLE
</span>

----

### How does one mock :question: 

<span>
<!-- .element: class="fragment" data-fragment-index="1" -->Replace (or monkeypatch) code that is outside of the unit under test.
</span>

<style>img.switcharoo {width: 40%; height: 40%}</style>
<span><!-- .element: class="fragment" data-fragment-index="2" --><img src="https://i.imgur.com/ElGiq38.jpg" alt="" class="switcharoo">
</span>

Note:
  Replace calls to code that is "external" to the code we're testing
  Doing the ol' switcharoo

----

### What should be mocked

- callables
- objects
- classes / interfaces
- global var / existing values

Note:
  Anything that is an interface to code outside of our function
  Replacing it with a mock object, allows us to assert that our
  code has interacted correctly with this interface

----

#### Basic example

----

### Test specifications

#### <div><!-- .element: class="fragment" data-fragment-index="1" -->Feature requirements </div>
<div><!-- .element: class="fragment" data-fragment-index="2" -->

- Implement a "simple number class"
- The number should have an "add" method
- The number should have an "multiply" method
- The number should raise an exception if initialized with invalid type
- <span><!-- .element: class="fragment highlight-red" data-fragment-index="3" -->the result should be cached in a DB</span>
</div>

Note:
  Remember our previous feature spec
  Now our product manager, has asked for a new feature
  Let's look deeper at what that means


----

#### The result should be saved to a DB for caching?

* <span><!-- .element: class="fragment" data-fragment-index="1" -->Repeatable</span><span><!-- .element: class="fragment" data-fragment-index="2" --> or flaky?</span>
* <span><!-- .element: class="fragment" data-fragment-index="3" -->Fast</span><span><!-- .element: class="fragment" data-fragment-index="4" -->  or slow?</span>
* <span><!-- .element: class="fragment" data-fragment-index="5" -->Independent</span><span><!-- .element: class="fragment" data-fragment-index="6" -->  or coupled?</span>
* <span><!-- .element: class="fragment" data-fragment-index="7" -->Self-validating</span><span><!-- .element: class="fragment" data-fragment-index="8" -->  or require manual assertion?</span>

Note:
  We could write this just like before, but if we use a real DB, will the results be...
  What if our database is down?
  What if we have internet issues all of the suddent?
  Are we going to have to clear the DB after every run?
  Will we need to query the DB to assert that the result is saved?
  
  There is a better way, let's see how mocking works

----

Mocking in python is easy with `mock.patch`:

<style>.reveal pre { width: 100%; }</style>

```python
from unittest.mock import patch

from simple_number import SimpleNumber


with patch('simple_number.DB') as mock_db:
    SimpleNumber(2).add(2)
    mock_db.assert_called()
```

----

Mock specific attribute with `mock.patch.object`:

<style>.reveal pre { width: 100%; }</style>

```python
from unittest.mock import patch

from simple_number import SimpleNumber, DB

@patch.object(DB, 'connect', return_value='OK')
def test_db_connect(mock_connect):
    simple_number = SimpleNumber()
    assert simple_number.connection_status == 'OK'
    mock_connect.assert_called_once_with(host='host', port='1234')
```

Note:
  cool thing about mock.patch and it's variants, is that it returns
  A magic mock

----

#### Python's MagicMock

<span><!-- .element: class="fragment" data-fragment-index="1" -->A `mock.MagicMock` is a special class that is used by default to replace "patched" objects.</span>

<span><!-- .element: class="fragment" data-fragment-index="2" -->It works by replacing magic methods such as `__str__` and `__call__` and by default returns a new `mock.MagicMock` when called, making call chaining easy!</span>

----

#### Python's MagicMock

- [ ] split into 2 fragments

A `mock.MagicMock` is a special class that is used by default to replace "patched" objects.

It works by patching magic methods such as `__str__` and `__call__` and by default returns a new `mock.MagicMock` when called, making chaining calls easy!

----

Chaining `MagicMock` objects:

<style>.reveal pre { width: 100%; }</style>

```python
from unittest.mock import patch

from simple_number import SimpleNumber

@patch('simple_number.DB')
def test_db_set(mock_db):
    simple_number = SimpleNumber(2)

    db_instance = mock_db.return_value  # the return_value of calling DB()
    db_instance.connect.assert_called_once_with(host='host', port='1234')

    simple_number.add(2)
    db_instance.set.assert_called_once_with(key=2, value=2)
```

---

## Testing is common

Let's take a break and look at some tests written in different languages.

Note:

  remember press B to fade presentation out
  when done: and now that we've tried this out

---

<span><!-- .element: class="fragment highlight-green" data-fragment-index="2" -->Let's try it ourselves!</span>

<!-- .slide: data-background="https://media.giphy.com/media/ZOY9f0GIvbIYM/giphy.gif" -->

----

### Cyber Dojo - go to

 https://cyber-dojo.org/id_join/show?id=NUZNCm
 or
 http://bit.do/pymalta-tdd-dojo
 or
 ![](https://i.imgur.com/ch5Ky2O.png)


Note:

  https://cyber-dojo.org/kata/group/NUZNCm

----

<style>span.dojo-qr img {width: 80%}</style>
<span class="dojo-qr">![](https://i.imgur.com/vDJHfmK.jpg)</span>

----

<span class="dojo-qr">![](https://i.imgur.com/fymxl71.png)</span>

---

## Thank you :tada:

We've reached the end, my friends! Can't wait to see the beautiful tests you will all write.

---

## References

|Refs      |
| -------  |
| ^1^ [wikipedia.org/tdd][1] |
| ^2^ [History of TDD][2] |
| ^3^ [Clean code: chapter 09][3] |
| ^4^ [Agile in a flash: F.I.R.S.T][4] |
| ^5^ [Bowling game TDD pair programming][5] |
| ^6^ [Bowling game TDD in C][6] |

[1]: https://w.wiki/488
[2]: http://derekbarber.ca/blog/2012/03/27/why-test-driven-development/#History_of_TDD
[3]: https://learning.oreilly.com/library/view/clean-code/9780136083238/chapter09.html
[4]: http://agileinaflash.blogspot.com/2009/02/first.html
[5]: https://sites.google.com/site/unclebobconsultingllc/home/articles/the-bowling-game-an-example-of-test-first-pair-programming
[6]: https://www.slideshare.net/amritayan/test-driven-development-in-c

<!-- ---
You can find me on

- GitHub
- Twitter
- or email me
 -->
