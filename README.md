# Lost baggage claim letter

A static page (`index.html`) plus one serverless function (`api/polish.js`) that tidies the passenger's wording with an AI model. If the AI call fails, the letter still works from the template.

## Deploy on Vercel
1. Put this folder in a GitHub repo, or run `npx vercel` inside it.
2. In Vercel, import the repo. No build settings needed.
3. Add the environment variables from `.env.example` (at least `LLM_API_KEY`, and set `LLM_MODEL` to a model your provider currently offers).
4. Deploy, then add your own domain under Project Settings > Domains.
5. Test: choose an airline, write a sentence under "What happened", press "Tidy my wording with AI". If it fails, check the function logs in Vercel.

Using cPanel instead? `index.html` works on its own, but the AI step needs a server function, so host `api/polish.js` on Vercel and set `POLISH_ENDPOINT` in `index.html` to its full URL.

## Analytics
Paste one snippet in the marked spot in the `<head>` of `index.html` (Plausible, Umami or Google Analytics). The page then reports these events: `airline_selected`, `letter_type`, `letter_copied`, `pdf_downloaded`, `email_opened`, `share_clicked`.
- In Plausible, create each as a custom event goal. Include props only if your plan supports them.
- Post LinkedIn links as `https://yourdomain.com/?utm_source=linkedin` to see that traffic separately.
- Main number to watch: `pdf_downloaded` divided by visitors.

## Before you post it publicly
- Re-check every email in `AIRLINES` and `AGENCIES` (top of the script) and update `LAST_VERIFIED`.
- Have a lawyer read the letter wording, including the 7-day deadline and the Part 19 reference.
- Add a short privacy notice. The AI step sends the passenger's account text to your provider, and your analytics tool sees page visits.
- Rotate the API key if it is ever shown in a screenshot or repo.
