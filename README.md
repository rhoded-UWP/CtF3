# CtF Final Protocol (Level 3) — Capture the Flag

The trilogy finale. A browser-based Capture the Flag activity for a high school Cybersecurity workshop: **20 hidden flags**, a draining "target integrity" meter, a 20-node sector map, and escalating breach alarms. Sequels: [Level 1](https://rhoded-uwp.github.io/CtF_v1/) · [Level 2](https://github.com/rhoded-UWP/CtF2).

## The 20 flags

**13 returning types** (one of every category from Levels 1 and 2, all with new values): HTML comment, JS source, data attribute, meta tag, CSS comment, broken image src, hidden element, same-color text, console message, CSS `::after`, robots.txt recon, Caesar cipher (ROT-13 this time), and Network-tab JSON intercept.

**7 brand-new types:**

| Challenge | Skill taught |
|---|---|
| **Local Storage** | Application tab → Storage |
| **Cookie** | `document.cookie` / Application → Cookies |
| **Base64 Beacon** | `atob()` in console; encoding is a costume, not a safe |
| **Binary Beacon** | 8-bit binary → ASCII, by hand or with code |
| **Dormant Function** | A function nothing calls — students must invoke it from the console |
| **Secret Code** | The Konami code; the listener is readable in the source |
| **Master Key (capstone)** | Two shards: one in the external `js/uplink.js`, one on the hidden `/vault/` page it points to; assemble `flag{alpha_beta}` |

## What's new beyond CtF-2

- **Deep-ice cyan theme** with aurora accents — a new visual chapter after two green levels
- **Particle network backdrop** (mouse-reactive nodes + lines, ~25fps, FX toggle, pauses on hidden tabs)
- **Animated ASCII "ICEBREAKER" banner** with aurora shimmer
- **Target integrity meter** — drains 5% per capture; the progress bar is the *victim's* health bar
- **Sector map** — 20 chamfered nodes that light up as flags fall
- **Breach milestones** at 5/10/15 captures: red vignette bleeds in, log feed panics, stage-3 alarm pulse
- Everything from CtF-2 carries forward: typed boot/outro sequences, glitch title, capture bursts, scramble text, live log feed, `prefers-reduced-motion` support, no audio

## Scoring (rebalanced for 20 flags)

- **35 points** per flag, minus **2** per full minute elapsed (gentler than Levels 1–2's −5), floored at **5** — a flag at minute 15 is still worth 5×+ the floor
- Each hint costs **5 points**; max possible score 700
- Answers stored as **SHA-256 hashes**; 50+ decoy `flag{...}` strings across the page, robots.txt, the memo, the external script, the vault, and the live log feed

## Files

```
index.html          the main console
robots.txt          recon flag: points at /hidden/
hidden/keycard.txt  what robots.txt tried to hide
api/telemetry.json  network flag payload (fetched, never displayed)
js/uplink.js        external script: master key shard alpha + the vault pointer
vault/index.html    hidden page: master key shard beta + assembly protocol
```

## Deployment

Static host (GitHub Pages) — same two requirements as Level 2:

1. **Serve over http(s).** `file://` breaks `fetch()` and the recon flags. Local test: `python -m http.server` in this folder.
2. On a project site (`username.github.io/CtF3/`), robots.txt lives under the project path; the in-page hint ("add /robots.txt to this page's URL") handles that correctly.

---

Built for the CS Cybersecurity Workshop. Stay curious, stay ethical.
