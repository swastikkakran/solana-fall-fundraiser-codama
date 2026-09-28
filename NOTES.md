# NOTES - Solana Fall Fundraiser Codama

## versions

- anchor-cli: 1.1.2
- node: v24.20.0
- @codama/cli: 1.6.3


## TODO 3

`contribute` seeds the fundraiser PDA on ["fundraiser", fundraiser.maker]. The
second seed is a field stored inside the fundraiser account itself, so a finder
would need the account's data to compute the account's address. That is
circular, so the caller must pass `fundraiser`. In `initialize` the same seed is
the `maker` account, which the caller already has, so `fundraiser` is optional
there. `contributorAccount` and `contributorAta` are optional because all of
their seeds (the fundraiser address, the contributor, the mint) are available
from inputs the caller already provides.

`vault` is seeded by `fundraiser.mint_to_raise` — again a field inside the on-chain Fundraiser account.
Same reason: Codama can only resolve seeds that come from other instruction accounts or constants, not
from fields inside accounts that require a network fetch. So `vault` must also be passed explicitly.

