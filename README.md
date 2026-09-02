# AI Delivery Portfolio Dashboard

Single-file HTML dashboard tracking Loyalty Juggernaut's AI delivery portfolio.

⚠️ **This repository contains commercially sensitive material.** Client names,
commercial figures, named individuals, candid assessments of client
dissatisfaction, and unannounced delivery commitments. It must never be served
from a publicly readable URL.

---

## Contents

| Path | Purpose |
|---|---|
| `index.html` | The dashboard. Fully self-contained — inline CSS/JS, no external requests. |
| `CHANGELOG.md` | Dated record of what changed each refresh, and the source for each change. |
| `.github/workflows/` | Reserved for a future build step. No secrets are stored here. |

---

## Hosting — read before you deploy

**Do not use GitHub Pages.** Pages sites are publicly readable. A private repo
does *not* produce a private Pages site; access-controlled Pages requires
GitHub Enterprise Cloud. Publishing this file to Pages exposes the whole
portfolio to anyone with the URL, and to search engines.

### Recommended: Cloudflare Pages + Cloudflare Access

1. Push this repo to GitHub as a **private** repository.
2. Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git.
3. Select the repo. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: `/`
4. Deploy. Note the `*.pages.dev` URL.
5. **Immediately** lock it down — Zero Trust → Access → Applications → Add:
   - Type: Self-hosted
   - Domain: your `pages.dev` hostname
   - Policy: Allow → Emails ending in `@lji.io`
6. Verify in a private browser window that you are challenged for login.

Cloudflare Access is free up to 50 users. Step 5 is not optional — between
deploy and policy creation the site is world-readable.

### Alternatives

- **Vercel** — connect the private repo, then enable Deployment Protection
  (Vercel Authentication). Requires a Pro plan.
- **Netlify** — connect the repo, then Site settings → Access control →
  password protection or SSO. Requires a paid plan.
- **GitHub Enterprise Cloud** — Pages with access control restricted to org
  members. Only viable if LJI is already on Enterprise Cloud.
- **Internal LJI server** — behind the existing VPN/SSO. No third party involved.

---

## Updating

The dashboard is refreshed by a scheduled Claude Cowork task that produces a
**draft report only** — it does not edit `index.html`. The workflow is:

1. Scheduled task runs and reports what changed across Jira, email, and the
   AI SoS transcripts.
2. You review the proposed changes.
3. Approved changes are applied to `index.html`.
4. Commit, push, and Cloudflare redeploys automatically.

```bash
git add index.html CHANGELOG.md
git commit -m "Refresh: <date> — <one-line summary>"
git push
```

### Why the narrative is not automated

Jira reports state; it does not report meaning. Two examples from the Aug 25
refresh that no automated pull would have caught:

- Ali Lootah signed off the AI Individualize UAT build in an **email thread**
  on 24 Aug. The Jira issue and every AI SoS transcript were silent on it. An
  automated Jira-only refresh would have kept showing "awaiting Ali" — a month
  stale and wrong about the most important state change on the account.
- WestJet's Jira status looked healthy while the 21 Aug SoS recorded the client
  rejecting a solution proposed two months earlier. The move from "On Track" to
  "Client Pushback" was a judgment call, not a data change.

Facts can be pulled. Meaning has to be reviewed.

---

## Data sources

| Source | What it provides |
|---|---|
| Jira — `AT` project (bankofloyal.atlassian.net) | Issue status, keys, comments, transitions |
| Gmail | Client-facing commitments, sign-offs, contact reports |
| Google Drive — "AI SoS" Gemini notes | Internal delivery detail, blockers, decisions |
| Monday.com | Contact reports |

## Structure of `index.html`

A single `<script>` block holds `const clients = { ... }`, keyed by client slug.
Each entry carries `name, jiraKey, jiraUrl, status, statusLabel, owner,
briefing, modules[], timeline[], risks[], jiraLinks[]`.

Several surfaces are authored as static HTML and must be updated alongside the
data object — they do not render from it:

- attention cards (`#section-attention`)
- upcoming deliveries table (`#section-deliveries`)
- portfolio table (`#section-portfolio`)
- the KPI tiles at the top

### Validate before committing

```bash
python3 - <<'PY'
import re
h = open('index.html', encoding='utf-8').read()
open('/tmp/dash.js','w').write(re.findall(r'<script[^>]*>(.*?)</script>', h, re.S)[0])
print('div', h.count('<div'), h.count('</div>'), '| tr', h.count('<tr'), h.count('</tr>'))
PY
node --check /tmp/dash.js && echo "JS OK"
```

Unescaped `"` inside a double-quoted JS string is the recurring failure mode —
it has broken this file twice. Escape as `\"` inside `note:` and `text:` fields.
