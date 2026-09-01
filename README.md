# L&K Homestay — website

A single-page site for L&K Homestay (Ujjain), run by Lav and Kush. No build step, no framework — plain HTML/CSS/JS, plus a folder of real photos from the listing.

## Files

```
index.html      the whole site
images/         property photos (jpg)
```

## Run it locally

From this folder:

```
python3 -m http.server 8000
```

Then open http://localhost:8000 in a browser.

## Publish on GitHub Pages

1. Create a new GitHub repo and push this folder to it:
   ```
   git init
   git add .
   git commit -m "L&K Homestay website"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
2. On GitHub: **Settings → Pages → Source → Deploy from a branch → `main` / `/ (root)`** → Save.
3. GitHub gives you a URL like `https://<your-username>.github.io/<repo-name>/` within a minute or two.

### Using your own domain (optional)

Add a `CNAME` file to this folder containing just your domain (e.g. `lkhomestay.com`), then point your domain's DNS at GitHub Pages (an `A` record to GitHub's IPs, or a `CNAME` record to `<your-username>.github.io` for a subdomain). GitHub's Pages docs have the exact records to use.

## Editing content

Everything is in `index.html` — search for the text you want to change (address, phone number, copy) and edit it directly. The WhatsApp number appears in several `https://wa.me/918770549040...` links and the `tel:+918770549040` links; update all of them together if the number ever changes.

To swap or add a photo, drop a `.jpg`/`.jpeg` into `images/` and update the matching `<img src="images/...">` in `index.html`.
