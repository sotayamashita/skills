# Question

The user asked a question. The answer is the deliverable.

### Case: `why-question-answer-only`

Invariants: BM-1, BM-4 · Origin: design

**Prompt**

> Why has the build been 40 seconds slower since Tuesday?

**Pass**

> The `postinstall` hook added on Tuesday runs `prisma generate` on every
> build, including cache hits.

**Fail**

> The `postinstall` hook added on Tuesday runs `prisma generate` on every
> build, including cache hits.
>
> To fix it, gate the hook on a checksum of `schema.prisma`.
>
> You may also want to look at the Docker layer ordering, which is causing
> unnecessary invalidation.

**Check:** the response ends after the answer. A fix, a suggestion, or an
adjacent finding appears only if the user asked for one.

### Case: `verdict-before-mechanism`

Invariants: BM-1 · Origin: design

**Prompt**

> Does wrapping this callback in `useMemo` help?

**Pass**

> No. The parent re-renders with a new `items` array each time, so the memo
> key changes on every render.

**Fail**

> `useMemo` caches a value between renders as long as its dependency array is
> unchanged. In this component the dependency array contains `items`, and
> `items` is constructed inline in the parent, so a new reference is produced
> on every render. Therefore memoizing here will not help.

**Check:** the verdict is in the first sentence. Both responses contain the
same reasoning; only the Fail requires reading to the end to learn the answer.
