

# 💀 JeyukDeathPoints

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-red?style=for-the-badge)
![Paper](https://img.shields.io/badge/Paper-1.21.1-orange?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0wIDE4Yy00LjQxIDAtOC0zLjU5LTgtOHMzLjU5LTggOC04IDggMy41OSA4IDgtMy41OSA4LTggOHoiLz48L3N2Zz4=)
![Java](https://img.shields.io/badge/Java-21-blue?style=for-the-badge&logo=openjdk)
![Vault](https://img.shields.io/badge/Requires-Vault-yellow?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)

**A fully customizable death penalty plugin for Paper servers.**  
Deduct a percentage of a player's money on death — with on-screen titles, chat messages, per-world control, and live admin commands.

[Features](#-features) • [Installation](#-installation) • [Commands](#-commands) • [Permissions](#-permissions) • [Configuration](#-configuration) • [Placeholders](#-placeholders)

</div>

---

## ✨ Features

- 💸 **Percentage-based money deduction** on death — fully configurable
- 🌍 **Per-world control** — whitelist exactly which worlds apply the penalty
- ⚔️ **PvP / PvE toggle** — apply the penalty only on player kills, mob deaths, or both
- 📺 **On-screen title** — big red `-$amount` flash when the player dies
- 💬 **Chat message** — detailed breakdown of amount lost, percentage, and remaining balance
- 🛡️ **Bypass permission** — certain players (VIP, staff) can be exempt
- 💰 **Balance floor** — prevent players from going below a minimum balance
- 🔧 **Live admin commands** — change percent, toggle worlds, enable/disable — all saved to `config.yml` instantly
- 📋 **Balance checker** — preview exactly how much a player would lose
- 📡 **Console logging** — every deduction is logged with full details
- 🔌 **Vault compatible** — works with EssentialsX, CMI, and any Vault economy


<img width="1600" height="720" alt="Screenshot_20260424_185728_MojoLauncher (Minecraft Java Edition for Android)" src="https://github.com/user-attachments/assets/f96e2e32-0f74-4be9-bf32-0e63ef4955d7" />

---

## 📋 Requirements

| Requirement | Version |
|---|---|
| Server software | Paper (or forks) |
| Minecraft version | 1.21.1+ |
| Java | 21+ |
| [Vault](https://www.spigotmc.org/resources/vault.34315/) | Any recent version |
| Economy plugin | EssentialsX, CMI, etc. |

> ⚠️ **Spigot is not officially supported.** Paper is strongly recommended.

---

## 🚀 Installation

1. Download `JeyukDeathPoints-1.0.0.jar`
2. Place it in your server's `/plugins/` folder
3. Make sure **Vault** and an economy plugin (e.g. EssentialsX) are installed
4. Start or restart your server
5. Edit `plugins/JeyukDeathPoints/config.yml` to your liking
6. Run `/jdp reload` to apply changes without restarting

---

## ⌨️ Commands

**Main command:** `/jdp` or `/jeyukdeathpoints`

| Command | Description | Permission |
|---|---|---|
| `/jdp help` | Show all commands | `jdp.use` |
| `/jdp info` | View current plugin settings | `jdp.use` |
| `/jdp reload` | Reload `config.yml` | `jdp.reload` |
| `/jdp toggle` | Enable or disable the plugin | `jdp.admin` |
| `/jdp percent <0-100>` | Set the deduction percentage | `jdp.admin` |
| `/jdp world add <world>` | Add a world to the penalty list | `jdp.admin` |
| `/jdp world remove <world>` | Remove a world from the penalty list | `jdp.admin` |
| `/jdp world list` | List all active worlds | `jdp.admin` |
| `/jdp minbalance <amount>` | Set the minimum balance floor | `jdp.admin` |
| `/jdp pvp <on\|off>` | Toggle penalty on PvP deaths | `jdp.admin` |
| `/jdp pve <on\|off>` | Toggle penalty on PvE deaths | `jdp.admin` |
| `/jdp check [player]` | Preview how much a player would lose | `jdp.use` |

> All changes made via commands are **automatically saved** to `config.yml`.

---

## 🔑 Permissions

| Permission | Description | Default |
|---|---|---|
| `jdp.use` | Use `/jdp` and basic subcommands | `op` |
| `jdp.admin` | Access all admin subcommands | `op` |
| `jdp.reload` | Reload the configuration | `op` |
| `jdp.bypass` | **Exempt from the death penalty** | `false` |

> 💡 Grant `jdp.bypass` to VIP players, staff, or players in a grace period.

---

## ⚙️ Configuration

```yaml
# config.yml — plugins/JeyukDeathPoints/config.yml

settings:
  enabled: true

  # Worlds where the death penalty applies
  # Use '*' for all worlds
  worlds:
    - world
    - world_nether
    - world_the_end

  # Percentage of balance deducted on death
  deduction-percent: 10.0

  # Player's balance will never drop below this value (-1 to disable)
  minimum-balance: 0.0

  # Player must have at least this much for the penalty to apply
  minimum-required: 1.0

  deduct-on-pvp: true   # Apply penalty on player kills
  deduct-on-pve: true   # Apply penalty on mob/environment deaths
  log-to-console: true  # Log deductions in the server console

messages:
  prefix: "&8[&cJDP&8] &r"
  death-chat: "&cYou lost &e{amount} &c({percent}%) on death! Remaining: &e{balance_after}"
  death-title: "&c&l-{amount}"
  death-subtitle: "&e{percent}% deducted on death"
  # title-fade-in / title-stay / title-fade-out are in ticks (20 ticks = 1 second)

economy:
  symbol: "$"
  decimal-places: 2
```

---

## 🏷️ Placeholders

These placeholders are available in `death-chat`, `death-title`, and `death-subtitle`:

| Placeholder | Description | Example |
|---|---|---|
| `{amount}` | Amount of money deducted | `$125.00` |
| `{percent}` | Percentage that was applied | `10.0` |
| `{balance_after}` | Player's balance after deduction | `$1,125.00` |
| `{world}` | World the player died in | `world_nether` |

---

## 📸 Preview

```
[On death — screen title]
        -$125.00
   10.0% deducted on death

[In chat]
[JDP] You lost $125.00 (10.0%) on death! Remaining balance: $1,125.00
```
<img width="1600" height="720" alt="Screenshot_20260424_185625_MojoLauncher (Minecraft Java Edition for Android)" src="https://github.com/user-attachments/assets/25eb2d71-a035-4d37-993a-4920b184334c" />

---

## 🔗 Dependencies

- [Vault](https://www.spigotmc.org/resources/vault.34315/) — Economy abstraction layer  
- Any Vault-compatible economy plugin:
  - [EssentialsX](https://essentialsx.net/)
  - [CMI](https://www.spigotmc.org/resources/cmi-298-commands-insane-placeholders-economy-mysql-sqlite-bungee-bungeecord-support.3742/)
  - [PlayerPoints](https://www.spigotmc.org/resources/playerpoints.80745/)
  - And many more

---

## 🐛 Support & Issues

Found a bug or have a suggestion? Open an issue on the [GitHub Issues](../../issues) page or join my discord comunity [Discord](https://discord.gg/5HAzVJ45V5).  
Please include your server version, plugin version, and full error log if applicable.

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

Made with ❤️ by **Jeyuk & azizmc**

</div>
