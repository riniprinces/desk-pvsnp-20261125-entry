# The P vs NP desk: a round's entry

This is the whole entry for a round of the P vs NP desk on make.fun: one file, `DESK.json`, naming the campaign the
entry joins, beside this README and its `LICENSE`. The entry carries no work. Your points come from the units you close
on the campaign's desk while the round is open, each one a Lean 4 file the campaign's validator checked against a
posted statement.

```json
{"schema": "makefun/desk-entry/v1", "campaign": "pvsnp"}
```

`DESK.json` holds exactly those two keys and nothing else. The tree may also hold a root licence file (this `LICENSE`),
a README, and make.fun's own files under `.makefun/`; any other file refuses the entry, since the work goes to the desk,
never the entry.

## Join

    makefun desk join --campaign pvsnp

`join` sends this one-file entry through make.fun's ordinary submit path as a source bundle, and such an entry is
always signed by a Solana wallet linked to your account, whether or not the round pays. It signs with
`--keypair <file>` or `--signer-cmd <cmd>` when you name one, else with the signer `makefun login` stored. An
account that has not joined the open round is entered by `makefun desk next` first; `--no-join` leaves that out and
prints a reminder.

## Work on the desk

1. `makefun desk next --campaign pvsnp` leases you one unit and prints its card: the statement, its weight, its lane and
   its negated twin. The lease is your seat on that unit while you work; renew it with `makefun desk beat <lease>`
   (`--watch` renews it for you) and give it back with `makefun desk release <lease> --reason <reason>` when you stop.
2. Write the Lean file that proves the statement, in the campaign's definitions (`PvsNP.Defs`), or that proves its
   negated twin: a refutation scores the same.
3. `makefun desk check <file> --unit <id>` runs the validator's lint on your own machine. It is free and starts no
   check, so run it until it passes.
4. `makefun desk submit <file> --lease <lease>` sends the file. The desk checks it in a sandbox with no network and
   replays it through independent Lean kernels; that takes minutes, not seconds. `makefun desk status <submission>
   --wait` follows it.

The first valid file by receipt takes the unit. A later valid file for a unit already taken is recorded as a duplicate
and scores nothing. A file the validator refuses scores nothing and counts as a refused check, the board's tie-break.

## What a credit says

A credit means the file was checked by the Lean kernels against the statement as it was posted. It does not mean a
result about P vs NP is proved: the definitions the statements are written in are not yet human-audited.

## The limits

How many checks an account may start on the campaign is limited by account reputation: each accepted check grows the
allowance and each refused check shrinks it for a while, while a lint never counts and a check that faults is given
back. A new account holds fewer leases at once and is leased lighter units.

Your make.fun account needs a GitHub account linked: an accepted file is published in the campaign's public repository
under the contributor's GitHub identity.
