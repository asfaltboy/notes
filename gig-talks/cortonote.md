---
title: "CortoNote: Building a better note takling app with Draft JS"
tags: talk, draft.js, cortonote, typescript
description: View the slide with "Slide Mode"
---

# CortoNote

## Building a better note takling app with Draft.JS

slides: https://hackmd.io/@pavel-savchenko/HJ7znk7TH

---

# Agenda

1. Why another note taking app
2. Why use Draft.JS
3. Introducing CortoNote
4. Open source

Note: 1. business, 2. technical, 3. show off

---

## Why another note taking app?

:notebook: 

----

### Current state of note taking apps

An intersection of the following shortcomings:

- Bloated
- Slow
- Paid
- No mobile client
- Ugly

note: what we dislike about them (personal opinion)

----

### Current state of note taking apps

![](https://i.imgur.com/rsrDScY.png)

----

### Current state of note taking apps

![](https://i.imgur.com/S6eJIzA.png)

----

### Current state of note taking apps

![](https://i.imgur.com/pYnuyIi.png)

----

### Current state of note taking apps

![](https://i.imgur.com/3vXoI5q.png)

----

### Recap: list of wanted features

- Small and fast
- Synced to remote
- Mobile client
- Support markdown style (w/ inline)
- Freeware / opensource

note: decided to build it ourselves!

---

## Why use Draft.JS

note: technical part

----

### Other "rich text editors"

![](https://i.imgur.com/NVQ7zkD.png)

----

### Problems w/ other "Rich text editors"

- (way too) Fully featured
- Slow / resource intensive
- Dependency heavy
- React wrappers feel "slapped on"

Note: Too many batteries

----

### Introducing Draft.JS

----

### Draft.JS - History

Open sourced by Facebook in 2016, used today in many of their products
(posts, comments, messenger, etc)

note: this new editor is based on ContentEditable

----

### Draft.JS - Content Editable

<style>.sm {font-size: 14px}</style>

![](https://i.imgur.com/mr7aiME.png)
<span class="sm">snagged from the draft.js intro presentation</span>

----

### Draft.JS - Content Editable

Facebook aimed to build:

> a controlled content editable

Override the default behaviour of ContentEditable to render DOM w/ React; while still using CE's powerful "native selection API".

note: unlike other methods, does not need to manually render absolutely everything from scratch, nor does it need to use an underlying text area, or calculate input dimensions, cursor and selection and position.

----

### Problems with Draft.JS

- Tough to get started with (complex flow, immutable.js)
- Documentation is lacking
- Only 2 "maintainers" (previously 1)
- Facebook product focus
- Despite hype (17k stars) not widespread

Note: not popular, meaning compared to other editors

----

### Problems with Draft.JS


![](https://i.imgur.com/TsyG3QU.png)

note: despite this, once you get over the initial learning curve, the idea is quite elegant and fun to work with.

----

### Tips for using Draft.JS

- Use RichUtils and Modifier to DRY out code
- Get comfortable with Immutable
- 

note: in summary once you get over the initial learning curve, the idea is quite elegant and fun to work with.

---

## Introducing CortoNote

----

### an example of a "plugin" for rich text

----

### a gnarlier example

----

### attention to detail

- right arrow escape
- simpler "markdown-style" inline styles
- language-aware code blocks (using prism)
- undo/redo, copy/paste
- really simple structure using tags

---

## Open source

----

### What we intend to open source

- Editor
- ...

----

### When do we intend to open source

- As soon as core version is stable

---

## Addendum

For more information, see:

- https://draftjs.org/docs/getting-started
- draft.js intro talk: https://www.youtube.com/watch?v=feUYwoLhE_4
- other resources available online; plugins, blog posts, video tutorials, even a course on Udemy
- https://github.com/immutable-js/immutable-js

---

### Thank you! :bow:

- Questions? Reach out to me after the talk
