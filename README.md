# Newsletter Signals

A single-page dashboard that reads a Substack export in the browser and shows reader-level findings the Substack stats page does not.

**Live tool:** https://yummyamy.github.io/newsletter-signals/

**Post:** https://ameikpe.substack.com/p/how-i-built-an-advanced-substack-dashboard-using-claude-artifacts

**Original artifact:** https://claude.ai/artifact/PpwpzrNoTvEhcDNVW2EKTL

Made for [Data According to Me](https://ameikpe.substack.com/) by Amy.

## What it shows

| Tab | Question it answers |
|---|---|
| Growth | Are emails delivered and recorded openers growing at the same pace? |
| Your list | Who opens regularly, who stopped, who has no recorded open, who gets no email? |
| First email | Open rate by email number, split by whether the first email was opened |
| Cohorts | Share of each sign-up quarter with a recorded open, quarter by quarter |
| Sources | Which sign-up sources bring subscribers who open |
| List review | Subscribers with no recorded open over a chosen number of emails, downloadable as CSV |
| Timing | How quickly opens arrive after sending |
| Open range | Open rate with and without possible Apple Mail privacy opens |
| Every email | Each email against the average of the five before it |

The default view is the author's own newsletter with subscribers anonymised. Load your own export to see yours.

## Input files

1. **Export .zip** (required): Substack Settings → Import / Export → New export. Leave it zipped.
2. **Subscriber .csv** (optional, unlocks the Sources tab): Subscribers → three dots → Export → All columns.

Files read from the .zip: `posts.csv`, `posts/<id>.delivers.csv`, `posts/<id>.opens.csv`.

## Privacy

- Files are parsed in the browser tab. Nothing is uploaded.
- The page makes no fetch, XHR or beacon calls and stores nothing.
- Email addresses appear only in the List review tab, and only for an export the visitor loads themselves.

## How figures are defined

- **Open rate:** people with a recorded open ÷ emails delivered.
- **Status groups:** based on the last 5 emails (regular, now and then, used to open, no recorded open, not getting emails, too new to tell).
- **Possible Apple Mail privacy open:** an open whose user agent is exactly `Mozilla/5.0`. Other privacy proxies can look the same, so the open rate is reported as a range.
- **Source comparison:** only sources with 30 or more subscribers are compared.
- An open is an email open. Reading in the Substack app is not recorded as one.

## Tech

- One self-contained `index.html`: HTML, CSS and vanilla JavaScript, no build step.
- [JSZip](https://stuk.github.io/jszip/) and [PapaParse](https://www.papaparse.com/) are bundled inline.
- Charts are hand-built SVG and HTML bars.
- Fonts load from Google Fonts: Newsreader, IBM Plex Sans, IBM Plex Mono.
- Hosted on GitHub Pages.

## How it was built

Built with Claude as a published Artifact, then exported as a static page. Claude was used to:

- inspect the raw export files and run the analysis in Python before any page was built
- write the page (parsing, metrics, charts, layout)
- test it in a headless browser against the real export
- recount every figure independently from the raw files and compare with the page

The Artifact version and this version share the same code. The only difference is the CSV download, which uses a normal browser download here.

## Run locally

Download `index.html` and `datm-newspaper.mp4` into one folder and open `index.html` in a browser.

## Limits

- Tested on one newsletter's export. Other exports may have columns this page does not expect.
- Needs at least two sent emails.
- Substack can change its export format at any time.

## Contributing

Open an issue for a bug or an export that fails to load. Pull requests are welcome.
