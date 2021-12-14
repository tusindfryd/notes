---
title: Site manual
---

This site is based on the [Digital Garden](https://github.com/maximevaillancourt/digital-garden-jekyll-template/) template by Maxime Vaillancourt. 

#### Link syntax
- external links: `[link title](url)`
- internal links:
  - [[note title]]
  - [[note filename]]
  - [[note title | link title]]
  - [[note filename | link title]]
  - normal HTML syntax

#### Footnotes

Footnotes are treated like internal links.[^1]

[^1]: here, a footnote


#### Code syntax highlighting

You can add code blocks with full syntax color highlighting by wrapping code snippet in triple backticks and specifying the type of the code (`js`, `rb`, `sh`, etc.):

```js
// a bit of JavaScript:
console.log("hello!");
```

```sh
$ cat /dev/urandom | grep "the answer to life" # shell scripts look nice too
```
