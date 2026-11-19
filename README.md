# Orfreon website

Prototype v0.1.0 is an early preview of Orfreon, a planned experimental exokernel. The prototype version refers to the website. The kernel is in early planning, and no kernel release is available.

The site uses static HTML and CSS with system fonts. There are no runtime dependencies or build steps, and all navigation works without JavaScript.

## Local development

Run this from the project root with Python 3 installed.

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Open [http://127.0.0.1:8000/](http://127.0.0.1:8000/). Edit `index.html` or `assets/css/style.css`, then refresh the browser. To preview without a server, open `index.html` directly.

## Cloudflare Workers Static Assets

The Wrangler configuration is in `deploy/cloudflare/`. With a supported Node.js version and npm installed, run the following from the project root to stage only the public site files and preview them locally.

```sh
mkdir -p deploy/cloudflare/public
cp index.html deploy/cloudflare/public/
cp -R assets deploy/cloudflare/public/
npx wrangler dev --config deploy/cloudflare/wrangler.jsonc
```

Open the local URL printed by Wrangler. Restage the files after edits. If you remove or rename an asset, start with an empty `deploy/cloudflare/public` directory so stale files stay out of the deployment.

When ready to publish, stop the preview server. Confirm the Worker name in `wrangler.jsonc` is available in the correct Cloudflare account, and run these commands manually.

```sh
npx wrangler login
npx wrangler deploy --config deploy/cloudflare/wrangler.jsonc
```

Use the URL printed by Wrangler to verify the page and stylesheet. See [Cloudflare Workers Static Assets](https://developers.cloudflare.com/workers/static-assets/).

## GitHub Pages

In a repository you control, prepare a publication branch with `index.html` and `assets/` at its root. Add an empty `.nojekyll` file to serve the files directly. When ready to publish, push that branch and select it under **Settings → Pages → Build and deployment → Deploy from a branch**, using **/ (root)** as the folder. Relative stylesheet paths support both user sites and project sites hosted under a repository subpath. See [GitHub Pages publishing sources](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Verification

- Follow the About, Vision, and Ecosystem links and confirm that they reach the corresponding content. Both GitHub links should open the Evan-Windproof profile.
- Use Tab to reveal the skip link and check visible focus on navigation links. Check the page at mobile, tablet, and desktop widths.
- With reduced motion enabled, check that anchor navigation jumps directly and link transitions are disabled.
- Check that the hero, ecosystem entries, and development status identify Orfreon and its planned operating systems as future projects.

## License

A license decision is pending.
