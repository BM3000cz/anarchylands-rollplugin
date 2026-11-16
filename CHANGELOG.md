# Changelog

## 1.2.4
- Accepted duels retain results and their original timeout across disconnects.
- Missing rolls can finish while participants are offline; payouts await their return.
- Normal-roll cooldowns are preserved across reconnects.
- Autoroll stops before another reward if roll.use is removed.
- Reload cancels disabled autorolls and reapplies the period to existing eligible opt-ins.
- Reenabling autoroll does not enable it for players who had not opted in.
