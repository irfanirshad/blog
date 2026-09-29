---
title: "Designing an Online Auction System"
date: 2026-09-29T10:00:00+05:30
author: Irfan Irshad
# The picture on the home-page card and at the top of the post. Put the file in
# static/img/auction/ and keep the path starting with /img/. Delete the line for no cover.
cover: /img/auction/cover.jpg
categories:
  - ENG
tags:
  - System Design
  - Distributed Systems
# draft: true keeps it off the live site. Change to false when it's ready, then push.
draft: true
---

One or two sentences that tell the reader what this post is about. This part shows on the home-page card.

<!--more-->

<!--
  HOW TO USE THIS TEMPLATE
  - Anything between these arrow marks is a note to you: it never shows on the site.
  - Replace the example text under each heading with your own. Delete sections you don't need.
  - Images: put them in static/img/auction/ and write ![what it shows](/img/auction/file-name.png)
  - A cheat sheet of everything you can use is at the bottom of this file.
-->

## What we're building

Describe the auction site in plain words. What does a seller do? What does a buyer do?

- Sellers list an item with a starting price and an end time
- Buyers place bids, and each bid must beat the current highest
- When the timer runs out, the highest bidder wins

## Requirements

**Functional** (what it must do):

- ...
- ...

**Non-functional** (how well it must do it):

- ...
- ...

## Rough numbers

How many users, auctions and bids per second? A quick estimate is enough.

## The big picture

![Architecture diagram of the auction system](/img/auction/architecture.png)

*Caption: explain the diagram in one line.*

## Placing a bid

Walk through what happens when someone clicks **Bid**, step by step:

1. ...
2. ...
3. ...

## The hard part: two bids at the same moment

What happens when two people bid in the same second? How do you make sure only one wins?

## Showing live updates

How does every watcher see the new highest bid straight away?

## Ending the auction

What happens at the closing second? What about a bid that arrives just after?

## What I'd do differently

Trade-offs, things you'd change, what you learned.

## Watch the video

I walk through this design on my YouTube channel:

{{< youtube VIDEO_ID >}}

<!-- Replace VIDEO_ID with the code after "v=" in the YouTube address.
     For https://www.youtube.com/watch?v=dQw4w9WgXcQ the ID is dQw4w9WgXcQ.
     Or delete the line above and just link it: [Watch on YouTube](https://www.youtube.com/@your-channel) -->

## Further reading

- [A link title](https://example.com)
- [Another link](https://example.com)

<!--
  ============================================================
  CHEAT SHEET (only you see this)
  ============================================================

  Headings        ## Big heading        ### Smaller heading
  Bold            **bold text**
  Italic          *italic text*
  Both            ***bold and italic***
  Link            [text people click](https://example.com)
  YouTube channel [My YouTube channel](https://www.youtube.com/@your-channel)
  Video in page   {{</* youtube VIDEO_ID */>}}
  Image           ![what the image shows](/img/auction/screenshot.png)
  Bullet list     - item            (start each line with a dash and a space)
  Numbered list   1. item           (1. 2. 3. ...)
  Nested list     indent two spaces:  - item
                                        - sub-item
  Quote           > quoted text
  Inline code     `bid_amount`
  Code block      three backticks, then the language, then the code, then three backticks:
                  ```python
                  def place_bid(auction_id, amount):
                      ...
                  ```
  Line break      leave an empty line between paragraphs
  Divider         ---               (on its own line, with empty lines around it)

  Preview before publishing: ask Claude to run the blog locally with drafts shown.
  Publish: set draft: false at the top, then push to master (Netlify deploys in ~1 minute).
-->
