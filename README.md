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

This repository is an [Agent Plugin](https://agent-plugins.org/plugin-authors/build-an-agent-plugin).
Installation depends on your client; the portable format does not define an
install command.

#### Claude Code

Start Claude Code in a local checkout containing the plugin manifests, then run:

```text
/plugin marketplace add .
/plugin install bridge-mode@sotayamashita-skills
```

Follow the install prompt, then start a new conversation. Invoke
`/bridge-mode:bridge-mode` and send `bridge-mode on`. Send `bridge-mode off`
to stop it. The skill retains `disable-model-invocation: true` so Claude Code
does not invoke it automatically.

Avoid loading both a standalone copy and the plugin copy in the same client.
Installation and conversational behavior have not been tested end to end.

#### Codex

Compatibility is pending: the Codex plugin validator rejects the skill's
existing `disable-model-invocation: true` setting. It is retained for Claude
Code. Codex's `agents/openai.yaml` separately sets
`allow_implicit_invocation: false` for explicit activation; this does not resolve
the plugin validation failure. The commands below have not been installation-tested.

From a local checkout containing the plugin manifests:

```bash
codex plugin marketplace add .
codex plugin add bridge-mode@sotayamashita-skills
```

Start a new conversation, invoke the installed `bridge-mode` skill, and send
`bridge-mode on`. Send `bridge-mode off` to stop it. Installing the plugin does
not configure automatic activation in every conversation.

Avoid loading both a standalone copy and the plugin copy in the same client.

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
