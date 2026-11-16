# Known issue — RollPlugin 1.2.4

## Duel items after an abrupt server crash
When a duel is accepted, both stakes are removed from the players and held in
memory until the duel ends. An abrupt server/JVM crash, forced process termination
or host failure during this time can cause both stakes to be lost.

If a crash occurs during item delivery or player-data saving, items may also be
missing or duplicated after restart.

During a normal stop/restart, the plugin attempts to return active stakes. Refunds
that cannot be delivered immediately are stored in `pending-duel-refunds.yml` and
retried when the player joins with inventory space. This file does not contain all
active-duel stakes. Restarting or using `/rollreload` cannot recreate an unsaved stake.

Pending invitations do not take items until accepted.
