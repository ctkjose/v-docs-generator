# Refactoring Notes

Preview changes [here](https://www.exponentialworks.com/v/docs/index.html).<br>
This repo is located at [here](https://github.com/ctkjose/v-docs-generator).<br>


## Code Examples and Playground

**Old behavior:**

The code implemented a run button that uses the [playground](https://github.com/vlang/playground) server api to execute code examples found in documents. This playground functionality was broken for a while. 

**Issues found:**
- Code pointing to old playground server.
- Cloudflare causes issues when attempted to use new server https://play.vlang.io to run snippets, requests will get block fairly fast.
- Code is using a very old version of CodeMirror. This version has multiple issues with mobile browsers, issues with clipboard among others.
- Playground and snippets code is implemented in the file `vlang-playground.js` which includes the source for the version of the CodeMirror used. This file is minified and I was unable to find original versions of the code.

**Refactoring reasoning:**

- Upgrade code to use CodeMirror 6 for syntax highlighting using vanilla js. The language mode for V was ported from the playground's [repo](https://github.com/vlang/playground).
- Removed the playground functionality. V-Lang has a full fledge playground at https://play.vlang.io the `docs` should focus on the documentation itself.
- Instead of a "run" button code snippets now present a "Try it..." button that takes users to https://play.vlang.io with the corresponding code.
- Code snippets now have a "copy" button.

## Search

- Fixed js code.
- CSS style got some minor tweaks.

## Javascript Refactoring

- All js code is now in a single file `v-docs.js`.
- The object `vdocs` is the namespace for all the functionality used. `vdocs.examples` handles all the code snippets. `vdocs.search` has all the search related code. `vdocs.ui` hydrates the UI and handles all UI interactions.
- A little code cleanup and refactoring.

## Main.v
- The index from section names and files is stored in the same `v-doc.js` file instead of a separate file. Items are stored under the `vdocs` namespace instead of global variables.


## Removed SASS

- Using sassc which is now deprecated.
- SASS only used for bundling.
- Project already using CSS Variables for themes.

## CSS Refactoring (WIP)

- Moving markdown related css classes to be under the umbrella of the `v-doc` class to make it more reusable.
- Clean up of the theme used for codemirror/snippets.
- Fixing quirks and improving mobile rendering.

## To-Do & Issues
- docs.md uses Github markdown syntax currently not supported by the markdown module.
- The module `markdown` is using an old version of md4c. Missing more compatibility with GitHub's markdown.
- Since we promise a pure V implementation of markdown maybe explore writing a replacement to address GitHub compatibility. 

