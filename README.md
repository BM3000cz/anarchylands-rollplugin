# RollPlugin — AnarchyLands CZ/SK

Configurable dice rolls, jackpots, automatic rolls and private item-stake duels.

**Author:** AnarchyLands CZ/SK - g0dy69  
**Public edition:** 1.2.4

## Features
- `/roll`: roll 1–100, with a configurable chance of jackpot 101.
- Configurable command rewards; defaults give vanilla items and experience points.
- Player autoroll and optional scheduled server rolls.
- Two-player duels with items from each player's main hand. The winner receives
  both stakes; a draw returns each player's own stake.
- Pending invitations expire after 60 seconds. In an active duel, missing rolls
  are generated automatically after 60 seconds, even if a participant is offline.
- Accepted duels cannot be cancelled by disconnecting. Recorded results and the
  original deadline remain; offline payouts are delivered on a later join.
- Duel rolls do not execute normal reward commands or special death effects.
- English and Czech messages, editable language files and English fallback.
- Optional Discord webhook, disabled by default.
- bStats usage statistics with local and global opt-out.

## Requirements
- **Tested platform:** Paper 26.3 with Java 25.
- **Plugin compilation target:** Java 21; the server may require a newer Java version.
- Plain Spigot and other Paper versions have not been verified for this release.
- Folia is not supported.

## Installation
1. Stop the server normally.
2. Download `RollPlugin-1.2.4.jar` from [Releases](https://github.com/BM3000cz/anarchylands-rollplugin/releases/latest)
   and place it in `plugins/`. Remove any older duplicate RollPlugin JAR.
3. Start the server. Configuration and language files are created in `plugins/RollPlugin/`.
4. Edit rewards, cooldowns and other settings in `config.yml`.
5. For Czech messages, set `language: cz` and use `/rollreload`.

Existing configuration and language files are not overwritten on startup.
Updating the JAR does not reset existing settings or custom reward commands.
Replace the JAR while the server is stopped, then restart. `/rollreload` reloads
configuration and messages; it does not load a replacement JAR.

## Commands and permissions
| Command | Permission | Purpose |
| --- | --- | --- |
| `/roll` | `roll.use` | Roll normally or submit your active duel result. |
| `/autoroll` | `roll.use` | Toggle automatic standard rolls. |
| `/rollduel <player>` | `roll.use` + `roll.duel` | Challenge a player with your main-hand stack. |
| `/rollaccept` | `roll.use` + `roll.duel` | Accept a challenge with your main-hand stake. |
| `/rolldeny` | `roll.use` | Decline a pending challenge. |
| `/rollcancel` | `roll.use` | Cancel your own unaccepted challenge. |
| `/rolladmin <1-101>` | `roll.admin` | Force your own normal or active-duel result; players only. |
| `/rollreload` | `roll.admin` | Reload configuration, messages and roll schedules. |

`roll.use` and `roll.duel` default to true. `roll.admin` defaults to operators.
Outside a duel, `/rolladmin` executes the configured rewards and enabled death
features for the forced result. During an active duel, it submits your duel roll.
Console `/roll` performs a server roll without player reward commands.
Normal-roll cooldowns survive reconnects while the server remains running;
a server restart resets their in-memory state.

Autoroll requires `roll.use` before each scheduled roll. `/rollreload` stops
autorolls when disabled and applies the configured period to existing eligible
opt-ins. Enabling the setting does not automatically opt players in.

### Duel access
Both players need **roll.use AND roll.duel** when a challenge is created and
accepted. Denying roll.duel disables new duels without affecting normal rolls or
autoroll. A player without the required permissions cannot be challenged.
If the challenger loses access before acceptance, the invitation is cancelled
without taking either stake.

With roll.use, players can still deny/cancel pending invitations after roll.duel
is removed. Already accepted duels can finish using `/roll`.

Example with LuckPerms; use your own group names and inheritance:
```text
/lp group default permission set roll.duel false
/lp group vip permission set roll.duel true
```

## Configuration and language
- [config.yml](examples/config.yml): English-commented default configuration.
- [config_cs.yml](examples/config_cs.yml): Czech-commented template with identical settings.
- [messages_en.yml](examples/messages_en.yml): English messages.
- [messages_cz.yml](examples/messages_cz.yml): Czech messages.

The plugin reads `config.yml`. To use the Czech-commented template, replace the
active config with it. Both templates contain `language: en`; set `language: cz`
(or `cs`) separately for Czech messages. Invalid language values and missing
selected-language messages fall back to English. Language is server-wide.
Message files support `&` colors and named placeholders such as `%player%` and `%roll%`.

Reward commands execute as console. Use `%player%` for the player's name and omit
the leading slash. Defaults cover results 1, 50, 99, 100 and 101 with golden apples,
ender chests, diamonds and experience points.

The optional Order 66 event kills all online players in all worlds; self-death
kills only the roller. Both are disabled by default. For these deaths, the plugin
keeps inventory and XP level and clears item/XP drops. Duel rolls never trigger
these effects. Scheduled server rolls are also disabled by default.

## Known issue: duel items after a server crash
An abrupt server or host crash during an accepted duel can lose stakes. A crash
during item delivery can also leave missing or duplicated items. Normal shutdown
has a refund routine, but the pending-refund file does not contain all active stakes.
See [Known issues](KNOWN-ISSUES.md) or [Známá omezení](KNOWN-ISSUES_cs.md).

## Usage statistics
Standard statistics include server/player counts, software versions, OS/CPU information and a random server identifier.RollPlugin includes bStats

Metrics are enabled by default. To disable them for RollPlugin, set
`metrics.enabled: false` in `config.yml` and run `/rollreload`. The shared bStats
opt-out in `plugins/bStats/config.yml` is also respected; restart after changing
that shared file.

## Support and license
Report reproducible problems through [GitHub Issues](https://github.com/BM3000cz/anarchylands-rollplugin/issues).
Include server, Java and plugin versions, reproduction steps and relevant logs.

Free to run, including on monetized servers, under [LICENSE.txt](LICENSE.txt).
Resale and false authorship are not permitted. Free unofficial modified JARs must
retain the license and original author credit, identify changes and be marked
unofficial. Source code is not distributed in this repository.
See [Third-party notices](THIRD-PARTY-NOTICES.md) for bundled components and attribution.
