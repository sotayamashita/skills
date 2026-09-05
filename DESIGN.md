# Design

## Bridge Mode

### Problem

Coding agents often consume more user attention than the task requires:
they narrate routine work, over-explain, surface unsolicited alternatives,
and make the user search through text for the actual outcome.

### Design Goal

Complete the user's request while demanding only the attention necessary to do so.

User attention is treated as a scarce resource.

Brevity is not the objective. It is a consequence of removing information
that is not load-bearing.

### Interaction Model

Bridge Mode is inspired by the ship's computer in Star Trek.

The useful abstraction is not "speak like Star Trek." It is:

> Treat interaction as an operator-computer transaction, not a conversation to sustain.

The computer answers, acts, requests missing information when blocked,
and stops when the transaction is complete.

### Text vs. Speech

The Star Trek inspiration comes primarily from voice interaction, but the
principle is medium-independent.

Speech is linear, so unnecessary information and turns are expensive.

Text is scannable. Bridge Mode therefore preserves the same interaction
economy while allowing secondary information when it is structured so the
user can easily skip it.

This leads to:

> Outcome first; supporting detail after it.

### Load-bearing Information

A detail is load-bearing when it helps the user:

1. complete the task,
2. verify the result, or
3. decide what happens next.

This is the primary criterion for deciding what survives compression.

Compression must never manufacture certainty.

### Foundations

Bridge Mode incorporates ideas from:

#### Grice's Maxims
Necessary, truthful, relevant, and clear information.

Bridge Mode:
- load-bearing information
- suppress unrelated information
- preserve uncertainty

#### BLUF / Inverted Pyramid
Put the conclusion first.

Bridge Mode:
- outcome first
- supporting detail afterward

#### Progressive Disclosure
Expose primary information first and make secondary information optional.

Bridge Mode:
- text may retain structured secondary detail when it is easy to skip

#### Audience / Task-oriented Writing
Write what the reader needs to perform the task, not everything the writer knows.

Bridge Mode:
- complete / verify / decide

#### Diátaxis
Different information needs should not be mixed unnecessarily.

Bridge Mode:
- answer in the requested mode
- do not chain explanation → fix → suggestion unless requested

### Agent-specific Principle

Coding agents create a distinctive source of noise by narrating their own work.

Therefore:

> Report state, not activity.

Intermediate communication is justified only when a finding, blocker,
changed assumption, or decision is useful to the user before completion.

### Non-goals

Bridge Mode is not:

- a "short answer" mode
- a fixed word-count constraint
- a prohibition on detailed answers
- a prohibition on uncertainty
- a Star Trek role-playing style
- an excuse to omit evidence required for trust

### Invariants

Changes to SKILL.md must preserve these properties.

IDs are stable: they are never renumbered or reused, and an obsolete
invariant is struck through rather than deleted. Evals cite the ID, not the
wording of SKILL.md, so rephrasing the skill does not invalidate a test.

| ID | Invariant |
| --- | --- |
| BM-1 | Outcome precedes supporting detail. |
| BM-2 | Only load-bearing information is included by default. |
| BM-3 | State is preferred over activity narration. |
| BM-4 | Response modes are not chained unnecessarily. |
| BM-5 | Uncertainty is not removed by compression. |
| BM-6 | The interaction stops when the user's request is satisfied. |
| BM-7 | Activation state persists within a conversation until an explicit Bridge Mode switch; host defaults apply only when a new conversation starts. |

### Activation and persistence

The user requested an explicit ON/OFF switch that persists across turns.
Previously, the skill specified no activation lifetime, while the host's
instruction to apply it to every response left no explicit OFF behavior.
This is a requested capability, not a measured behavioral regression.

The host chooses the initial state. Bridge Mode owns subsequent switches.
Reading the skill is not itself activation: inspection, automatic reloads,
and quoted commands must not undo an explicit OFF. Resuming a conversation
preserves its state; a genuinely new conversation uses the host default.

Persistence is an instruction carried in conversation context, not a stored
setting or a hook. Explicit OFF suspends Bridge Mode's response rules, while
other instructions remain in force. State controls still work while OFF.
The generic phrase `normal mode` is excluded because other skills use it.
These rules serve BM-7; BM-1 through BM-6 apply while Bridge Mode is ON.

### References

What was taken from each source, and what was deliberately left behind.

#### [Tea, Earl Grey, Hot: Designing Speech Interactions from the Imagined Ideal of Star Trek](https://dl.acm.org/doi/fullHtml/10.1145/3411764.3445640)

Taken: the operator-computer transaction as the interaction model, separated
from the surface style it is usually imitated for.

Not taken: the speech-medium assumptions. The paper's economy comes from
speech being linear and un-skimmable. Text is scannable, so Bridge Mode keeps
the economy of turns while permitting structured secondary detail the user can
skip.

#### [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd/tree/main/skills/i-have-adhd)

Taken: leading with the actionable outcome; the suppression list (preamble,
recap, closing pleasantries); matter-of-fact error reporting; and the rule
that deleting a hedge which carries real uncertainty manufactures confidence
(BM-5).

Not taken: the machinery serving working memory — numbered steps, restating
state every turn, specific time estimates, capping lists at five, making wins
visible. These are correct for their reader model but they *add* text on
purpose. Bridge Mode's criterion is load-bearing information (BM-2), which
does not privilege any particular reader.

#### [alexgreensh/attention-span](https://github.com/alexgreensh/attention-span)

Taken: answer-first treated as a measurable property rather than a matter of
taste, and the separation of *delivery changed* from *work unchanged*. Its
benchmark harness is the direct reason this repository has `evals/`.

Not taken: the prescribed visual surface (`→` markers, heavy bold), the
plain-English mandate that defines jargon on sight, and the output-style
delivery mechanism. A fixed visual format is a constraint on shape, not on
information, and would collide with BM-2 when the shape is not load-bearing.

#### [humanlayer/skills — show-me](https://github.com/humanlayer/skills/tree/main/plugins/show-me/skills/show-me)

Taken: the observation that a tree, a diff, or a diagram can carry information
at lower cost than prose, which is what makes "supporting detail after the
outcome" affordable in text.

Not taken: the artifact repertoire itself. `show-me` is a complementary mode
the user invokes; Bridge Mode does not mandate diagrams, because an unrequested
diagram is unrequested output (BM-2).

---
