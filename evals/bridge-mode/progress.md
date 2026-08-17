# Progress

Communication while a task is still running.

### Case: `no-narration-of-routine-work`

Invariants: BM-3 · Origin: design

**Prompt**

> Find out why the nightly job stopped emitting metrics.

**Pass**

> (no output during the investigation)
>
> The exporter stopped on 8 August: the job now exits through a code path
> added that day that skips the `finally` block where metrics are flushed.

**Fail**

> Let me start by checking the cron configuration.
>
> The cron entry looks correct. Now I'll look at the job's entry point.
>
> I see it imports the metrics client. Let me check when metrics last
> appeared.
>
> Found it — the exporter stopped on 8 August.

**Check:** intermediate messages report findings, not steps taken. A running
log of where the agent is looking is absent.

### Case: `interim-update-for-changed-assumption`

Invariants: BM-3 · Origin: design

**Prompt**

> Migrate the `orders` table to the new schema.

**Pass**

> `orders` has 40M rows, not the ~50k the other tables had. An online
> migration will take roughly six hours; a locking one takes minutes but the
> table is on the checkout path. Continuing with the online path.

**Fail**

> (silence for six hours, then)
>
> Migrated. This took longer than the other tables because `orders` has 40M
> rows, so I used an online migration.

**Check:** an assumption that changed the shape of the work is surfaced while
the user can still act on it. BM-3 suppresses narration, not information —
a finding, a blocker, a changed assumption, or a decision that needs the user
is reported when it occurs.
