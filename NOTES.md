
## Versions

- anchor-cli 1.1.2
- solana-cli 3.1.10
- node v24.10.0
- @codama/cli 1.6.3
- @solana/kit 8.3.0

## TODO 3
`contribute` still requires `fundraiser` and `vault`. It fills in `contributorAccount`, `contributorAta`, `tokenProgram`, and `systemProgram`.

`fundraiser` is seeded with `fundraiser.maker`, a field inside the account being derived, so the finder would need the address to compute the address. `initialize` and `refund` seed the same PDA with `maker.key()`, and `maker` is an account the caller already passes, so there `fundraiser` is optional. `vault` has the same problem: its ATA mint seed is `fundraiser.mint_to_raise`, not the `mint_to_raise` account. `contributorAccount` and `contributorAta` only seed off accounts already in the instruction (`fundraiser`, `contributor`, `mint_to_raise`), which is why those two can be derived. Leaving `maker` out of `contribute` saves an account in the transaction and makes every client pass the PDA instead.

## Bonus
Attempted

## One thing that surprise me
Using CODAMA is much easier to interact with Programs. 