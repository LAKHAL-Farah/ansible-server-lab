# Phase 2 — Fleet Drift Investigation

## Commands used
- `ansible role_web -m stat -a "path=/etc/manual-change-nobody-documented.flag"`
- `ansible role_web -m shell -a "dpkg -l | grep tree"`

## Finding
web02 has an undocumented manual change: a flag file and the `tree` package,
neither of which exist on web01. This simulates untracked manual drift on
a production host.

## Why this matters
This is exactly the kind of drift Ansible's baseline role (Phase 3) is meant
to prevent from mattering long-term — but note that Ansible only *fixes*
drift when a playbook actually runs against the host. It doesn't
continuously detect this on its own (see Section 1.5 of the lesson guide —
agentless + push means no automatic self-healing).