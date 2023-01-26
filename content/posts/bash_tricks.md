---
title: 5 Bash Scripts & Resources to flavorize your Journey to the Centre of the Shell
date: 2021-01-12T23:54:31+08:00
author: 1rfan
avatar: /img/ss.jpeg
cover: /img/bash2.jpeg
images:
  - /img/build-a-chrome-extension-with-figwheel-main.png
categories:
  - ENG
tags:
  - bash
  - github
---

You like computers? You like software? You're probably already secretly married to Bash then..

<!--more-->

## What's bash? Where do I even start?

Bash is a shell program.

A shell program is typically an executable binary that takes commands that you type and  translates those commands into system calls to the Operating System API.

<a href="https://wiki.bash-hackers.org/scripting/basics" target="_blank">Click here</a> for a quick read-up on its basics incase you're not already familiar with bash.

> Note that bash is not the only kind of shell. There are other shells out there as well.
This diagram helps give a picture of the history of bash:

<br/>

![Scenario 1: Across columns](/img/bash_table.png)


Just dropping <a href="https://mywiki.wooledge.org/BashFAQ" target="_blank">this FAQ link</a> here for those questions I can't answer because I have disabled comments functionality on this site lol. However the wiki/FAQ should more than makeup for my failings.

Back to the topic, in this post, we are going to use [Figwheel Main](https://figwheel.org/), a brand new upgraded version of lein-figwheel, to build a chrome extension.
I have used it in [GitHub Colorful Contributions](https://github.com/g1eny0ung/github-colorful-contributions-graph) to replace lein-figwheel.
There will be some differences from regular web development that require our special attention. But don't worry, I will point out them later.

Let's start.


Back to the topic, in this post, we are going to see a couple of interesting github repositories and scripts, all of them which will ultimately help you, in sharpening your bash skills.

There will be some resources that might seem a lot to digest at first and may require our special attention. But don't worry, I will point out them later.

Let's start.

## Progress bar
![Scenario 1: Across columns](/img/bashgif.gif)

Repository: <a href="https://github.com/edouard-lopez/progress-bar.sh" target="_blank">Link</a>

Reading other people's bash scripts seems like opening a can of worms at first. I mean, it never ends well to be honest. But as you start to progress, you really pick up speed.

That is why I have placed this fun script top of our list. This will not only teach you how to read up silly bash code but also leave you with some code that you'll almost always use when you're writing up a script in bash that involves waiting or loading up stuff of some kind. Chuck this piece of code in there to make it look a little bit more professional.


## Bocker

[Github Repo](https://github.com/p8952/bocker)
Bocker is docker rewritten in 100 lines of bash. I've honestly never used it myself as of yet, but it certainly looks inviting if you happen to dabble with containers and packaging up your code.



## Extension manifest

To develop a chrome extension, we need to create a `manifest.json` in the `resources/public` dir:

```bash
touch resources/public/manifest.json
```

You can view [Manifest file format](https://developer.chrome.com/docs/extensions/mv2/manifest/#manifest_version) for more details. This time we will fill the content below:

```json
{
  "name": "Hello World",
  "version": "0.1.0",
  "manifest_version": 2,
  "browser_action": {
    "default_popup": "index.html"
  }
}
```

Then we can go to the next step.

## fff (Fucking Fast File-Manager)

<a href="https://github.com/dylanaraps/fff" target="_blank">Github Repo</a>

Dependencies for image display

- w3m-img
- xdotool for X.
- fbset for the framebuffer.



Now we can put it into extensions, open `chrome://extensions` and click **Load unpacked** to select `resources/public` folder:

![Load unpacked](/img/build-a-chrome-extension-with-figwheel-main/load-unpacked.png)

Everything looks normal, but when you click the extension icon in the extensions bar, some errors will occur:

![Errors](/img/build-a-chrome-extension-with-figwheel-main/errors.png)

This is the first point we need to pay attention to: [Chrome Apps Content Security Policy](https://developer.chrome.com/docs/apps/contentSecurityPolicy/).

Since we are in a development environment, Figwheel Main will insert some inline scripts (relate to its own functionality) into the document. You can view the `dev-main.js`:

```js
if (typeof goog == 'undefined') document.write('<script src="/cljs-out/dev/goog/base.js"></script>')
document.write('<script src="/cljs-out/dev/goog/deps.js"></script>')
document.write('<script src="/cljs-out/dev/cljs_deps.js"></script>')
document.write(
  '<script>if (typeof goog == "undefined") console.warn("ClojureScript could not load :main, did you forget to specify :asset-path?");</script>'
)
document.write('<script>goog.require("figwheel.core");</script>')
document.write('<script>goog.require("figwheel.main");</script>')
document.write('<script>goog.require("figwheel.repl.preload");</script>')
document.write('<script>goog.require("devtools.preload");</script>')
document.write('<script>goog.require("figwheel.main.system_exit");</script>')
document.write('<script>goog.require("figwheel.main.css_reload");</script>')
document.write('<script>goog.require("process.env");</script>')
document.write('<script>goog.require("hello_world.core");</script>')
```

This violates this rule:

> You can't use inline scripting in your Chrome App pages. The restriction bans both \<script\> blocks and event handlers (\<button onclick="..."\>).

Refer to the errors above, to solve this problem, we need to set `content_security_policy` field in the `manifest.json`:

```json
{
  "content_security_policy": "script-src 'self' 'unsafe-eval' 'sha256-xxx' 'sha256-xxx' 'sha256-xxx'; object-src 'self'"
}
```

The errors contain all `sha256-xxx` which need to be filled in the policy field. This is a little bit cumbersome. You may think why we can't use the `unsafe-inline`?
Because chrome ignores this keyword especially, even the errors tell you can 😢.

After finishing this, edit the code and you will see that your code has completed the hot reload 😎.



## Pure Bash Bible  && <a href="https://github.com/dylanaraps/pure-sh-bible" target="_blank">Pure sh Bible</a>

The goal of this book is to document commonly-known and lesser-known methods of doing various tasks using only built-in bash features. Using the snippets from this bible can help remove unneeded dependencies from scripts and in most cases make them faster. I came across these tips and discovered a few while developing neofetch, pxltrm and other smaller projects.
References:

- [ClojureScript](https://clojurescript.org/)
- [Figwheel Main](https://figwheel.org/)
- [figwheel.main template](https://rigsomelight.com/figwheel-main-template/)
- [Chrome Apps Content Security Policy](https://developer.chrome.com/docs/apps/contentSecurityPolicy/)