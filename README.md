# nasty queer — tip page

A performer tip page for Nasty Queer events. Tap a performer → see their Venmo, Cash App, and Instagram. Roster pulls live from a Google Sheet — no code changes needed to update the lineup.

---

## deploy to vercel

1. Install Vercel CLI: `npm i -g vercel`
2. In this folder, run: `vercel`
3. Follow the prompts. Done.

To assign a custom domain (e.g. `tip.queerolina.org`):
- Go to your Vercel project → Settings → Domains
- Add `tip.queerolina.org`
- In your DNS (wherever queerolina.org is managed), add a CNAME record:
  - Name: `tip`
  - Value: `cname.vercel-dns.com`

---

## google sheet setup

1. Create a new Google Sheet with these exact column headers in row 1:

   | Name | Role | Venmo | CashApp | Instagram | PhotoURL | EventName |

2. Fill in performer rows. Example:
   | Garnet Starlet | Drag | @garnet-starlet | $garnetstarlet | @garnetstarlet | https://... | Turn the Page — June 20 |

   - **PhotoURL** — paste a direct image URL (Google Drive public link, Imgur, etc). Leave blank to use initials avatar.
   - **EventName** — only needs to be filled in one row. It becomes the badge on the page.
   - **Venmo / CashApp / Instagram** — any of these can be blank. That row just won't show in the modal.

3. Publish the sheet:
   - File → Share → Publish to the web
   - Select: Sheet1 → Comma-separated values (.csv)
   - Click Publish. Copy the URL.

4. In `index.html`, find this line near the bottom:
   ```
   const SHEET_URL = 'YOUR_SHEET_CSV_URL';
   ```
   Replace `YOUR_SHEET_CSV_URL` with the URL you copied.

5. Remove the word `dev` from the `<body class="dev">` tag to hide the setup instructions box.

6. Redeploy: `vercel --prod`

---

## updating the lineup

Just update the Google Sheet. The page re-fetches on every load — no redeployment needed.

For a new event, update the `EventName` column and swap out performers. The page reflects it instantly.

---

## photo tips

- Google Drive: right-click file → Share → Anyone with link → copy link. Replace `/view` with `/uc?export=view` in the URL.
- Imgur: upload photo, right-click → open image in new tab → use that direct URL.
- If a photo URL breaks, the page automatically falls back to the initials avatar. Nothing looks broken.
