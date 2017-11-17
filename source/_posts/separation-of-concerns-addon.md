---
title: Faster Test Suites, Less Code, Embracing Writing Addons.
description: Less code, a faster test suite, and a tighter focus on core functionality can be achieved through embracing open source.
date: 2017/11/17
tags:
  - Git
  - Open Source
  - Ember
  - Testing
---

Less code, a faster test suite, and a tighter focus on core functionality can be achieved through embracing open source. [Ember addons](https://www.emberaddons.com/) are on point in delivering such a promise as I've learned while open sourcing a widely used [component at work](https://github.com/q2ebanking/ember-select-light).

The key is a separation of concerns. Modifying code rebuilds the app and, before shipping, all tests must be verified again regardless of what the modifcations touch. Moving chunks of an app, such as a component, to an open source addon grants all the benefits that come with code isolation. Admittedly similar can be achieved with careful abstraction and no open source, but I feel it's the right direction for myself and likely others to aim for.

**Less code** a developer must retain in their heads the easier they may reason about the way an app flows. A well tested and well documented addon promises a level of functionality not often afforded by yet another file to be debugged within the app. While addon code eventually gets compiled into the final output, I've found the act of isolating code into an addon forces me to code more concisely and clearly for public consumption. Without the goal of open sourcing the addon I may cut corners thinking "it's just for me, no big deal" which can do more harm than good longterm.

**Faster test suite** runs, without the cost of coverage, comes isolating tests to separate addon projects. This goes both ways in fact. Tests get removed from the original app and an addon will have just the tests to cover itself resulting in a quick build and test time. Isolated testing concerns can lead to higher relative code coverage and a quicker feedback loop for [test-driven development](https://www.youtube.com/watch?v=2b1vcg_XSR8).

**Tighter focus on core functionality** arises from the need to isolate an addon's concern to a concise idea. Assigning a name and writing documentation for an addon is a healthy exercise in producing a highly intentional and hopefully valuable addon.

After becoming no longer afraid of the world of open source I've learned to embrace the advantages that come from creating a wide range of projects. Addons are a new and exciting world for me and hopefully for you as well.