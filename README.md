# BMX_Mod

BMX_Mod is a fork of CoDaM MiscMod, rebranded and extended for the V3NOM server community. It adds new commands, renames existing ones, and cleans up the original codebase.

Based on [MiscMod by Cato](https://cod.pm/guide/d0da8d/installing-and-configuring-codam-miscmod).

---

## HOW TO INSTALL

Edit `codam/modlist.gsc`:
```gsc
level.topText = &"<your text>";
[[ register ]]( "BMX_Mod", codam\miscmod::main );
```

The files `bmx_bans.dat` and `bmx_reports.dat` must be created in the main folder and be writeable by the server (or it will crash).

**NOTE:** Must be loaded before CoDaM_HamGoodies due to conflicting takeover (or any other mod).
This mod is only compatible with the latest [CoDExtended](https://github.com/xtnded/codextended).

---

## CONFIGURATION

Some settings support appending a postfix to the CVAR, such as:
`"scr_mm_spawnprotection_<MAP/GAMETYPE> <value>"`

See `CoDaM_MiscMod.cfg` for full CVAR documentation.

---

## BMX_BANS.DAT

Before running any of the commands below, back up your ban file:

```bash
mv bmx_bans.dat bmx_bans.backup.dat
```

### Upgrade ban file format from MiscMod 3.0.9 to BMX_Mod

```bash
awk 'BEGIN {FS="%";OFS=FS} NF==4&&$1~/^[0-9]+\./&&!ip[$1]++{print $1,$4,$2,0,0,$3}' bmx_bans.backup.dat > bmx_bans.dat
```

### Remove duplicate and invalid IPs

```bash
awk '$1~/^[0-9]+\./&&!ip[$1]++{print $0}' bmx_bans.backup.dat > bmx_bans.dat
```

---

## COMMANDS

`<num>` can be replaced with a player name and will be matched by string.

```
Command:                                    Description:                                         Permission ID:
!login <user> <pass>                        Login to access commands.                            0
!help                                       Display available commands.                          1
!version                                    Display BMX_Mod version.                             2
!name <new name>                            Change your name.                                    3
!fov <value>                                Set field of view (80-95).                           4
!rename <num> <new name>                    Rename a player.                                     5
!logout                                     Logout from session.                                 6
!say <message>                              Broadcast admin message with group prefix.           7
!saym <message>                             Print message on screen (center).                    8
!sayo <message>                             Print message in obituary.                           9
!kick <num> (reason)                        Kick a player.                                       10
!reload                                     Reload BMX_Mod config.                               11
!restart (*)                                Restart map (soft).                                  12
!end                                        End the map.                                         13
!map <mapname> (gametype)                   Change map and gametype.                             14
!status                                     List players and info.                               15
!mute <num|list>                            Mute a player.                                       16
!unmute <num>                               Unmute a player.                                     17
!warn <num> <message>                       Warn a player.                                       18
!kill <num>                                 Kill a player.                                       19
!weapon <num> <weapon>                      Give a weapon to a player.                           20
!heal <num>                                 Heal a player.                                       21
!invisible <on|off>                         Toggle invisibility.                                 22
!ban <num> <time> <reason>                  Ban a player.                                        23
!unban <ip|index>                           Unban a player.                                      24
!pm <player> <message>                      Send a private message.                              25
!re <message>                               Reply to last PM.                                    26
!who                                        Show logged in admins.                               27
!drop <num> (height)                        Drop a player.                                       28
!prone <num> (time)                         Force a player to prone.                             29
!slap <num> (damage)                        Slap a player.                                       30
!blind <num> (time)                         Blind a player.                                      31
!runover <num>                              Run over a player with a tank.                       32
!squash <num>                               Squash a player with a barge.                        33
!toilet <num> (time)                        Turn a player into a toilet.                         34
!explode <num>                              Explode a player.                                    35
!mortar <num>                               Drop mortars on a player.                            36
!matrix                                     Activate matrix mode.                                37
!burn <num>                                 Burn a player.                                       38
!cow <num>                                  BBQ a player.                                        39
!disarm <num>                               Disarm a player.                                     40
!rocket <num>                               Launch a player like a rocket.                       41
!spec <num|all>                             Move player(s) to spectator.                         42
!allies <num|all>                           Move player(s) to allies.                            43
!axis <num|all>                             Move player(s) to axis.                              44
!swapteams (*)                              Swap both teams.                                     45
!teambalance <on|off|force>                 Balance the teams.                                   46
!sniper                                     Snipers only (scoped).                               47
!allsniper                                  All snipers (scoped + non-scoped).                   48
!allwep (*)                                 All weapons.                                         49
!mg                                         Machine guns only.                                   50
!rifles <on|off|only>                       Toggle rifles.                                       51
!disableweapon <weapon> <on|off>            Disable a specific weapon.                           52
!health <off|0|1|2|3>                       Health settings.                                     53
!grenade <off|0|1|2|3|reset>               Grenade settings.                                    54
!pistols <on|off|reset>                     Pistol settings.                                     55
!1sk <on|off>                               Toggle instant kill.                                 56
!roundlength <time>                         Set round length. (sd|re)                            57
!psk <on|off>                               Toggle instant kill on pistols.                      58
!meleekill <type> (...)                     Toggle instant kill on melee.                        59
!wmap <weapon=map>                          Change CoDaM weapon map settings.                    60
!belmenu <on|off>                           Toggle BEL menu.                                     61
!report <num> <reason>                      Report a player.                                     62
!rs                                         Reset your score.                                    63
!optimize <num>                             Optimize connection settings for a player.           64
!pcvar <num> <cvar> <value>                 Set a player CVAR.                                   65
!scvar <cvar> <value>                       Set a server CVAR.                                   66
!respawn <num> <sd|dm|tdm>                  Respawn a player at a new spawnpoint.                67
!teleport <num> (<num>|<x> <y> <z>)         Teleport a player.                                   68
!freeze <on|off> <num|all>                  Freeze player(s).                                    69
!move <num> <u|d|l|r|f|b> <units>           Move a player in a direction.                        70
!bansearch <query>                          Search the banlist.                                  71
!banlist                                    List recent bans.                                    72
!reportlist                                 List recent reports.                                 73
!changename <on|off>                        Toggle player name changing.                         74
!password <password|off>                    Set or remove server password.                       75
!fps <125|250|333>                          Set your FPS.                                        76
!dfps <on|off>                              Toggle FPS counter.                                  77
!net                                        Optimize your connection settings.                   78
!lagom <on|off>                             Toggle lagometer.                                    79
!rules                                      Display server rules.                                80
!discord                                    Display Discord link.                                81
```

---

## SERVER CVARs (BMX-specific)

| CVAR | Description |
|------|-------------|
| `scr_bmx_rule1`, `scr_bmx_rule2`, ... | Server rules displayed by `!rules` |
| `scr_bmx_discord_link` | Discord link displayed by `!discord` |

---

## CHANGES FROM MISCMOD

- Renamed to **BMX_Mod v4.0.0**
- Ban/report files renamed to `bmx_bans.dat` and `bmx_reports.dat`
- Chat prefix changed to `[BMX]`
- `!spank` renamed to `!prone`
- `!endmap` renamed to `!end`
- `!namechange` renamed to `!changename`
- `!os` renamed to `!sniper`
- `!aw` renamed to `!allwep`
- `!omp` renamed to `!mg`
- `!force` split into dedicated `!spec`, `!allies`, `!axis` commands
- New commands: `!rocket`, `!allsniper`, `!disableweapon`, `!password`, `!fps`, `!dfps`, `!net`, `!lagom`, `!rules`, `!discord`
- Command IDs renumbered throughout

---

## CREDITS

- BMX_Mod fork by BO7MEDX
- Original MiscMod by Cato
- Mapvote based on DaMoLe's mapvote for CoD2
- Spawnfix based on LaZy's spawnfix for jump server
- Fun admin commands based on Cheese's and PowerServer's commands
- BEL menus based in part on code by Indy's endless menu
- `scr_mm_scoreboard_text` uses code from Defected (dftd)

---

## COMMUNITY

- **Discord:** [V3NOM Community](https://discord.gg/VwZhDcbehx)
- **Contact:** [@bo7medx](https://discord.com/users/bo7medx)
