# Personal Assistant

A personal Claude-powered chat assistant with a local knowledge base.

## Project Structure

```
chat-app/
├── netlify.toml                        # Netlify build config
├── package.json                        # Node project file
├── .gitignore
├── public/
│   └── index.html                      # Chat UI
└── netlify/
    └── functions/
        ├── chat.js                     # Serverless function + Claude API proxy
        └── knowledge.txt               # Your knowledge base — edit this
```

## Updating the Knowledge Base

Edit `netlify/functions/knowledge.txt` and redeploy.
Use `##` headings to organize sections. Plain text, no special format required.

## Deploy: Zip Upload (quick)

1. Zip the `chat-app` folder
2. Go to your Netlify site → **Deploys** → drag the zip onto the dropzone
3. Done — no build settings needed

## Deploy: GitHub (recommended for ongoing use)

1. Push this folder to a GitHub repo
2. In Netlify: **Add new site → Import from Git → select your repo**
3. Build settings (Netlify usually auto-detects from `netlify.toml`):
   - Build command: *(leave blank)*
   - Publish directory: `public`
   - Functions directory: `netlify/functions`
4. Go to **Site configuration → Environment variables** → add:
   - `ANTHROPIC_API_KEY` = your key from https://console.anthropic.com
5. Deploy

After that, every `git push` triggers an automatic redeploy.
To update the knowledge base: edit `knowledge.txt`, commit, push.

## First-time Netlify setup (either method)

Make sure `ANTHROPIC_API_KEY` is set under:
**Site configuration → Environment variables**

## Debug

Click the **KB?** button in the app header to confirm the knowledge base is loading.
