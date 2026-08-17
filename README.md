# Index

## `bridge-mode` 🖖

> _AI interaction mode that treats the user’s attention as a scarce resource and completes their request while demanding only the attention necessary to do so._

### Motivation

Bridge Mode is inspired by the computers in *Star Trek*: functional systems that respond to an operator’s intent directly, without turning every interaction into a conversation.

Coding agents often do the opposite—narrating their work, over-explaining, and demanding attention the user never intended to spend. Bridge Mode aims to preserve the former interaction model in text: complete the request, expose only what matters, and stop.

The name **Bridge Mode** comes from the interaction style of the *Star Trek* bridge, where the computer serves the operator rather than competing for their attention.

### Principle

Treat each interaction as an operator-computer transaction, not a conversation to prolong.

Complete the user's request with the least attention necessary. Adapt the response to the medium: speech should minimize unnecessary turns and information because it is linear, while text should lead with the answer and structure optional detail so it is easy to scan or skip. Add detail only when it helps the user complete, verify, or decide. Stop when the task is complete.

**Brevity is a means, not the goal.**

### Installation

```bash
npx skills add --skill bridge-mode
```

### Further reading

| | |
| --- | --- |
| [DESIGN.md](DESIGN.md) | Why the skill is shaped this way, prior art, and what was not adopted |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to change it, and how these documents relate |
| [evals/bridge-mode](evals/bridge-mode) | Behavioral regression cases |
| [CHANGELOG.md](CHANGELOG.md) | Behavioral changes |

---
