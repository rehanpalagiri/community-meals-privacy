# Community Meals — public privacy policy

The published privacy policy for the **Community Meals** volunteer app, served by GitHub Pages at:

**https://rehanpalagiri.github.io/community-meals-privacy/**

That URL is what App Store Connect points at. Apple requires a publicly reachable privacy-policy
URL, and the app's own source repo is private — which is the only reason this repo exists
separately. Nothing else lives here.

## What this repo is

One file, `index.html`, with its CSS inlined. No build step, no dependencies, no framework. Editing
the file and pushing to `main` publishes it.

## It is a mirror, and it is synced by hand

`index.html` is a copy of `src/app/privacy.tsx` from the app's private repo
(`rehanpalagiri/Food_Volunteering`). **That file is the source of truth. This one is downstream.**
There is no automation keeping them in step, so they can drift, and drift here means the policy
Apple links to says something different from the policy in the app.

The **“Last updated” date is the tell.** In the app it is rendered from `POLICY_VERSION` in
`src/lib/policyVersion.ts` and never typed by hand; here it is literal text. If the two dates differ,
this page is stale.

That date is not decoration. Guardian consent for volunteers aged 13–17 is pinned to
`POLICY_VERSION`: a material rewrite makes existing consents stale and every guardian is asked
again. So the version this page shows should match the version consent is being measured against.

### Syncing it

1. Read `src/app/privacy.tsx` in the app repo — the whole file, not the diff.
2. Update the sections here to match. The markup maps directly: `<Section title="…">` → `<section>`
   + `<h2>`, `<Bullet>` → `<li>`, `<B>` → `<strong>`, `<Text style={s.body}>` → `<p>`.
3. Set the “Last updated” line to `formatPolicyDate(POLICY_VERSION)` — e.g. `2026-09-03` renders as
   `September 3, 2026`. Note it is **not** built with `new Date()`, which would be UTC midnight and
   render a day earlier west of Greenwich.
4. Diff the prose before pushing. Comparing the set of words on each side catches a dropped clause
   far more reliably than reading both; a real omission shows up as policy vocabulary present in the
   app and missing here.
5. Commit as `Sync with the in-app policy: <what changed>`, matching the existing history.

## Current state

Synced **2026-09-03** against the guardian-consent rewrite: 20 sections, up from 9. That pass added
the guardian-consent disclosures (what a guardian's details are used for, the five separate items,
what a coordinator is and is not shown) and the sections on responsibility, collection method,
purposes, on-device storage, hand-off to other apps, sub-processors, breach notification, consent
withdrawal, succession, and data-subject rights.

## What must not drift

Three things are load-bearing and are asserted or relied on elsewhere:

- **The 13 age floor.** Not negotiable and not overridable by a guardian — COPPA requires
  *verifiable* parental consent, which a tick-box is not.
- **Full names are visible to fellow organization members, and that is not optional.** The app says
  so, and a guardian acknowledges it rather than choosing it.
- **A guardian's own name, email and phone reach no other volunteer or coordinator, ever.**

## Not here

The Community Guidelines (`src/app/guidelines.tsx`) are in-app only and have no public mirror. They
are separately versioned by `GUIDELINES_VERSION`.
