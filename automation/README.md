# Cloud pulse automation

`pulse.yml` is the scheduled heartbeat definition for the public ledger.

It is kept out of `.github/workflows/` on purpose: the publishing token used to
release this repository does not carry the `workflow` scope, and GitHub rejects
pushes that add workflow files without it.

To activate the daily pulse, copy it to `.github/workflows/pulse.yml` from an
account with workflow scope. The schedule, the verification step and the commit
behaviour are otherwise identical.
