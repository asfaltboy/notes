---
title: Tech Fuckups - part 0
tags: talk, fuckups, tech
description: View the slide with "Slide Mode".
---

# Tech Fuckups
## Session 1

---

## Explanation

Place to share fuckup (tech?) stories, whether by leaders or beginners, devops or sysops, backend or frontend, etc...

---

## Why

![](https://media1.giphy.com/media/l2Je6ZzIdN68Y9PrO/source.gif)

---

## Really Why

- **Reason 1**: We all fuck up. And that's OK.
- **Reason 2**: When stuff breaks, we shouldn't cover it up. 
- **Reason 3**: _Stories are worth sharing!_

Note: 1. Regardless of how it looks at the moment, we can only grow from the experience. 2. Tell our story, so others will have the courage to speak up. 3. Surviving the battle to make things right _is worth sharing!_

---


### Story 1 - Lock us out of production

----

### Caused by

Ansible role that sets fail2ban to `maxretry: 1`

----

### Caused

Using our beloved xpanes, but with misconfigured user, we banned our office IP on all 16 production instances at once.

----

### Caused

![](https://pbs.twimg.com/media/ClFm_f7VEAAPL6c.jpg)

----

### Wat :question: 

![](https://user-images.githubusercontent.com/3874767/41632080-19336600-7430-11e8-96a4-eeb3c5bb5a86.gif)

----

### Fixed by

Connect to all the machines from another IP (hint: use VPN), with the right user, and unban the IP in fail2ban sshd jail.

----

### Lessons

1. Avoid fail2ban, if possible, just limit SSH whitelist.
2. If using fail2ban, be a bit more forgiving (2/3 attempts)
3. Xpanes is powerful tool; exercise caution when running commands on dozen of servers.

---

## Story 2 - Super slow data migration

----

### Caused by

Writing naive object fetch and update in Django for 10mil records

----

Surprise :exclamation: It's friggin slow af

![](https://media0.giphy.com/media/1xkMJIvxeKiDS/giphy.gif)

----

### Caused

1 hour Web UI downtime during release + 1 more hour to deploy hotfix

Note: Happens while doing planning.

----

### Fixed by

Hotfixed using bulk update query, that we were too lazy to write during PR review.

----

### Lessons

1. Do not dismiss review until all points are addressed
2. Pay closer attention to large data changes in production
3. Make staging a proper (data) copy of production
4. Don't handle release during another meeting

Note: We're still working on implementing some of these.

---

## Story 3 - Infinite regex backtracking

----

### Caused by

Writing an (awful) regex generator from user provided input

----

### What :question:

Similiar to cloudflare outage: https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/

![](https://blog-cloudflare-com-assets.storage.googleapis.com/2019/07/555-steps.gif)

Note: where you tell regex to match X or more characters and the match needs to repeat previously matched characters again and again.

----

### Caused

Weeks (or months?) of workers crashing randomly and odd memory leaking behaviour.

----

### Discovered by

Create and using dashboard for memory metrics.

[Blog post here](https://rebelpenguin.atlassian.net/wiki/spaces/AC/blog/2019/06/17/667189321/The+memory+leak+accident)

----

### Fixed by

- Instead of using things like wildcard matching `\W+` just use space
- Limit the word wildcard
- Normalize the target text to better fit the match we want to run, instead of trying to fit every possible scenario.

Note: simplified the regex

----

### Tl;dr

```
\b(?>\W*\w+)*?(?>\W+)or(?>\W+)currency(?>\W+)equivalent(\b|$)
```

Became

```
(^|\W)(\w+( \w+)*?) or currency equivalent(\W|$)
```

----

### Lessons

1. Monitor everything
2. Actually analyse the logs and metrics - build dashboards!
3. Don't over-generalise solutions

---

# Conclusion

![](https://media.giphy.com/media/xT5LMFNXUV9CnytDt6/giphy.gif)

Note: Hope this talk inspires others to step up and talk about their recent failures, to encourage us all that everyone can make a mistake, and we musn't fear failure, but embrace our mistakes as direct learning exprience.
