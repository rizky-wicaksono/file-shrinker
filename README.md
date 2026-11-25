# File Shrinker

**Make videos, audio recordings and PDFs smaller, right in your browser. Free, no sign-up, and your files never leave your computer.**

File Shrinker is a set of three small web tools: one for video (MP4), one for audio (M4A) and one for PDF. You open a page, drop in a file, pick how small you want it, and download the result. All the work happens on your own device.

Built by [Rizky Wicaksono](https://rizky-wicaksono.github.io) as part of a public experiment in *public relations engineering* (more on that [below](#why-this-exists-public-relations-engineering)).

---

## The tools

| Page | What it does | Good for |
|---|---|---|
| [`index.html`](index.html) | Start page that links to the three tools | |
| [`video.html`](video.html) | **MP4 Compressor.** Choose a resolution and quality, or type a target size such as 25 MB | Event footage, spokesperson clips, videos that are too big for email or WhatsApp |
| [`audio.html`](audio.html) | **M4A Compressor.** Set bitrate, switch to mono, lower the sample rate. Saves a real `.m4a` file | Interview recordings, podcasts, voice notes |
| [`pdf.html`](pdf.html) | **PDF Compressor.** Shrinks scans and slide decks | Press kits, scanned documents, decks that bounce off upload limits |

## How to use it

1. Open the start page (once it is online, at the GitHub Pages address, or just double-click `index.html` on your computer).
2. Pick the tool for your file type.
3. Drag your file in, or click to choose it.
4. Choose your settings. If you are not sure, keep the defaults; they aim for a good balance of size and quality.
5. Click compress, wait for it to finish, then download the smaller file.

**Tips**

- Use a current version of Chrome, Edge or Safari. The video and audio tools rely on the encoders built into the browser.
- Big or long videos take longer, because your own computer is doing the work. Keep the tab open until it finishes.
- **PDF note:** the PDF tool turns each page into an image. That makes scans and image-heavy decks much smaller, but the text is no longer searchable or selectable. Keep the original if you need to copy text from it.

## Privacy: nothing is uploaded

Many "free" online compressors upload your file to their server. For press releases under embargo, client documents or unreleased footage, that is a real risk.

File Shrinker works differently:

- Your file is read and processed **inside your browser tab**. It is never sent to any server, including GitHub's.
- There are no accounts, no tracking and no analytics.
- When you close the tab, everything is gone.

The only things fetched from the internet are the tool's own code libraries and fonts (see [Technical notes](#technical-notes)), and only when a page first opens. Your files are not part of those requests.

## Why this exists: public relations engineering

Marketing has had "marketing engineers" and growth engineers for years: people who know the craft *and* can build the tools that make it faster. Public relations mostly doesn't have that role yet. I'm trying to build it.

I'm Rizky Wicaksono, a PR consultant based in Jakarta. As a **public relations engineer**, my aim is to:

- **Use AI and just enough code to cut repetitive PR work** such as media monitoring, first drafts, media lists and reporting, so more time goes to strategy and relationships.
- **Turn PR playbooks into small tools that can be reused** by me, my team, and anyone else who finds them useful.
- **Write openly about what works and what doesn't**, including the failures.

File Shrinker is one of those tools. In PR work you constantly need to send big files: event videos to newsrooms, interview audio to editors, press kits through upload forms that cap at a few megabytes. Most online compressors that do this well are paid, add watermarks, or want your file on their server. So I made a free one that runs entirely in the browser.

More tools and write-ups: **[rizky-wicaksono.github.io](https://rizky-wicaksono.github.io)**

## Put it online with GitHub Pages

The tools are plain HTML files, so GitHub Pages can host them for free with no build step.

1. Make sure the repository is **public** (free GitHub accounts need a public repository for Pages).
2. Open the repository's **Settings**, then **Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Choose branch **main** and folder **/ (root)**, then click **Save**.
5. Wait one or two minutes. The address appears at the top of the Pages screen, usually `https://rizky-wicaksono.github.io/file-shrinker/`.

To run it without the internet hosting, download the files and open `index.html` in your browser.

## Technical notes

- Plain HTML, CSS and JavaScript. No build step and no server.
- Video and audio: [Mediabunny](https://github.com/Vanilagy/mediabunny) 1.46.0 with the browser's WebCodecs encoders, loaded from jsDelivr (unpkg as a fallback).
- PDF: [PDF.js](https://mozilla.github.io/pdf.js/) 3.11.174 to render pages and [pdf-lib](https://pdf-lib.js.org/) 1.17.1 to build the new file, loaded from cdnjs.
- Fonts: Inter and Space Grotesk from Google Fonts.
- Because the libraries come from public CDNs, you need an internet connection the first time a page opens.

## Roadmap

Ideas under discussion, not yet built:

- A PDF mode that keeps text searchable (compressing only the images inside the PDF).
- Bundling the libraries inside the repository so the tools work fully offline and don't depend on CDNs.

Suggestions and bug reports are welcome through GitHub Issues.

---

Made by [Rizky Wicaksono](https://rizky-wicaksono.github.io), public relations engineer in the making.
