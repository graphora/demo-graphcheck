# demo-graphcheck

A minimal public example showing GraphCheck running in CI against a demo graph — one green
run, and one caught failure — so you can see what wiring GraphCheck into your own pipeline
looks like before you try it.

## What this is

This repo uses [`graphora/graphcheck-action@v1`](https://github.com/graphora/graphcheck-action)
in a GitHub Actions workflow (`.github/workflows/graphcheck.yml`) that runs on every pull
request. It stands up a disposable Neo4j service, seeds it with the
[fraud-ring fixture](https://github.com/graphora/graphcheck-fraud-ring-fixture) (a graph with
known, documented conformance issues), and runs the `fraud-ring-conformance` check suite
against it.

## Fork or copy this to try it on your own graph

1. Fork or copy this repo.
2. Replace `checks/fraud-ring-conformance.yml` with your own check suite. See the
   [check reference](https://github.com/graphora/graphcheck/blob/development/docs/check-reference.md)
   for the available check types.
3. Point `profiles.yml` at your own Neo4j instance:
```console
   graphcheck init
```
   Then edit the generated `profiles.yml` to match your database's URI, user, and either an
   inline `password` (fine for local testing) or `password_env` (recommended for CI — set the
   matching value as a GitHub Actions secret).
4. Update `.github/workflows/graphcheck.yml` to seed or connect to your own graph instead of
   the fraud-ring fixture.

## Learn more

See the [GraphCheck user guide](https://github.com/graphora/graphcheck/blob/development/docs/user-guide.md)
for full setup, credential, and authoring instructions.