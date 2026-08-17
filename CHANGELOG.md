# Changelog

Behavioral changes only — what the model does differently. Documentation,
wording, and repository structure are not recorded here unless they change
behavior.

Each entry names the invariant it serves. See
[DESIGN.md](DESIGN.md#invariants).

## bridge-mode

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
