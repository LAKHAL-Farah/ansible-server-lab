# Phase 7 — Simulated Vault Password Leak

## What happened
Committed .vault_pass.txt to the `oops-accidental-commit` branch.

## Why "just delete the file" is not enough
Git keeps every previous version of every file in its history by default.
Even if I delete the file and commit that deletion, `git log --all --full-history`
and `git show <commit>:.vault_pass.txt` can still recover the old plaintext
password from history, forever, unless the history itself is rewritten.

## What a real remediation actually requires
1. Treat the vault password as compromised the moment it's committed —
   not "probably fine since it's a private repo."
2. Rotate every secret that vault password could decrypt — in this project,
   that means generating a new vault_db_password and re-encrypting with a
   brand new vault password, not reusing the old one.
3. If this had been pushed to a shared remote, the branch/commit would need
   history rewritten (git filter-repo or BFG Repo-Cleaner) and every clone
   of the repo would need to be told to re-fetch — deleting the branch
   locally is not sufficient once something is pushed.
4. Only after rotation is complete does deleting the branch actually matter —
   the deletion is cleanup, not the fix. The fix is that the leaked secret
   no longer has any power, whether or not it's still findable somewhere.

## What I actually did here
Deleted the throwaway branch locally, since it was never pushed anywhere.
Confirmed `main` was never affected.