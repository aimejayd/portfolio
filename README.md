# JayD Portfolio — go-live guide

Files:

| File | What it is |
|---|---|
| `index.html` | The website (photo and styles built in) |
| `og-image.png` | Link preview picture for email, LinkedIn, WhatsApp |
| `netlify/functions/chat.mjs` | The real AI assistant (server side, keeps your API key secret) |
| `netlify.toml` | Netlify settings |
| `DESIGN.md` | Design rules for future changes |

Opened directly from your computer, the chat uses its built-in answers. Once deployed with an API key, it switches to the real AI automatically (the badge in the chat changes to **live AI**).

---

## 1. Put it online (Netlify, free)

1. Push this folder to a new GitHub repo, for example `aimejayd/portfolio`.
2. Go to app.netlify.com → **Add new site → Import an existing project** → pick the repo → **Deploy**.
   (No build command needed. Settings come from `netlify.toml`.)
3. Optional: **Domain management → Add a domain** (for example `jayd.dev`).

## 2. Turn on the real AI assistant

1. Create an API key at console.anthropic.com and add a small credit balance. Short answers on a small model cost very little per conversation.
2. In Netlify → **Site configuration → Environment variables**, add:
   - `ANTHROPIC_API_KEY` = your key
   - `ALLOWED_ORIGIN` = your site address, e.g. `https://jayd.dev` (stops other sites using your key)
   - `ANTHROPIC_MODEL` (optional) = a model id from docs.claude.com/en/docs/about-claude/models
3. Redeploy. Ask the chat a question; the badge should say **live AI**.

Safety built in: the key never reaches the browser, visitors are limited to 20 questions per hour, messages are length-capped, and the assistant only answers about your professional profile and won't name employers or clients.

To change what the AI knows, edit the `KNOWLEDGE` text at the top of `chat.mjs`.

Also set a monthly spend limit in the Anthropic console.

## 3. Fix the link preview

In `index.html`, replace every `https://YOUR-DOMAIN` with your real address (near the top of the file). Then test the link at linkedin.com/post-inspector.

## 4. Visitor tracking (who clicked your email link)

1. Sign up free at goatcounter.com and pick a code, e.g. `jayd`.
2. In `index.html`, find the GoatCounter comment near `</head>`, put in your code and remove the `<!--` and `-->` around the script line.
3. Send each person their own link: `https://jayd.dev/?ref=company-name`. The dashboard shows visits per `ref`.

## 5. Things only you can fill in

In `index.html`, find `const LINKS` in the script:

- `linkedin`: your LinkedIn URL
- `cv`: put your CV in this folder (e.g. `JayD-CV.pdf`) and write its file name
- `cissp`, `pmp`, `iso27001`: your Credly badge or official verification links. Each **Verify ↗** link appears only once filled.

Just below, `TESTIMONIALS`: add 1–2 real quotes (with permission). The section appears automatically:

```js
const TESTIMONIALS=[
  {quote:"JayD led our ISO programme...", name:"Full Name", role:"Title, Organisation"},
];
```

Impact numbers (team size, systems secured, uptime, time saved): send them and they can be added to the numbers row in the Impact section.
