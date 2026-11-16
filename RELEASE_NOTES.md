# RollPlugin 1.2.4

- Accepted duels keep recorded rolls and their original deadline after disconnects.
- Missing rolls are generated at timeout, including for offline participants.
- Offline payouts are queued for the player's return.
- Normal-roll cooldowns survive reconnects while the server remains running.
- Autoroll checks roll.use before every scheduled reward.
- Reload stops disabled autorolls and reapplies the configured period to existing
  eligible opt-ins without enabling autoroll for other players.

## Known issue
An abrupt server or host crash during a duel can lose active stakes. A crash during
item delivery may also cause missing or duplicated items after restart.
[Details](https://github.com/BM3000cz/anarchylands-rollplugin/blob/public/KNOWN-ISSUES.md)
