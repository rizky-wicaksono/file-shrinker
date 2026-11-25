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
| [`pdf.html`](pdf.html) | **PDF Compressor.** Two methods: *Keep text* shrinks only the pictures inside the PDF, *Pages as pictures* turns each page into one image. Set a target such as "under 18 MB" and it picks the sharpest setting that fits | Heavy slide decks for email, press kits, scanned documents |

## How to use it

1. Open the start page (once it is online, at the GitHub Pages address, or just double-click `index.html` on your computer).
2. Pick the tool for your file type.
3. Drag your file in, or click to choose it.
4. Choose your settings. If you are not sure, keep the defaults; they aim for a good balance of size and quality.
5. Click compress, wait for it to finish, then download the smaller file.

**Tips**

- Use a current version of Chrome, Edge or Safari. The video and audio tools rely on the encoders built into the browser.
- Big or long videos take longer, because your own computer is doing the work. Keep the tab open until it finishes.
- **PDF decks:** use **Keep text** (the default). It resizes and re-saves only the photos and pictures, so text stays searchable, and links and fonts are kept. Use **Pages as pictures** for scans; it shrinks them more, but text can no longer be selected.
- **Email size:** Gmail and Outlook.com allow 25 MB attachments, but email encoding makes a file about a third bigger on the way, and some mail servers allow less. Aim for **18 MB or less** to leave room; that is the default target in the PDF tool. More in the [PDF guide](https://rizky-wicaksono.github.io/guides/how-to-compress-a-pdf-for-email/).

## Privacy: nothing is uploaded

Many "free" online compressors upload your file to their server. For press releases under embargo, client documents or unreleased footage, that is a real risk.

File Shrinker works differently:

- Your file is read and processed **inside your browser tab**. It is never sent to any server, including GitHub's.
- There are no accounts, no tracking and no analytics.
- When you close the tab, everything is gone.

The pages don't load anything from other websites either: the code libraries and fonts are stored in this repository (see [Technical notes](#technical-notes)).

## Why this exists: public relations engineering

Marketing has had "marketing engineers" and growth engineers for years: people who know the craft *and* can build the tools that make it faster. Public relations mostly doesn't have that role yet. I'm trying to build it.

I'm Rizky Wicaksono, a PR consultant based in Jakarta. As a **public relations engineer**, my aim is to:

- **Use AI and just enough code to cut repetitive PR work** such as media monitoring, first drafts, media lists and reporting, so more time goes to strategy and relationships.
- **Turn PR playbooks into small tools that can be reused** by me, my team, and anyone else who finds them useful.
- **Write openly about what works and what doesn't**, including the failures.

File Shrinker is one of those tools. In PR work you constantly need to send big files: event videos to newsrooms, interview audio to editors, press kits through upload forms that cap at a few megabytes. Most online compressors that do this well are paid, add watermarks, or want your file on their server. So I made a free one that runs entirely in the browser.

More tools: **[rizky-wicaksono.github.io/tools](https://rizky-wicaksono.github.io/tools/)**. Write-ups: [rizky-wicaksono.github.io](https://rizky-wicaksono.github.io)

## Put it online with GitHub Pages

The tools are plain HTML files, so GitHub Pages can host them for free with no build step.

1. Make sure the repository is **public** (free GitHub accounts need a public repository for Pages).
2. Open the repository's **Settings**, then **Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
4. Choose branch **main** and folder **/ (root)**, then click **Save**.
5. Wait one or two minutes. The address appears at the top of the Pages screen, usually `https://rizky-wicaksono.github.io/file-shrinker/`.

To try it on your own computer, download the repository and run a small local web server in the folder, for example `python3 -m http.server`, then open `http://localhost:8000`. Opening `index.html` straight from disk also works for the PDF tool; the video and audio tools then fall back to loading their library from a public CDN, because browsers block that kind of file from disk.

## Technical notes

- Plain HTML, CSS and JavaScript. No build step and no server.
- Video and audio: [Mediabunny](https://github.com/Vanilagy/mediabunny) 1.46.0 with the browser's WebCodecs encoders.
- PDF: [PDF.js](https://mozilla.github.io/pdf.js/) 3.11.174 to read and render pages, and [pdf-lib](https://pdf-lib.js.org/) 1.17.1 to write the new file.
- *Keep text* finds every picture in the PDF, decodes it in the browser, scales it down to what the page size needs at the chosen quality (for example 150 dpi for "Balanced"), and saves it as JPEG. Transparency masks stay lossless. A picture is only replaced when the new version is clearly smaller. Text, fonts, vector graphics and links are copied unchanged.
- Look and feel: shared with [rizky-wicaksono.github.io](https://rizky-wicaksono.github.io/). All colours, the font and the header and footer live in `theme.css`, so the style can change in one place. Font: Manrope.
- Everything is stored in the repository: libraries in `lib/`, fonts in `fonts/`, and their licenses in `licenses/`.

```
index.html   video.html   audio.html   pdf.html
theme.css    shared look: colour tokens, header, footer, buttons
lib/         pdf.min.js, pdf.worker.min.js, pdf-lib.min.js, mediabunny.min.mjs
fonts/       fonts.css and five Manrope .woff2 files
licenses/    licenses for the libraries and fonts
og.png       preview image for links shared on WhatsApp, LinkedIn and so on
```

## Roadmap

Done:

- PDF *Keep text* mode that compresses only the pictures, so decks stay searchable.
- Target size for PDFs ("under 18 MB"), picking the sharpest setting that fits.
- Libraries and fonts stored in the repository, with no CDN calls.
- Same look as the portfolio, listed on its [Tools page](https://rizky-wicaksono.github.io/tools/).

Ideas:

- Also shrink CMYK and other less common picture types inside PDFs (they are left as they are for now).
- Shrink pictures inside PowerPoint (`.pptx`) files directly.

Suggestions and bug reports are welcome through GitHub Issues.

---

Made by [Rizky Wicaksono](https://rizky-wicaksono.github.io), public relations engineer in the making.
