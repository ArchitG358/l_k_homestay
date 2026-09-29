# L&K Homestay — website

The website for L&K Homestay, Ujjain — five furnished 2BHK and 3BHK flats near the Mahakaleshwar Jyotirlinga, run by brothers Lav and Kush.

**Live at [lkhomestay.co.in](https://lkhomestay.co.in)**

Plain HTML and CSS. No framework, no build step — edit a file, push, it's live.

## Files

```
index.html                  home page
bhasma-aarti.html           guide: Bhasma Aarti timings and booking
how-to-reach-ujjain.html    guide: airport, trains, road
faq.html                    guest questions
styles.css                  all styling, shared by every page
images/                     property photos, temple photos, logo
sitemap.xml  robots.txt     for search engines
CNAME                       custom domain — see the warning below
```

## Run it locally

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

Use a server rather than double-clicking the HTML — opening files directly
(`file:///…`) breaks some links and the Google Maps embed.

## How it deploys

Pushing to `main` triggers two GitHub Actions workflows:

| Workflow | What it does |
|---|---|
| `static.yml` | Deploys to GitHub Pages → **lkhomestay.co.in** (this is the live site) |
| `deploy.yml` | FTPs a copy to InfinityFree — a leftover from before the domain existed |

`deploy.yml` is redundant now and can be deleted along with its FTP secrets,
unless you want InfinityFree kept as a backup.

### ⚠️ Everything in this folder gets published

`static.yml` deploys the **entire repository**. Any file here becomes publicly
readable at `lkhomestay.co.in/<path>` — even if no page links to it.

Before adding anything, ask whether it should be public. Already excluded in
`.gitignore` for this reason:

- `reviews/` — screenshots with guests' names and faces
- `analysis - temp/` — working notes containing ad spend and campaign data
- `images/amneties.jpeg` — the flyer, which has personal phone numbers on it
- the large PNG originals (optimised `.jpg` versions ship instead)

## Editing content

Everything lives in the HTML. Search for the text you want to change.

**Phone numbers** appear in many places — the primary number as both
`wa.me/917389111152` and `tel:+917389111152`, plus the alternate
`87705 49040`. If a number ever changes, update every occurrence:

```bash
grep -rn "917389111152" *.html
```

**Photos:** drop a `.jpg` into `images/` and point an `<img src="images/…">`
at it. Keep them under ~400KB; resize with
`sips -Z 1400 -s formatOptions 78 in.jpg --out out.jpg`.

## Analytics and ads

The Google tag is in the `<head>` of every page, running Google Analytics 4
(`G-34TM0DP939`) and Google Ads (`AW-18284589937`) from one loader.

A click listener at the bottom of each page fires GA4 events when someone taps
Call or WhatsApp:

- `contact_call`
- `contact_whatsapp`

Mark these as key events in GA4, then import them into Google Ads as conversion
actions — otherwise Ads has no signal for what a good click looks like.

## Custom domain

DNS is at GoDaddy. The apex points to GitHub's four Pages IPs and `www` is a
`CNAME` to `architg358.github.io`.

**Don't delete `CNAME`.** Because Pages deploys via a workflow, an artifact
without that file can reset the custom domain back to the github.io default.
