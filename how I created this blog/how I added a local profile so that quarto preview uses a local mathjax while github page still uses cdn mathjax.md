When I am offline, I was not able to use quarto preview as I the mathjax script that needs to be downloaded from the CDN was not available. So I set us a quarto profile, so so that I invoked quarto preview as:
```bash
quarto preview --profile offline
```
It used the offline profile, that instructed the quarto system to download any assets and and use local assets.

## Question

I want it to use a local copy for quarto preview but for the website it serves from github i want it to use a cdn

## Gemini's Solution

That is a super smart optimization. Serving from a CDN on the live site gives your readers faster load times globally, while keeping a local fallback lets you render LaTeX smoothly during offline drafting sessions on your laptop.

Quarto actually supports environment-based overrides, but the cleanest way to handle this without maintaining two separate `_quarto.yml` files is using a simple **local profile**.

---

### Step 1: Set up a Profile for Local Offline Preview

In the same folder as your main `_quarto.yml`, create a new file named `_quarto-offline.yml`:

```yaml
# _quarto-offline.yml
format:
  html:
    self-contained-math: true

```

That’s all that goes in it! Quarto will merge this file with your main `_quarto.yml` whenever you activate the `offline` profile.

---

### Step 2: Keep your Main Configuration Default (CDN)

Make sure your primary `_quarto.yml` stays configured for production (CDN). It should look standard:

```yaml
# _quarto.yml
project:
  type: website

format:
  html:
    theme: cosmo
    # Quarto defaults to CDN mathjax/katex when self-contained-math is not set

```

---

### Step 3: How You Run It

Now you get the best of both worlds:

#### 1. When working offline locally:

Run your preview using the `--profile` flag:

```bash
quarto preview --profile offline

```

* **What happens:** Quarto merges `_quarto-offline.yml` into `_quarto.yml`. It fetches/uses the local bundled MathJax assets so all your equations render instantly without an internet connection.

#### 2. When GitHub Actions publishes your live site:

When you run `git push origin main`, your GitHub Actions workflow runs the default build command (`quarto publish` / `quarto render`).

* **What happens:** Since GitHub Actions doesn't pass `--profile offline`, it uses only `_quarto.yml`. It compiles your blog linking directly to the high-speed CDN JS files!
