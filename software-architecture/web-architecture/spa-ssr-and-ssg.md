# SPA, SSR and SSG rendering

## Summary

A single page application (SPA) renders pages in the browser with JavaScript, server-side rendering (SSR) renders each page on the server at request time, and static site generation (SSG) renders pages once at build time. The choice trades time to first content, server cost and freshness of data.

## Prerequisites

- [Hypertext Transfer Protocol (HTTP)](../../computing-foundations/computer-networks-and-communications/http.md)

## Core concepts

TODO: add a diagram of the central mechanism (see GUIDELINE section 6.2).

- **SPA**: A single page application loads only a single web document from the server and then updates the content of that document on demand via `Javascript APIs` without reloading the entire document. React, Vue, Angular are the top frameworks used to create single page applications.
- **SSR**: This technique uses a server like `Node.js` to fully render the web document upon the receival of a request and then send it back to the client. This way the user get an interactive document with all the necessary information without having to wait for any JavaScript or CSS files to load.
- **SSG**: Static site generation renders the web document in the server(like SSR), however the page is rendered at **build time**. So, instead of rendering the page on the server upon the receival of a request, the page is already rendered in the server, waiting to be served to the client.

## Worked example

TODO: add a concrete, reproducible example with real values.

## Trade offs and when to use it

TODO: describe benefits, costs, alternatives and when this is the wrong choice.

## Common mistakes

TODO: list frequent misunderstandings and failure modes, with the fix for each.

## Practice

TODO: add three to five questions, with answers at the bottom.

## Further reading

- Miller, J., Osmani, A. (2019). [*Rendering on the Web*](https://web.dev/articles/rendering-on-the-web). web.dev. Compares server rendering, static rendering, client-side rendering and hydration with their performance effects.

TODO: check the content of this note against the sources above and record what was verified and when.
