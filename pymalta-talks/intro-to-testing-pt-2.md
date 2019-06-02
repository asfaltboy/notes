---
title: (pymalta) Introduction to testing pt. 2
tags: testing, coverage, test-types, pytest, CI, talk
description: Introduction to testing
slideOptions: 
    theme: 'white'
    transition: 'fade'
    progress: true
    center: true
    hideAddressBar: true
    display: 'block'

---

## Introduction to Testing (part 2)

- [ ] add slides link and QR code

slide: http://bit.do/pymalta-tdd-2

<style>span.qr img {width: 30%}</style>
<!-- <span class="qr">![](https://i.imgur.com/k9YxFQK.png)</span> -->

Note:
 I'm very excited to be talking about this subject with you. Testing, is one of my favorite, if not the favorite, aspect of programming.

[TOC]

---

## Agenda

* Test types
* Coverage
* Alternative runners: pytest
* Continuous Integration
* Practical

---

## Test types

* Unit tests
    * Test the smallest unit of code for correctness
* Integration tests
    * Test multiple units at once -- use cases and scenarios
* Functional tests
    * Test large part of the application end-to-end, application flow
* Performance tests
    * Benchmark the performance of a specific function or component

---

---

## Coverage

A tool to measure how much of our code is covered (executed) by tests.

----

### How to measure coverage :question: 

- html - example.html
- coverage.xml - cubertura format

----

### Practice measuring coverage

Check out my bowling calculator code from last time, is it fully covered?

Why not? What is left to be covered? Are these valid scenarios, or edge cases?

----

#### What does it mean

- Why should we reach for higher coverage values?
- Adding tests iteratively and measuring progress via coverage

---

## Alternative runners: Pytest

---

## Continuous Integration

What is continuous integration (CI)?



---

## CI Pipeline

1. What is it and why should we add a CI pipeline
2. What things to cover in the pipeline

----

#### What is it and why should we add a CI pipeline :question: 
