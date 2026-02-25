# Personal Assistant

A personal Claude-powered chat assistant with a local knowledge base, deployed on Netlify.

## Project Structure
```
chat-app/
├── netlify.toml                        # Netlify build config
├── package.json
├── .gitignore
├── public/
│   └── index.html                      # Chat UI
└── netlify/
    └── functions/
        ├── chat.js                     # Serverless function + Claude API proxy
        └── knowledge.txt               # Your knowledge base — edit this
```

## Updating the Knowledge Base

Edit `netlify/functions/knowledge.txt` and push to GitHub. Netlify redeploys automatically.
Use `##` headings to organize sections. Plain text, no special format required.

## Netlify Configuration

`netlify.toml` must include these settings for `knowledge.txt` to be bundled correctly:
```toml
[build]
  publish = "public"
  functions = "netlify/functions"

[functions]
  node_bundler = "zisi"
  included_files = ["netlify/functions/knowledge.txt"]

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

- `node_bundler = "zisi"` — uses the zip bundler instead of esbuild
- `included_files` — explicitly tells Netlify to bundle `knowledge.txt` with the function

## Environment Variables

In Netlify: **Site configuration → Environment variables** → add:
- `ANTHROPIC_API_KEY` = your key from https://console.anthropic.com

## GitHub → Netlify Deployment

1. Push this repo to GitHub
2. In Netlify: **Add new site → Import from Git → select your repo**
3. Netlify auto-detects settings from `netlify.toml` — no manual build config needed
4. Add the `ANTHROPIC_API_KEY` environment variable
5. Deploy

After that, every `git push` triggers an automatic redeploy.