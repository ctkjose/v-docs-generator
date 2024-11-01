# Refactoring Notes

Preview changes [here](https://www.exponentialworks.com/v/docs/index.html).<br>
This repo is located at [repo](https://github.com/ctkjose/v-docs-generator).<br>


## Code Examples and Playground

- Code implemented a run button that uses the [playground](https://github.com/vlang/playground) server api to execute code examples found in documents.
- This playground functionality is being broken for a while.
- Code pointing to old playground server.
- Cloudflare causes issues using https://play.vlang.io to run snippets, requests will get block fairly fast.
- Code is using a very old version of CodeMirror. This version has multiple issues with mobile browsers, issues with clipboard among others.
- Playground and snippets code is implemented in the file `vlang-playground.js` which includes the source for the version of the CodeMirror used. This file is minified and I was unable to find original versions of the code.
- The new playground at [playground code](https://github.com/vlang/playground) uses the new version 6 of Codemirror. Sadly the TS implementation will add a lot more complexity and dependancies to the generator code base. Currently there is no CodeMirror 6 language packages (mode) for V-Lang (@ctkjose will work on creating one.)
- Removed playground functionality. V-Lang has a full fledge playground at https://play.vlang.io the `docs` should focus on the documentation itself.
- Opted to upgrade to CodeMirror 5 to be able to reuse the current V's language package (mode) from "vlang-playground.js" until a new language package is made using as base the work already done by the folks at the playground's [repo](https://github.com/vlang/playground). Language mode was extracted from minified file.
- Code snippets now present a "Try it..." button that takes users to https://play.vlang.io with the corresponding code.
- Code snippets now have a "copy" button.

## Javascript Refactoring

-- All js code is now in a single file `v-docs.js`.
-- The object `vdocs` is the namespace for all the functionality used. `vdocs.examples` handles all the code snippets. `vdocs.search` has all the search related code. `vdocs.ui` hydrates the UI and handles all UI interactions.

## Removed SASS

- Using sassc which is now deprecated.
- SASS only used for bundling.
- Project already using CSS Variables for themes.

## CSS Refactoring (WIP)

- Moving markdown related css classes to be under the umbrella of the `v-doc` class to make it more reusable.
- Clean up of the theme used for codemirror/snippets.
- Fixing quirks and improving mobile rendering.

## To-Do & Issues
- Use of Github markdown syntax not supported by renderer.
- The module `markdown` is using an old version of md4c. Missing more compatibility with GitHub's markdown.
- Since we promise a pure V implementation of markdown maybe explore writing a replacement to address GitHub compatibility. 

