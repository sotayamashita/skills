# Index

[![skills.sh](https://skills.sh/b/sotayamashita/skills)](https://skills.sh/sotayamashita/skills)

## `bridge-mode` 🖖

> _AI interaction mode that treats the user’s attention as a scarce resource and completes their request while demanding only the attention necessary to do so._

### Motivation

Coding agents narrate their work, over-explain, and demand attention the user never intended to spend. The *Star Trek* bridge computer does the opposite: it answers the operator's intent and stops.

### Principle

**Brevity is a means, not the goal.**

Treat each interaction as an operator-computer transaction, not a conversation to prolong. Lead with the outcome, include detail only when it helps the user complete, verify, or decide, and stop there.

### Installation

```bash
npx skills add sotayamashita/skills --skill bridge-mode
```

### Further reading

| | |
| --- | --- |
| [DESIGN.md](DESIGN.md) | Why the skill is shaped this way, prior art, and what was not adopted |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to change it, and how these documents relate |
| [evals/bridge-mode](evals/bridge-mode) | Behavioral regression cases |
| [CHANGELOG.md](CHANGELOG.md) | Behavioral changes |
