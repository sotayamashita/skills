# Contributing

## Changing a skill

A skill file is not a place to collect good ideas. Every rule in a `SKILL.md`
costs the model attention at runtime and costs a reader attention forever, so
the entry point for a change is fixed.

```text
0. Start from an observed failure — never from an idea
   │
1. Can an existing invariant explain it?
   ├─ Yes ──────────────────────────────────┐
   └─ No → 2. Add the invariant to DESIGN.md │
                                             │
3. Add an eval case that cites the invariant ◄┘
   │  It must fail before the change.
   │
4. Change SKILL.md
   │
5. Record it in CHANGELOG.md if behavior changed
```

### 0. Start from an observed failure

Write down what actually happened: the prompt, the response, and what the
response cost the user. A change proposed without this step is a preference.

Preferences are not disqualified — but they are argued at step 2, against the
existing invariants, in the open.

### 1. Check the invariants

The invariants are in [DESIGN.md](DESIGN.md#invariants). Most failures are an
existing invariant that the skill does not yet enforce clearly enough. Those
are cheap: they need no new principle, only a sharper rule.

### 2. Add the invariant first, if there is no such thing

A new invariant changes what the skill is for. It goes into DESIGN.md with the
failure that motivated it, before any rule is written. IDs are append-only:
never renumber, never reuse. An invariant that no longer holds is struck
through with a note, not deleted, because evals still cite it.

If a proposed change contradicts an existing invariant, that is the whole
discussion. Resolve it in DESIGN.md or drop the change.

### 3. Add the eval first

The case goes in `evals/<skill>/` and cites invariant IDs. Confirm it fails
against the current `SKILL.md` before changing anything. An eval written after
the fix tests the fix, not the behavior.

Cases cite invariant IDs rather than quoting SKILL.md, so rewording the skill
does not invalidate them.

### 4. Change SKILL.md

Keep it the minimum behavioral specification. Rationale, prior art, and
history belong in DESIGN.md, CHANGELOG.md, and `evals/` respectively — none of
them belong in the file the model reads.

Prefer sharpening an existing rule to adding one. If a new rule makes another
redundant, delete the other in the same change.

### 5. Record behavioral changes

Anything that changes what the model does goes in
[CHANGELOG.md](CHANGELOG.md), with the invariant it serves. Typo fixes,
README edits, and rewording that leaves behavior intact do not.

## Repository layout

Three layers. Each answers a different question, and mixing them is what makes
a skill file grow until nobody can tell which rules still earn their place.

```text
 README.md · DESIGN.md
     │   why?
     │   Design rationale, background, prior art, and the reasons
     │   something was adopted or rejected.
     │   Read by whoever changes the skill.
     ▼
 skills/<skill>/SKILL.md
     │   what?
     │   The minimum behavioral specification, as it stands now.
     │   Read by the model, at runtime.
     ▼
 evals/<skill>/
         does it work?
         Concrete cases, regression tests, recorded failures.
         Read by a reviewer.
```

The arrows are also the direction of justification: a rule in `SKILL.md` must
trace to an invariant in `DESIGN.md`, and an eval case cites the invariant it
pins rather than quoting the skill. Nothing is justified by the layer below it.

Two files sit outside the layers. `CONTRIBUTING.md` — this file — fixes the
order changes are made in. `CHANGELOG.md` records what changed behaviorally,
for someone whose results shifted between versions.

The repository root is the plugin package. `plugin.json` defines its portable
identity. `.codex-plugin/plugin.json` and `.claude-plugin/plugin.json` provide
client compatibility. Their catalogs are `.agents/plugins/marketplace.json`
and `.claude-plugin/marketplace.json`, respectively. All manifests use the same
`skills/` directory. Keep their shared metadata in sync.

`skills/<skill>/` remains the distribution unit for the skill-only fallback.
Design documents, evals, and history are maintainer documentation, not runtime
instructions. Package references must resolve inside the repository.

For packaging changes, validate all manifests, check each catalog's plugin
name and source path, and confirm that skill references remain inside the
package. Test installation and ON/OFF behavior in a fresh client conversation
before claiming client compatibility or removing the fallback. Packaging-only
changes do not require behavioral eval changes.

Validate the Claude Code package from the repository root:

```bash
claude plugin validate .claude-plugin/plugin.json
claude plugin validate .claude-plugin/marketplace.json
```

DESIGN.md holds one `##` section per skill. Split it into `design/<skill>.md`
when the third skill is added, not before.

## Commits

Conventional Commits, with the skill name as the scope:

```text
feat(bridge-mode): ...
docs(bridge-mode): ...
test(bridge-mode): ...   # eval cases
```

English for commit messages, code, and identifiers.
