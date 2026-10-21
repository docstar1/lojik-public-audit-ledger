# Cloud pulse automation

`pulse.yml` is the scheduled heartbeat definition for the public ledger.

It is kept out of `.github/workflows/` on purpose: the publishing token used to
release this repository does not carry the `workflow` scope, and GitHub rejects
pushes that add workflow files without it.

To activate the daily pulse, copy it to `.github/workflows/pulse.yml` from an
account with workflow scope (or run `activate_cloud_actions.bat` in the private
repository, which refreshes the token scope and promotes the file for you).
The schedule, the verification step and the commit behaviour are otherwise
identical. The pulse verifies the chain with an inline, dependency-free
computation, so no script file has to be published for it to run.
