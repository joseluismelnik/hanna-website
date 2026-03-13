# Hanna's Blog

Personal blog built with [Hugo](https://gohugo.io/) + [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, hosted on [Netlify](https://netlify.com) for free. Posts can be written from a laptop (Markdown files) or from any browser including iPhone Safari (via Decap CMS at `/admin`).

**Live site:** https://hanna-in-spain.netlify.app/

---

## Initial Setup (one-time)

These steps only need to be done once when setting up on a new Netlify account.

### 1. Deploy to Netlify

1. Go to [netlify.com](https://netlify.com) and sign up (use "Log in with GitHub")
2. Click **Add new site** → **Import an existing project** → **GitHub**
3. Authorize Netlify to access your GitHub repos
4. Select the `hanna-website` repository
5. Build settings are auto-detected from `netlify.toml` — no changes needed
6. Click **Deploy site**

Your site will be live in ~1 minute. To set a custom subdomain: **Site configuration** → **Change site name**.

### 2. Enable Netlify Identity (for CMS login)

> **Note:** Netlify's new dashboard UI hides the Identity tab. Don't look for it in the sidebar — go directly to:
> `https://app.netlify.com/sites/hanna-in-spain/identity`

1. Click **Enable Identity**
2. Under **Registration preferences**, select **Invite only** (so random people can't sign up)
3. Under **External providers**, you can optionally enable Google login for convenience

### 3. Enable Git Gateway (so CMS can commit posts)

> Go directly to: `https://app.netlify.com/sites/hanna-in-spain/identity`

1. Scroll down to **Services** → click **Enable Git Gateway**

This allows the CMS to commit new posts to GitHub on your behalf without you needing to touch Git.

### 4. Invite yourself

1. Go to **Identity** tab → **Invite users**
2. Enter your email address → click **Send invite**
3. Check your email and click **Accept the invite**
4. Set a password — this is what you'll use to log into `/admin`

---

## Writing Posts from a Laptop

### Option A: Decap CMS (recommended, no Git knowledge needed)

1. Open https://hanna-in-spain.netlify.app/admin in your browser
2. Log in with your email and password
3. Click **New Post** in the Posts collection
4. Fill in:
   - **Title** — the post title
   - **Date** — defaults to now, adjust if needed
   - **Tags** — comma-separated, e.g. `spain, food, tech`
   - **Body** — write in the rich text editor (or switch to Markdown mode with the top-right toggle)
5. Click **Save** to save a draft, or **Publish** to make it live immediately
6. Netlify will rebuild the site automatically — your post is live in ~30 seconds

### Option B: Directly editing Markdown files

1. Create a new file in `content/posts/` named `your-post-title.md`
2. Add the frontmatter at the top:

```markdown
---
title: "Your Post Title"
date: 2026-03-13T12:00:00+01:00
tags: ["tag1", "tag2"]
draft: false
---

Your content here...
```

3. Save, then commit and push:

```bash
git add content/posts/your-post-title.md
git commit -m "Add post: Your Post Title"
git push
```

Netlify deploys automatically on every push.

### Adding images (from laptop)

1. Put the image file in `static/images/` (e.g. `static/images/my-photo.jpg`)
2. Reference it in your post:

```markdown
![Description of image](/images/my-photo.jpg)
```

When using the CMS, use the image upload button in the editor toolbar — it handles this automatically.

### Previewing locally before publishing

```bash
hugo server
```

Open http://localhost:1313 in your browser. Changes update live as you edit files.

---

## Writing Posts from iPhone (Safari)

No apps needed — everything works in Safari.

### First time: log in

1. Open Safari and go to https://hanna-in-spain.netlify.app/admin
2. Enter the email and password you set during initial setup
3. Tap **Log in**

### Writing a post

1. Tap **Posts** in the left sidebar
2. Tap **New Post** (top right)
3. Fill in the title, date, tags
4. Write your post in the body editor — use the toolbar for bold, headings, links, etc.
5. To add a photo: tap the image icon in the toolbar → **Upload** → choose from your camera roll
6. When done, tap the **Publish** button (top right) → **Publish now**

Your post is live on the site in about 30 seconds.

### Saving a draft

If you're not ready to publish, tap **Save** instead of **Publish**. Drafts are saved to GitHub but won't appear on the live site. You can come back later on any device and finish the post.

### Tips for iPhone

- The CMS works best in landscape orientation for the editor
- Use the **Rich Text** mode (default) rather than Markdown mode on mobile — easier with the touch toolbar
- If the page seems stuck after publishing, pull down to refresh — the CMS sometimes needs a nudge on mobile

---

## Site Structure

```
content/
  posts/        ← blog posts (managed by CMS or manually)
  about.md      ← About page
  search.md     ← Search page (do not delete)
static/
  admin/        ← Decap CMS files (do not modify)
  images/       ← uploaded images
hugo.toml       ← site configuration (title, theme, menus)
netlify.toml    ← build settings for Netlify
themes/
  PaperMod/     ← theme (git submodule, do not edit)
```

## Changing Site Settings

Edit `hugo.toml` to change:
- **Site title** — `title = "..."`
- **Homepage blurb** — `[params.homeInfoParams]` section
- **Navigation menu** — `[[menu.main]]` entries
- **Author name** — `author = "..."`

After editing, commit and push — Netlify rebuilds automatically.

---

## Troubleshooting

**CMS login fails / "Git Gateway Error"**
Make sure Git Gateway is enabled: Netlify dashboard → Site configuration → Identity → Services → Enable Git Gateway.

**Post published but not showing on site**
Check the Netlify dashboard → **Deploys** tab to see if the build succeeded. If it failed, the error message will be shown there.

**Image not showing in post**
Make sure the filename has no spaces and the path starts with `/images/` (not `static/images/`).

**CMS not loading on iPhone**
Try a hard refresh (hold the reload button in Safari → Reload Without Content Blockers). Some ad blockers interfere with the CMS script.
