# Index

## `bridge-mode`

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

### References

- [Tea, Earl Grey, Hot: Designing Speech Interactions from the Imagined Ideal of Star Trek](https://dl.acm.org/doi/fullHtml/10.1145/3411764.3445640)
- [github.com/ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd/tree/main/skills/i-have-adhd)
- [github.com/alexgreensh/attention-span](https://github.com/alexgreensh/attention-span/tree/main)
- [github.com/humanlayer/skills/show-me](https://github.com/humanlayer/skills/tree/main/plugins/show-me/skills/show-me)

---
