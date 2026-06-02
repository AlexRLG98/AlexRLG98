# Visa-ready content edits — Profile README

This branch (`visa-ready`) replaces the public profile README with a
minimal placeholder for the duration of the F-1 visa window. The
interview is scheduled on **2026-06-04** at the US Embassy in Paris.

Because this repository must remain **public** for GitHub to render
the README on the user's profile page, the original (richer) README
remains visible in the git history through `git log` on `main`. The
visa-ready commit only changes the *current* content rendered on the
profile.

The change is forward-only — no commit was amended, rebased, squashed,
or force-pushed.

## Git anchors

| Anchor | SHA | Meaning |
|---|---|---|
| `main` (before edits) | `b720929da716c0bf7329fe0b16ad85dc94d0c097` | Last commit on `main` before the visa-ready branch was cut |
| Tag `pre-visa-edit` | `7c1b3fa33f352cf97036b2fe1b64be8676cbbaf4` | Annotated tag object pointing at the above commit. Pushed to `origin`. |
| `visa-ready` HEAD | `173f7ee3c07ffe555a5045f00e87658afb1d7a25` | Last commit on this branch |

Snapshot taken on **2026-06-02**.

## Forward-only commits on `visa-ready`

```
173f7ee refactor(content): switch README to minimal placeholder during visa window
```

## What changed

The previous `README.md` rendered an *About Me* `class Alexandre`
Python block, a full *Tech Stack* listing (Languages / Frontend /
Backend / DevOps / Security), GitHub stats cards, and a *Featured
Projects* badge. The visa-ready version drops all of that and keeps:

- The typing SVG tagline (reworded to drop "Security Researcher", now
  reads "Full-Stack Developer / Epitech Nice / TEK3 Student").
- Three link badges: Portfolio, LinkedIn, Email.
- A single italic line: "TEK3 student at Epitech Nice · Monaco".
- The profile views counter.

What was removed:

- `self.interests = [..., "Cybersecurity & Pentesting", ...]`
- `self.current_focus = "Building my CTF platform with 61 challenges"`
- The `Security: CTF • Pentesting • Reverse Engineering` line.
- The `Security Researcher` mention in the typing SVG.

What stayed: name, profession (Full-Stack Developer), school
affiliation, location, contact links.

## How to roll back after the visa interview

```bash
git fetch --tags
git checkout main
git reset --hard pre-visa-edit
git push origin main --force-with-lease

git tag -d visa-rollback-done 2>/dev/null || true
git tag -a visa-rollback-done -m "Rollback applied after visa receipt"
git push origin visa-rollback-done

# Optionally clean up
# git branch -D visa-ready
# git push origin --delete visa-ready
# git tag -d pre-visa-edit
# git push origin --delete pre-visa-edit
```

The rollback restores the full original README (including the
`class Alexandre` block and the Tech Stack section) — i.e. exactly
the state captured at commit `b720929`.

## Historical commits are still visible

Even though `main` will be rewound after the rollback, the public
GitHub UI keeps the older commits in `git log` and the per-commit
content. This is the trade-off documented in the original brief.
The risk is judged acceptable: an immigration officer reviewing the
profile reads the *current* README, not the git history.
