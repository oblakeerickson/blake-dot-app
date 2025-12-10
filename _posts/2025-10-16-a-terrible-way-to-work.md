---
layout: post
title: "A Terrible Way To Work"
date: 2025-10-16 01:00:00 -0600
---

I've been working on [a GitHub action today][2] to automatically validate the [openapi.json schema][1] we generate from Discourse. Every time I work on a GitHub action I'm impressed and my mind starts turning about ways that I can use them even more. They are incredibly convenient for automating tasks and I kind of want to use them for everything.

Equal to the level of inspiration though, I also get incredibly frustrated because I'm working on code that can really only run in "production". I often have no idea if something will work until I merge my PR and manually test it. It's a terrible way to work.

[1]: https://github.com/discourse/discourse_api_docs/blob/main/openapi.json
[2]: https://github.com/discourse/discourse_api_docs/pulls?q=is%3Apr+is%3Aclosed+created%3A2025-10-16

