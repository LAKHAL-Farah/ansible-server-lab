# Phase 11 — Drift Detection Exercise

## What I did
Manually edited /etc/nginx/sites-available/app.conf on web01 twice, bypassing
Ansible entirely. First time, I ran the normal site.yml playbook and watched
it silently overwrite my manual change back to the git-defined state. Second
time, I ran drift_check.yml with --check --diff instead, and it reported the
exact drift without touching the file.

## Why this matters for agent vs agentless, push vs pull
[Write 4-6 sentences here explaining, in your own words:
 - why nothing detected the Step 3 drift on its own
 - what a Puppet or Chef agent would have done differently, and roughly when
 - why Ansible's agentless + push design trades away that automatic
   self-healing on purpose, and what it gains in exchange
 - what you would actually add to THIS project to close that gap for real]