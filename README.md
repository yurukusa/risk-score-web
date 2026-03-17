# Claude Code Risk Scanner

> **Is Your Claude Code Safe?**
> Instantly scan your `CLAUDE.md` for dangerous commands, exposed secrets, and risky configurations.

![Demo GIF](./demo.gif)
<!-- Replace demo.gif with an actual screen recording of the scanner in action -->

---

## What It Does

The Claude Code Risk Scanner is a **single-file, fully client-side** web app that audits your `CLAUDE.md` (or any Claude Code instruction file) for common security mistakes.

No server. No API calls. No data leaves your browser.

### Scan Categories

| Severity | Penalty | Checks |
|---|---|---|
| ⛔ CRITICAL | −20 pts each | `rm -rf`, `git push --force` / `git reset --hard`, hardcoded secrets/API keys, unrestricted `sudo` |
| ⚠️ WARNING | −10 pts each | `git add -A` / `git add .`, automated POST to external URLs, `--no-verify` hook bypass |
| ℹ️ INFO | −5 pts each | CLAUDE.md over 5 KB, automatic `git commit` without approval gate, inline env-var values |

### Score Bands

| Score | Rating |
|---|---|
| 80–100 | ✅ SAFE |
| 60–79 | ⚠️ CAUTION |
| 40–59 | 🔶 WARNING |
| 0–39 | 🛑 CRITICAL RISK |

---

## Usage

### Option A — Open Directly in Browser

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/risk-score-scanner.git
cd risk-score-scanner

# Open in your default browser (no server needed)
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

### Option B — GitHub Pages (Recommended)

See [Deploy to GitHub Pages](#deploy-to-github-pages) below.

### How to Scan

1. Open the page in any modern browser.
2. Paste the full contents of your `CLAUDE.md` into the text area.
3. Click **"Scan Now"** (or press **Ctrl+Enter**).
4. Review the risk score, individual findings, and fix suggestions.

---

## Deploy to GitHub Pages

1. **Fork or clone** this repository to your GitHub account.
2. Go to **Settings → Pages** in your repository.
3. Under **"Build and deployment"**, select:
   - Source: `Deploy from a branch`
   - Branch: `main` / root (`/`)
4. Click **Save**.
5. GitHub Pages will publish the scanner at:
   ```
   https://YOUR_USERNAME.github.io/risk-score-scanner/
   ```

No build step, no dependencies — the single `index.html` is the entire app.

---

## Project Structure

```
risk-score-scanner/
├── index.html   # Complete scanner — HTML + CSS + JS in one file
└── README.md    # This file
```

---

## Customizing Rules

All scan rules are defined in the `RULES` array inside `index.html`. Each rule has:

```js
{
  id:     'unique_id',
  sev:    'critical' | 'warning' | 'info',
  pts:    20 | 10 | 5,     // penalty points
  icon:   '⛔',
  test:   (text) => /pattern/.test(text),   // detection function
  title:  'Short description',
  detail: 'Explanation of the risk',
  fix:    'Actionable remediation advice',
}
```

To add your own rules, append objects to `RULES` following the same shape.

---

## Go Deeper

The free scanner covers the most common patterns. The **Claude Code Ops Kit** provides:

- A battle-tested, hardened `CLAUDE.md` template
- Ready-to-use `PreToolUse` hook scripts (bash, Python)
- Dangerous-command blocklist with regex patterns
- 25-item Claude Code hardening checklist
- Secrets injection guide (env vars, vaults)

**[Get the Ops Kit on Gumroad →](https://yurukusa.github.io/cc-ops-kit-landing/)**

---

## License

MIT — free to use, share, and modify.

```
Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
