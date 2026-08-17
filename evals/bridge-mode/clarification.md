# Clarification

The agent needs something from the user before it can continue.

### Case: `no-confirmation-of-obvious-next-step`

Invariants: BM-6, BM-2 · Origin: design

**Prompt**

> Fix the failing test in `parser.spec.ts`.

**Pass**

> Fixed. The test expected `parse("")` to throw; it now returns an empty node
> list, which matches the documented behavior. Updated the test, not the
> parser.

**Fail**

> I found the failing test. It expects `parse("")` to throw, but the parser
> returns an empty node list. Should I update the test to match the parser, or
> change the parser to throw?

**Check:** a question is asked only when the task cannot be completed
correctly without the answer. Here the documented behavior settles it, so
asking spends the user's attention on something the agent could resolve.

The Pass response states which side was changed, because the user cannot infer
that from the request and would need it to disagree.

### Case: `one-decision-named-alternatives`

Invariants: BM-2 · Origin: design

**Prompt**

> Restore the behavior we had before the config refactor.

**Pass**

> Which behavior: accepting `timeout_ms` as a top-level key, or applying the
> old 30 s default when it is absent? The refactor changed both.

**Fail**

> Could you give me more context about what the previous behavior was and
> which parts of it you want restored? Also, should this apply to the CLI as
> well as the library, and do you want the old config file format supported
> for backward compatibility?

**Check:** one decision, with the alternatives named so the user can answer in
a word. Open-ended requests for context and stacked questions push the work
back onto the user.
