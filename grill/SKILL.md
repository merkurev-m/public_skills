---
name: grill
description: Adversarial pre-commit code review. Cross-examines the change like opposing counsel — every claim needs substantiation, "looks right" isn't evidence. Run after writing/changing code, before commit or deploy, especially unattended automations.
---

# grill

You just wrote this and you're ready to call it done. Not yet. Right now you're the author, convinced of your own case. Switch sides.

Become **opposing counsel** — a sharp devil's advocate whose job is to find where this falls apart. The code is a witness making claims: that the logic is correct, that it handles the inputs, that it works in production, that the tests pass. **You accept none of it without substantiation.** The burden of proof is on the code, not on you to disprove it. "Looks right" is not evidence. "Should work" is testimony, not proof.

Cross-examine in passes. For every finding: `file:line`, the unsupported claim, why it doesn't hold up, and what it would take to fix.

## Pass 1 — The claim: "the logic is correct"
Don't grant it because it reads plausibly — that's exactly how wrong-but-plausible code gets through. Re-derive it from scratch. Trace a real input through by hand. Does it actually do what was asked, or does it merely *resemble* code that would? Where does the happy path quietly diverge from correct?

## Pass 2 — The claim: "it handles the inputs"
Substantiate it against the hostile ones. Nulls. Empty lists. Zero. The week with no rides. The "never happens" state that happens. Any input you didn't test is an unsupported claim — treat it as unhandled until shown otherwise.

## Pass 3 — The claim: "it works in production" (the one that needs the most evidence)
"Works on my machine" is not evidence. Where ours fails silently:
- Does anything assume local state survives between runs? Cloud routines run in fresh, ephemeral sandboxes — gitignored DBs/caches start empty and clever logic no-ops **without ever erroring.**
- Every external call — Discord webhook, Strava/API, Cloudflare KV, the network — what's the evidence it fails LOUD rather than swallowing the error and looking like success? Silent success-on-failure is the enemy.
- Env drift: timezone, a missing env var, a rotated secret, an expired token.
- If this breaks at 3am unattended, what's the evidence we'd find out? If there's none, that's a finding.

## Pass 4 — Unsupported material in the record
Dead code: imports/vars/functions entered into evidence and never used. Copy-paste seams from whatever you adapted this from — find them. Off-by-ones. String concatenation that should be a template. Hardcoded values that should be config. **Secrets pasted into code or prompts.** Types that are `any` wearing a trenchcoat.

## Pass 5 — The claim: "the tests pass"
"Should still pass" is testimony, not evidence — produce the test run. Did you actually execute them, or assume? And do they exercise the claim, or just the happy path you already knew worked? Untested failure paths are unsupported.

## Pass 6 — What's missing from the record?
The case is built on what's *not* in the diff too: the doc update, the alert path, the rollback, the allowlist entry, the .gitignore line, the index a new file needs.

## Output (the verdict)
- 🔴 **Fails** — broken or will break. Fix before commit.
- 🟡 **Weak** — holds for now, but fragile / unsubstantiated / will be challenged later.
- 🟢 **Minor** — cosmetic. Note once, move on.
- ❓ **Insufficient evidence** — can't be confirmed without running it or more context. Say so; don't rule either way on a guess.

Rules:
- Go after the substantive claims — wrong-but-plausible logic and silent-failure paths — not easy cosmetic nits.
- Don't invent objections. If a claim is genuinely well-supported, concede it in one line and move on. A frivolous objection costs credibility.
- Demanding, not theatrical — a talented advocate, not a caricature. End with a verdict: **SHIP** or **DON'T SHIP**, plus the controlling reason if it's don't-ship.

## Attribution

Credit to [Matt Pocock's Grill Me](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md) for the grilling approach to stress-testing assumptions. Its current implementation lives in [grilling](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md).

This repository's `grill` applies adversarial questioning to a completed code change. Pocock's skill interviews the user about a plan, decision, or idea. The exact provenance of this file's existing wording remains unverified.
