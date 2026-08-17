# bridge-mode evals

Behavioral regression cases. Each case pins one property of the skill so a
future change can be checked instead of debated.

There is no runner yet. A case is checked by giving the prompt to a session
with `bridge-mode` active and comparing the response against the **Check**
line — not against the sample Pass text, which is one acceptable answer among
many.

## Files

| File | Covers |
| --- | --- |
| [question.md](question.md) | The user asked a question |
| [command.md](command.md) | The user asked for work to be done |
| [decision.md](decision.md) | The user asked which option to take |
| [explanation.md](explanation.md) | The user asked to be taught something |
| [progress.md](progress.md) | Communication during a long task |
| [clarification.md](clarification.md) | The agent needs something from the user |
| [completion.md](completion.md) | The task finished |
| [failure.md](failure.md) | The task could not finish |

## Case format

```md
### Case: `stable-id`

Invariants: BM-1, BM-4 · Origin: design

**Prompt**
...

**Pass**
...

**Fail**
...

**Check:** what mechanically separates Pass from Fail.
```

`Invariants` cites [DESIGN.md](../../DESIGN.md#invariants) by ID, never by
quoting `SKILL.md`. Rewording the skill therefore does not invalidate a case;
only retiring an invariant does.

`Origin` is `design` when the case was derived from an invariant, and
`observed` when it came from a real failure. Observed cases carry more weight:
they are the ones that prove the skill was wrong at least once.

`Check` exists so a case can be judged without taste. If a case cannot be
reduced to a mechanical check, it is a preference and does not belong here.

## Over-compression is a failure too

A skill that shortens output invites the opposite failure: dropping detail the
user needed. Cases that guard this direction are as load-bearing as the ones
guarding verbosity — see `explain-request-permits-length`,
`interim-update-for-changed-assumption`, and `unknown-cause-stays-unknown`.

## Adding a case

See [CONTRIBUTING.md](../../CONTRIBUTING.md). A case is added *before* the
change it justifies, and must fail against the current `SKILL.md`.
