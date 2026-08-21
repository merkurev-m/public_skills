# public_skills

Two Claude Code skills I use in daily work, published so I can link to them.

A skill is just a folder with a `SKILL.md` inside. Claude reads the `description` in the frontmatter, decides whether the current task matches, and loads the full file only when it does. No code, no install step, no dependencies.

## The skills

### `grill`, adversarial pre-commit review

You finish writing code and you are convinced it works. That is exactly the moment you are the worst judge of it. `grill` makes Claude switch sides and cross-examine the change like opposing counsel: every claim needs evidence, "looks right" is not evidence, "should work" is testimony.

Six passes: is the logic actually correct, does it handle hostile inputs, will it survive production, what dead code and hardcoded values are in the diff, did the tests actually run, what is missing entirely. Ends with a verdict, SHIP or DON'T SHIP.

Built for unattended automations, where the failure mode is not a crash but silent success. A cloud job that starts with an empty cache and no-ops without ever erroring will pass every review that only reads the diff.

**Use it:** after writing or changing code, before commit or deploy.

### `council`, five advisors and one verdict

Ask one AI, get one answer, and you have no way to tell if it is good because you only saw one perspective. `council` runs the question through 5 advisors with deliberately conflicting lenses (Contrarian, First Principles, Expansionist, Outsider, Executor), has them peer-review each other anonymously, then a chairman synthesizes where they agree, where they clash, and what to actually do.

For decisions where being wrong is expensive. Not for questions with one right answer.

**Use it:** "council this", "pressure-test this", or any real decision with a tradeoff.

## Install

Copy the folder you want into your skills directory.

Personal, available in every project:

```bash
git clone https://github.com/merkurev-m/public_skills.git
cp -r public_skills/grill ~/.claude/skills/
cp -r public_skills/council ~/.claude/skills/
```

Or per project, checked into the repo so your team gets it too:

```bash
cp -r public_skills/grill .claude/skills/
```

Restart Claude Code, then run `/grill` or say "council this". Both also trigger on their own, `grill` after a code change and `council` on a real decision, because that is what the `description` field is for.

The same folder works in the Claude desktop app and on claude.ai too, they just take it as a zip upload in Settings instead of a directory on disk.

## Credits

Neither skill is my work. I use both daily and I am publishing copies so an article can link to
something stable, not because I wrote them.

`council` is adapted from the [LLM Council skill by Ole Lehmann](https://github.com/aiwithremy/claude-skills-llm-council),
which implements [Andrej Karpathy's LLM Council](https://github.com/karpathy/llm-council). My copy
renames the skill and drops the HTML report step in favour of printing the verdict straight into
the chat. Everything else is his. Go star his repo.

`grill` I picked up somewhere and genuinely cannot trace back. Before publishing I searched GitHub
code for four distinctive phrases from it (`Unsupported material in the record`,
`a talented advocate, not a caricature`, `Silent success-on-failure is the enemy`,
`A frivolous objection costs credibility`) and got zero hits on all four. Web search surfaced only
unrelated skills that happen to share the name. If it is yours, open an issue: I will credit you
properly, or take it down, whichever you prefer.

## License

There is no license file here, deliberately. I did not write either skill, so neither is mine to
license. `council` is Ole Lehmann's, and his own repo carries no license either. `grill` belongs to
whoever wrote it.

In practice: copy them into your `.claude/skills/` and use them. Do not resell them or pass them off
as your own. If either author asks for this repo to come down, it comes down.
