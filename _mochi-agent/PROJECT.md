# all-printable — what it is

The marketing home for all-printable: a **one-page site** at **https://all-printable.com/**,
plus roughly forty redirect stubs for URLs that predate the split from the app.

**This is the product's own record.** It is kept current by the agents that work this repo, and
it is theirs to read before changing anything.

> **Created 2026-09-04.** This repo was worked as part of the `all-printable` project until
> then, alongside `all-printable-app-www`. A project now owns exactly one repo, so this became
> a product in its own right — with, honestly, very little written about it: nearly everything
> the old shared record said was about the app.

## Repos

| Repo | Publishes | Holds |
|---|---|---|
| [`all-printable-www`](https://github.com/ptk-studio/all-printable-www) | **https://all-printable.com/** | the one-page marketing home, and ~40 redirect stubs |

Public, default branch `main`.

**The catalogue is a separate product**, at
[`all-printable-app-www`](https://github.com/ptk-studio/all-printable-app-www), publishing
**https://app.all-printable.com/**. It has its own `_mochi-agent/`.

## How code reaches production

**A merge to `main` is a production deploy.** GitHub Pages publishes from `main`; there is no
staging and no build step, so a merge is live within a minute or two.

> This is the same rule as the app repo, and it is unconditional here. There is no route that
> ships without deploying.

**Rollback is a revert commit**, deployed the same way.

## How a change is verified

**Not established.** This repo has had no agent tick of its own, so nothing here has been run
and confirmed rather than assumed — it is a static one-page site with no build and no CI, but
that is a reading of the tree, not a verification.

The first agent to work this repo owes this section: what to serve locally, what to open, and
what a pass looks like. **Do not fill it in from what a site like this usually needs.**

**What only a human or a browser can check:** that
[all-printable.com](https://all-printable.com/) actually loads after a merge, and that the
redirect stubs still land where they should. An unattended run has no browser and, from the
cloud, no route to the host.

## What bites

Nothing recorded yet, honestly rather than optimistically — no tick has worked this repo alone.

- **The redirect stubs are the part most likely to bite.** Forty of them exist to keep
  pre-split URLs working; a change that quietly breaks one is invisible on the page itself.

## Deliberately not doing

- Nothing recorded yet.
