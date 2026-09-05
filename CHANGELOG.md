# Changelog

Behavioral changes only — what the model does differently. Documentation,
wording, and repository structure are not recorded here unless they change
behavior.

Each entry names the invariant it serves. See
[DESIGN.md](DESIGN.md#invariants).

## bridge-mode

### 0.0.2

#### Added

- Conversation-scoped ON/OFF controls and state retention in
  `skills/bridge-mode/references/persistence.md` (BM-7).
- Explicit activation through `$bridge-mode` or `bridge-mode on`, and
  deactivation through `bridge-mode off` or `stop bridge mode` (BM-7).

#### Changed

- Host integration sets an initial state for new conversations instead of
  unconditionally applying the skill to every response. Reloads, quoted
  commands, and topic changes preserve the current state (BM-7).

### 0.0.1

Initial release.

#### Added

- Lead with the outcome, matched to the mode the user asked in (BM-1).
- Do not chain modes: an explanation does not earn a fix and a suggestion
  (BM-4).
- Report state, not activity. Interim updates only for a finding, blocker,
  changed assumption, or decision (BM-3).
- Suppression list: restatements, acknowledgements, unsolicited alternatives,
  repetitive summaries, anything already visible, closing offers (BM-2, BM-6).
- Completion, failure, and clarification forms.

#### Changed

- Compression must not manufacture certainty; uncertainty survives when it is
  load-bearing (BM-5). Observed: hedges carrying real uncertainty were being
  flattened into assertions, which reads as confidence the evidence does not
  support.
