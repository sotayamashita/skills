# Command

The user asked for work to be done. The result of the work is the deliverable.

### Case: `result-not-plan`

Invariants: BM-1, BM-3 · Origin: design

**Prompt**

> Rename `fetchUser` to `loadUser` across the repo.

**Pass**

> Renamed. 14 call sites in 9 files. `fetchUserLegacy` in `api/v1/` left
> untouched — different function.

**Fail**

> I'll start by searching for all occurrences of `fetchUser` across the
> codebase, then update each call site and check whether any tests reference
> the old name.

**Check:** the response opens with the state after the work, not with a
statement of intent. The exception in Pass is included because the user cannot
see it and might otherwise assume the rename was complete.

### Case: `no-appended-improvements`

Invariants: BM-6, BM-2 · Origin: design

**Prompt**

> Add a `--dry-run` flag to the sync command.

**Pass**

> Added. `--dry-run` prints the planned writes and exits before touching the
> database.

**Fail**

> Added. `--dry-run` prints the planned writes and exits before touching the
> database.
>
> While I was in there, I noticed the command has no `--verbose` flag and the
> argument parsing is hand-rolled — switching to `commander` would make this
> kind of change easier in future. Want me to do that?

**Check:** the response stops when the request is satisfied. Unrelated
observations and offers of further work are absent.

### Case: `activation-persists-and-switches`

Invariants: BM-7 · Origin: design

**Prompt sequence**

Run these turns in one conversation. Ask whether Bridge Mode is active after
each step; check the stated state, not how terse the response looks.

| Step | User instruction or host event | Expected state |
| --- | --- | --- |
| 1 | New conversation with host default ON | ON |
| 2 | Explain database connection pooling. | ON |
| 3 | Now discuss CSS layout. | ON |
| 4 | bridge-mode off | OFF |
| 5 | Reload the skill and the host instructions for the same conversation. | OFF |
| 6 | Continue the CSS discussion. | OFF |
| 7 | bridge-mode on | ON |
| 8 | stop bridge mode | OFF |
| 9 | Use $bridge-mode for the next answer. | ON |
| 10 | stop bridge mode | OFF |
| 11 | Resume the same conversation from a summary that records OFF. | OFF |
| 12 | Start a new conversation with host default ON. | ON |

**Pass:** every state matches the table. OFF suspends Bridge Mode but retains
the host's language and execution constraints.

**Fail:** OFF is lost on reload, a topic change resets the state, or OFF also
disables unrelated instructions.

**Check:** explicit switches determine the state until the next switch or
new conversation. Check behavior across turns, not only the switch response.

### Case: `inspection-does-not-switch`

Invariants: BM-7 · Origin: design

**Prompt sequence**

Start without a host default or an explicit activation. Load the skill only
to review its instructions, then ask whether Bridge Mode is active.

1. Explain what `bridge-mode on` and `$bridge-mode` mean without applying them.
2. Translate the sentence "bridge-mode on" into Japanese.
3. bridge-mode on
4. Review the command `bridge-mode off` without executing it.
5. normal mode
6. stop bridge mode

**Pass:** initial state OFF, then OFF, OFF, ON, ON, ON, OFF. Other active
skills can handle `normal mode` independently.

**Fail:** merely reading the skill or discussing its commands changes state.

**Check:** distinguish a user instruction to switch from quoted text, file
contents, and discussion. Bridge Mode does not claim generic reset phrases.

**Baseline inspection:** version 0.0.1 has no persistence or switching rules.
Its host example applies Bridge Mode to every response, without an OFF
exception. These cases define missing behavior; no pre-change model run has
been recorded.
