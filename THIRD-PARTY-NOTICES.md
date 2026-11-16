# Third-party notices

The distributed RollPlugin JAR contains the project's own plugin classes,
configuration, translations, license, Maven metadata and the bStats library.
The server APIs and Minecraft are not bundled.

## bStats

`org.bstats:bstats-bukkit:3.2.1` and its matching `bstats-base` dependency are
bundled and relocated to `cz.beatmachine.roll.lib.bstats` using Maven Shade.
Copyright (c) 2021 Bastian Oppermann; licensed under the MIT License. The full
upstream notice is included at `META-INF/licenses/bstats-MIT.txt` in the JAR
and in this documentation's `licenses/bstats-MIT.txt`. The RollPlugin custom
license does not replace the MIT rights for these third-party components.
Source: https://github.com/Bastian/bstats-metrics

## Server APIs

Paper/Bukkit API is a provided compile-time dependency and must be supplied by
an independently installed server. Paper inherits licenses from its upstream
projects, including GPL-3.0 and permissively licensed contributions:
https://github.com/PaperMC/Paper/blob/main/LICENSE.md

The RollPlugin license covers only copyrightable materials owned by its author;
it neither changes upstream licenses nor determines whether a particular
integration is a derivative work. The RollPlugin license does not cover an entire server bundle.

Minecraft is a trademark of Mojang/Microsoft. This project is not affiliated
with or endorsed by Mojang/Microsoft, PaperMC or SpigotMC.
