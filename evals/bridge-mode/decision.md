# Decision

The user asked which option to take. The recommendation is the deliverable.

### Case: `recommendation-before-comparison`

Invariants: BM-1 · Origin: design

**Prompt**

> Should the rate limiter live in the gateway or in each service?

**Pass**

> Gateway. The limit is per-tenant, and only the gateway sees every request
> from a tenant.

**Fail**

> Both placements are viable. In the gateway you get a single enforcement
> point and one place to configure limits, but you lose per-endpoint
> granularity. Per-service gives you that granularity and keeps services
> independently deployable, at the cost of duplicated configuration and no
> global view of a tenant's traffic. Given that your limit is per-tenant, the
> gateway is probably the better fit.

**Check:** the recommendation is the first word. The reason given is the one
that drives the decision, not a survey of considerations.

### Case: `tradeoffs-only-when-decision-changing`

Invariants: BM-2 · Origin: design

**Prompt**

> Postgres or SQLite for this CLI's local index?

**Pass**

> SQLite. The index is per-machine and never shared, so a server process buys
> nothing.
>
> This assumes the index stays under a few hundred MB. Past that, rebuild time
> becomes the constraint and Postgres is worth revisiting.

**Fail**

> SQLite. The index is per-machine and never shared, so a server process buys
> nothing.
>
> Postgres has richer types, better concurrent write handling, a mature
> extension ecosystem, and stronger tooling for schema migrations. SQLite is
> a single file, has no server to run, ships with most language runtimes, and
> is faster for single-process reads.

**Check:** supporting detail after the recommendation is limited to what could
change the decision. The Pass caveat names a condition that would flip the
answer; the Fail paragraph would not change anything.
