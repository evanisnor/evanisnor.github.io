---
title: "I built textytools.dev — fast browser-based text utilities"
date: 2025-11-23
layout: single
tags:
  - tools
  - text
  - productivity
  - nextjs
gallery:
  - url: /assets/images/textytools/json-wizard.png
    image_path: /assets/images/textytools/json-wizard.png
    alt: "JSON Wizard — validate, pretty-print, and search JSON"
  - url: /assets/images/textytools/csv-json-converter.png
    image_path: /assets/images/textytools/csv-json-converter.png
    alt: "CSV / JSON Converter — bidirectional conversion and parsing"
  - url: /assets/images/textytools/diff-viewer.png
    image_path: /assets/images/textytools/diff-viewer.png
    alt: "Diff Viewer — side-by-side comparison with highlights"
---

Hi! 👋🏼 I've been working on a new project that I'm excited to share with you.

My passion is building software that people love! Lately, I've been focusing that energy on a problem I face every day: the friction of switching between dozens of small web tools to handle text and data. Whether I'm coding, writing, or debugging, I often need to format JSON, convert cases, or check diffs. I wanted a single place with friction-free utilities that are fast, private, and consistent.

So, I built [textytools.dev](https://textytools.dev). It's a collection of browser-based utilities designed to be a reliable companion for your daily work.

I believe that the best tools are the ones that empower you without getting in your way. That's why TextyTools is client-first. There's no server processing your data, which keeps things private and incredibly fast. It's built with Next.js and TypeScript, and I've really enjoyed the process of crafting a smooth user experience with Tailwind CSS.

Here are some of the things it can do:

- [Text Counter](https://textytools.dev/text-counter) — count characters, words, lines, paragraphs, and LLM tokens in real time.
- [Diff Viewer](https://textytools.dev/diff-viewer) — side-by-side comparison with highlighting.
- [Case Converter](https://textytools.dev/case-converter) — convert between common case formats (camelCase, snake_case, kebab-case, Title Case, CONSTANT_CASE, and more).
- [Text Sanitizer](https://textytools.dev/text-sanitizer) — chainable sanitization filters (trim, remove duplicates, strip punctuation, etc.).
- [JSON Wizard](https://textytools.dev/json-wizard) — validate, pretty-print, search, and manipulate JSON with real-time feedback.
- [CSV / JSON Converter](https://textytools.dev/csv-json-converter) — convert between CSV and JSON with proper parsing and type detection.
- [Text Encoder](https://textytools.dev/text-encoder) — encode/decode Base64, URL-encoding, hex, and other formats, plus hash utilities.
- [JWT Decoder](https://textytools.dev/jwt-decoder) — decode and inspect JSON Web Tokens, with validation of standard claims.

Some of these tools can even interact! For example:
* _JSON Wizard_ allows you to convert your output to CSV by sending it to _CSV / JSON Converter_
* _CSV / JSON Converter_ will auto-detect your CSV and convert it to JSON, which you can then open with _JSON Wizard_
* Decoded JWTs in _JWT Decoder_ can be opened with _JSON Wizard_ as well

I'd love for you to check it out at [textytools.dev](https://textytools.dev). Let me know what you think!

If you find any bugs, missing features, or want a tool added, please use the **"Suggest a Tool"** link on the site to send feedback or ideas.

Thanks for checking it out — I hope it saves you a few context switches.

{% include gallery caption="Screenshots of TextyTools in action" %}
