# Explanation

The user asked to be taught something. The explanation is the deliverable.

### Case: `explanation-not-followed-by-fix`

Invariants: BM-4 · Origin: design

**Prompt**

> Explain how the retry backoff works in `client.ts`.

**Pass**

> Each failure doubles the delay from a 200 ms base, capped at 30 s, with up
> to 25% random jitter subtracted. The counter resets on any 2xx, so an
> intermittent failure never accumulates toward the cap.

**Fail**

> Each failure doubles the delay from a 200 ms base, capped at 30 s, with up
> to 25% random jitter subtracted. The counter resets on any 2xx, so an
> intermittent failure never accumulates toward the cap.
>
> This is a problem: resetting on any 2xx means a flapping endpoint keeps
> retrying at the base delay forever. I'd change the reset to require two
> consecutive successes. Want me to make that change?

**Check:** an explanation request produces an explanation. A defect noticed
while explaining is not silently converted into a fix proposal — the user
asked to understand the code, not to change it.

### Case: `explain-request-permits-length`

Invariants: BM-2 · Origin: design

**Prompt**

> Walk me through how session cache invalidation works end to end.

**Pass**

> A full account: the write path, the two invalidation triggers, the
> cross-region propagation delay, and the one case where a stale read is
> possible. Structured with headings so the reader can navigate back, and as
> long as the mechanism requires.

**Fail**

> Sessions are cached in Redis and invalidated on logout and on password
> change.

**Check:** length is set by what the reader needs to understand the mechanism,
not by a preference for short answers. The Fail response is compressed past
the point where the user could complete, verify, or decide anything —
brevity is a by-product, never the target.

This case exists because a skill that shortens output invites over-compression
as its characteristic failure. See the non-goals in
[DESIGN.md](../../DESIGN.md).
