---
title: "Code Is Cheap Now. Judgment Isn't."
date: 2026-09-20T10:00:00+05:30
author: Irfan Irshad
cover: /img/school-of-athens.jpg
categories:
  - ENG
tags:
  - AI
  - Engineering
  - Essays
---

For most of the history of software, writing the code was the expensive part. That's no longer true, and it changes what an engineer is for.

<!--more-->

<small>*Cover: [The School of Athens](https://commons.wikimedia.org/wiki/File:%22The_School_of_Athens%22_by_Raffaello_Sanzio_da_Urbino.jpg), Raphael, 1509–1511. Public domain.*</small>

Not long ago, going from "I know what this function should do" to "this function exists and compiles" took real effort. You had to recall the API, get the types right, handle the edge cases and write the test. That effort made code feel valuable, so we measured ourselves by it: lines shipped, tickets closed, features delivered.

AI coding tools have pushed the cost of that step close to zero. A model will write a working first draft of a service, a migration or a test suite in the time it takes to describe one. This is real and it's useful, and I use it every day.

What it hasn't done is make *software* cheap. It has shown how little of the cost of software was ever in the typing.

## Where the cost actually was

Think about the last bug that cost your team a week. It probably wasn't a typo. It was more likely one of these:

- Two services disagreed about what a field meant.
- A retry turned one payment into two.
- A job that "always finishes in ten minutes" didn't, and nothing noticed for six hours.
- A schema changed upstream, and a number downstream was quietly wrong for a month.

None of these come from failing to write code. They come from failing to *understand a system*: its failure modes, its hidden assumptions, and how it interacts with everything around it. An AI can write the retry loop in seconds. It can't tell you, unprompted, that the endpoint behind it isn't idempotent, because that fact lives in a meeting from two years ago, in a vendor's small print, or in the head of someone who left.

The expensive part of software has always been **deciding what should happen** and **knowing whether it did**. Code was the medium in between.

## Reading is the new writing

When generating code is cheap, the bottleneck moves to verifying it. The most important skill becomes reading: reading a diff and seeing what it *doesn't* handle, reading a design and seeing where it will break under load, reading a stack trace and seeing the real cause two layers below the symptom.

This has an uncomfortable consequence. Reading well is a skill you build by writing a lot, making mistakes and living with their consequences. An engineer who has only ever reviewed generated code has skipped the part that teaches you what to look for. We will have to be deliberate about how people build that intuition, because the old path to it, years of writing everything by hand, is quietly disappearing.

## Specification is engineering

A model does what you asked, not what you meant. So the gap between those two things, which used to be absorbed by an engineer's judgment *while typing*, now has to be closed *before* anything is generated.

This makes the unglamorous parts of engineering central again:

- **Precise requirements.** What exactly should happen when the input is empty, duplicated, late or malicious?
- **Invariants.** What must *always* be true, however the code is written? ("A client's balance is never negative." "Every event is processed at least once.")
- **Interfaces and contracts.** What does this component promise its callers, and what does it assume about them?

These were always the real design work. Now they're also the prompt. An engineer who can state an invariant clearly will get better results from any tool, and so will their colleagues.

## Taste doesn't compress

Given a problem, a model will usually produce a *reasonable* solution. Reasonable is often wrong, because it's the average of many solutions to many slightly different problems.

Good engineering is full of decisions where the average answer is the wrong one for *this* system:

- not adding the cache, because the data changes faster than it's read;
- polling every thirty seconds instead of adding a message broker, because the box has one CPU and the requirement is "within a minute";
- choosing the boring database the team already knows over the ideal one nobody can operate at 3 a.m.

Each of these is a judgment about context and constraints, and about the people who will maintain the thing. It's what we call *taste*. It comes from having been wrong in specific ways. It's the part of the job I'm most confident isn't going away, because it's the part that depends on being responsible for the outcome.

## Responsibility stays with a person

When a generated function corrupts data in production, the model doesn't get paged. Someone does. That asymmetry settles most arguments about where engineering is heading.

The engineer's job has always been to **own the consequences** of a system. We just used to do that mostly by writing the system ourselves. Now we'll increasingly do it by specifying, reviewing, testing and operating systems that were partly written by something else. That isn't a smaller job. In some ways it's larger, because the volume of code one person answers for is going up.

## What I think this means in practice

A few things I've started doing, and would recommend:

1. **Write the invariants first.** Before generating anything, write down what must be true. Then check the output against them, not against your impression that it "looks right".
2. **Test the failure paths, not the happy path.** Generated code is usually fine when nothing goes wrong. Spend review time on timeouts, retries, partial failures and concurrent writes.
3. **Keep systems small enough to hold in your head.** The cheaper code gets, the easier it is to produce more of it than anyone understands. Fewer moving parts is still the best defense.
4. **Write down *why*.** Code shows what a system does, but only a decision record shows why it does it that way. When code can be regenerated in seconds, the reasoning behind it is the durable asset.
5. **Keep building by hand sometimes.** Not out of nostalgia, but because it's how you keep the intuition that lets you catch the machine's mistakes.

## The optimistic version

There's a gloomy reading of all this, in which engineers become proofreaders for machines. I don't think that's right.

For decades a large share of engineering time went into translating clear ideas into correct syntax. If that share shrinks, more of the job goes to the parts that were always the point: understanding problems, designing systems that fail gracefully, and making good calls under uncertainty.

Code is cheap now. Knowing what to build, and being sure it works, never was. That was always the job.
