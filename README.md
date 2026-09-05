# Agent skills

## `bridge-mode` 🖖

Complete your request with only the explanation and input it needs.

### Motivation

Coding agents often narrate routine work, repeat information, and add unsolicited
advice. Bridge Mode takes its cue from the *Star Trek* bridge computer: answer
the request, report what matters, and stop.

### Principle

Keep the information you need to understand, act, verify, or decide.

Lead with the answer or result. Follow with the necessary evidence, conditions,
and uncertainty. Detailed explanations belong when the task requires them;
brevity follows from removing what does not help.

### Install

#### Codex

Run in your terminal:

```bash
codex plugin marketplace add sotayamashita/skills
codex plugin add bridge-mode@sotayamashita-skills
```

#### Claude Code

Run in Claude Code:

```text
/plugin marketplace add sotayamashita/skills
/plugin install bridge-mode@sotayamashita-skills
```

#### Skill-only fallback

For clients that support Agent Skills but not plugins:

```bash
npx skills add sotayamashita/skills --skill bridge-mode
```

### FAQ

#### How does it differ from [Caveman](https://github.com/JuliusBrussee/caveman)?

Both remove filler. Bridge Mode focuses on what to include and what comes
first. Caveman focuses on shorter wording, using short sentences and fragments
when the meaning stays clear.

You can use them together: Bridge Mode selects and orders the information;
Caveman compresses the wording while preserving necessary detail.

### Further reading

| Document | Purpose |
| --- | --- |
| [Design](DESIGN.md) | Principles, influences, and design decisions |
| [Contributing](CONTRIBUTING.md) | How to propose and validate changes |
| [Evaluation cases](evals/bridge-mode) | Expected behavior and regression checks |
| [Changelog](CHANGELOG.md) | Changes to the skill's behavior |
