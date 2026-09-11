# FileKiln

The client-side source of [filekiln.com](https://filekiln.com), published so
that the central claim can be checked rather than believed.

## Why this repo exists

FileKiln says your files are never uploaded. Every conversion runs in your
browser, and nothing leaves the machine. That is the kind of claim a site can
make for free, so this repo exists to make it auditable.

Everything here already ships to every visitor. Opening View Source on any tool
page shows the same code. Publishing it changes nothing about what runs; it
just means you do not have to read it through a browser to check.

## How to verify the claim yourself

Two ways, neither of which requires trusting this README.

**Read the code.** Each tool is a single self-contained page. Open the page for
the tool you care about and look for a network call that sends your data
anywhere. There is not one.

**Watch the network.** Open a tool page, open your browser's developer tools,
switch to the Network tab, and run a conversion. Your file never appears in a
request.

**Check the whole tree at once.** No page here contains `fetch(`,
`XMLHttpRequest`, `sendBeacon`, `WebSocket`, `FormData` or a `<form>` element.
Grep for them:

```
grep -rl -E 'fetch\(|XMLHttpRequest|sendBeacon|WebSocket|FormData|<form' . --include='*.html'
```

That returns nothing. The pages have no mechanism to send your data anywhere.

You can also confirm this tree matches what is actually served. Fetch any page
from filekiln.com and compare it with the same path here.

## What the pages do load

Being straight about this, because a privacy claim that hides something is
worth less than no claim at all. Your files stay on your machine, but the pages
are not free of third parties. Every tool page loads:

- Google Fonts (`fonts.googleapis.com`, `fonts.gstatic.com`)
- Google AdSense (`pagead2.googlesyndication.com`)
- Product Hunt and SaaSHub badge images

Those are ordinary third-party embeds and they see that you visited the page.
They do not receive the file you converted, because the page never reads it
into a request.

If you want the tools with none of that, run them yourself. 65 of the 72 pages
are fully self-contained, so you can save one and open it straight from disk.
The remaining 7 load a library from `/assets/vendor/` and need the repo around
them: clone it and serve the folder locally. Those 7 are the home page,
`markdown-to-html`, `json-to-yaml`, `yaml-to-json`, `pdf-to-csv`,
`bank-statement-to-csv` and `bank-statement-to-qbo`.

## What is in here

The built site: 72 HTML pages, the tool code they carry, one stylesheet, and
four vendored libraries under `assets/vendor/`.

## What is not in here

The generator that produces these pages is not included. It is the part that
turns page definitions into the built tree, and it is not needed to read, run
or audit anything the browser receives. Account-specific files that were never
source (search-engine verification tokens and an ads.txt) have also been left
out.

## Licence

FileKiln's own code is licensed under **AGPL-3.0** (see `LICENSE`).

The vendored libraries keep their own licences: PDF.js under Apache-2.0, js-yaml
and marked under MIT. See `NOTICE` for the details.

## Who builds it

[Northline Office](https://northlineoffice.com).
