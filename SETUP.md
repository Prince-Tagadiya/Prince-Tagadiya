# Setup Guide — Creato4 Edition

## 1. File structure

Push all of this into the root of your `Prince-Tagadiya/Prince-Tagadiya` repo, keeping the folders intact:

```
Prince-Tagadiya/
├── README.md
├── assets/
│   ├── creato4-logo-rounded.svg   ← your logo, clipped to rounded corners + glow ring
│   ├── circuit-divider.svg        ← the repeating "signal" section divider
│   ├── terminal-boot.svg          ← the animated terminal boot sequence
│   ├── the-collective.svg         ← the 4-engineer team diagram
│   └── signal-strength.svg        ← the animated skill bars
└── .github/
    └── workflows/
        ├── snake.yml               ← required for the contribution snake
        └── self-host-stats.yml     ← optional reliability upgrade (see §3)
```

Commit and push to `main`.

## 2. Turn on the contribution snake (one-time, ~2 minutes)

The snake in section 08 needs to run once before it exists:

1. Go to your repo's **Actions** tab. If prompted, click **"I understand my workflows, enable them."**
2. Open **Generate Signal Snake** in the left sidebar → **Run workflow** → **Run workflow**.
3. Wait ~30 seconds, then refresh your profile page. It also re-runs automatically every day and on every push to `main`, so you never have to touch it again.

If nothing appears after running it, check **Settings → Actions → General → Workflow permissions** and make sure **"Read and write permissions"** is selected — the action needs that to publish to the `output` branch.

## 3. (Optional) Self-host the stat cards for 100% uptime

By default, README.md pulls the GitHub Stats / Top Languages / Streak cards live from their public endpoints (github-readme-stats.vercel.app and streak-stats.demolab.com). These are free community services — reliable most of the time, but they're shared infrastructure and can occasionally get rate-limited.

`self-host-stats.yml` is already included and will bake those same three cards into static SVGs in `assets/generated/` on a daily schedule. To switch over to the bulletproof version once it's run at least once:

- Replace the GitHub Stats `<img src="...">` in section 08 with `assets/generated/stats.svg`
- Replace the Top Languages `<img src="...">` with `assets/generated/top-langs.svg`
- Replace the Streak `<img src="...">` with `assets/generated/streak.svg`

You can do this immediately or wait until you notice a card fail to load — the live version works fine on its own.

## 4. Customizing

- **Brand colors** were sampled directly from your logo (`#1D4623` deep green, `#F5E6CA` cream) plus one added accent gold (`#E3B34A`) for highlights. They're used consistently across every badge, chart, and custom SVG — search-and-replace these six hex codes (see the top of any file in `assets/`) if you ever want to shift the palette.
- **The Collective diagram** (`the-collective.svg`) hard-codes the four names and roles from your team carousel. If roles change, regenerate it or edit the `<text>` elements directly — each member's initials, name, and role are plain, readable SVG text nodes.
- **Terminal boot sequence** (`terminal-boot.svg`) types out once on page load and then holds with a blinking cursor, rather than looping — regenerate the underlying script if you want to change the lines.

## 5. A couple of honest platform notes

GitHub sanitizes README HTML for security, which rules out a few things that were requested and are worth knowing about rather than silently faking:

- **True `:hover` states and JavaScript-driven interactivity are not possible** in a rendered README — GitHub strips `<style>`/`<script>` and disables interaction on embedded images. Every "interactive-feeling" element here (the typing text, the terminal boot, the traveling signal pulses, the skill-bar shimmer) is instead *autoplaying* motion baked into the SVGs themselves, which is the closest real equivalent GitHub supports.
- **Real scroll-linked parallax** isn't possible for the same reason. The waving capsule-render banners and layered gradients approximate depth without needing scroll events.

Everything else in the brief — animated SVGs, the circuit-flow signal motif, the animated team/timeline diagrams, dynamic GitHub metrics, the contribution snake, terminal simulation — is real, working, and self-contained in the files above.
