# Actual Outcome Preview — a WYSIWYG combat preview mod for *Unity of Command II*

**中文说明见下方 [中文简介](#中文简介)。**

See this battle before you commit.

Expected losses help you judge the odds. When you are ready to attack, you may
want to know something more specific: **what happens this time?**

This mod adds actual-outcome previews to supported engagements in *Unity of
Command II*. It caches the game's original preparation result and reuses that
result for the subsequent action, so the preview and the action agree. It keeps
the original combat formulas — this is **not** a low-randomness combat
overhaul.

---

## Releases

| Version | Status | Notes |
|---|---|---|
| `1.9.0` | **Current** | Landings, airborne drops, the air-attack family, naval bombardment and the tactical cards now show the actual outcome, and a preview that falls back to the estimate says so. |
| `1.8.3-preview-mode-localization` | Previous | English / Chinese / German / Russian option names and native tooltips; verified against the registered Windows baseline. |

Download the package from the [Releases page](https://github.com/misprit/uoc2-actual-outcome/releases).
Each release contains a ZIP and a `SHA256SUMS.txt` file — please verify the
checksum before installing.

> **This repository contains no game files.** It holds release packages and
> installation instructions only. You need your own copy of the game.

---

## Three ways to preview

The selector sits next to the **Language** option in the main menu and in the
in-game options panel. Your choice is stored in a mod-specific preference file;
the mod never extends the vanilla settings or save-game formats.

| Mode | Behaviour |
|---|---|
| **Vanilla** | The original probability / expected-outcome preview. |
| **Actual Outcome** | The actual result of supported engagements. Toggling fog-of-war visibility does not change the preview mode. |
| **Fusion** *(default until you save a setting)* | Vanilla while the fog-of-war display is **on**; Actual Outcome while it is **off**. |

Fusion follows the game's **real** fog-of-war display state, not the physical
`F` key. If you rebound the fog-of-war hotkey, your own binding still works.

Mode names and native tooltips are available in **English, Chinese, German and
Russian**.

Switching preview modes or toggling fog of war draws **no additional random
numbers**. Neither is a "reroll" button.

---

## Scope

**Currently supported**

1. Regular ground combat from the unit's actual current position.
2. HQ Pindown.
3. HQ Suppressive Fire.
4. HQ Set-Piece Attack.
5. Assault crossings.
6. Amphibious landings, previewed on the cell you aim at.
7. Airborne drops, previewed on the cell you choose.
8. Air attacks: plain air attack, saturation strike, flying artillery and
   precision bombing.
9. Naval bombardment, previewed with the setting the bombardment itself uses.
10. Tactical cards: tactical para drop and tactical naval assault, including the
    divisional variants.

Previews include information on retreats, trapped units, overrun, city
destruction, fortifications and entrenchments.

**When a preview falls back.** If an exact preview cannot be prepared, this
release says so instead of quietly showing a probability estimate: map labels
switch to a distinct colour and the combat sheet names the estimate. A coloured
label or a named estimate means "this one is not the exact result". The action
itself still works.

**Not included**

- Exact previews for hypothetical movement destinations. Movement-hover
  previews deliberately keep the vanilla estimate, so you can compare
  positions; after moving, supported engagements at the unit's real position
  use your selected mode.
- Other action paths are not guaranteed.

**L-key integration.** The game's existing "Hide Map Labels" action (default
`L`) is retained. During eligible player action phases, each valid press also
discards one random value and clears cached previews so you can look again.
It does not reset the random seed, it does not guarantee a different number,
and it is inactive during AI turns, history playback and deployment.

---

## Installation

> **Manual installation is required.** Subscribing on the Steam Workshop does
> **not** install the mod, and unsubscribing does **not** undo a manual
> install. Do not install this mod alongside other mods that overwrite the same
> files without resolving the conflict first.

1. **Exit the game completely.**
2. In your Steam Library, right-click the game and choose
   *Manage → Browse local files*. The folder that opens contains `uoc2.exe`,
   `lib` and `_packages` at the same level. Do not open `lib` or `_packages`
   yet.
3. **Back up the eight original files** the mod replaces (paths relative to the
   game root):

   ```
   lib/uoc2/state/game/combat.pyc
   lib/uoc2/state/game/actions/combat.pyc
   lib/uoc2/game_world/widget.pyc
   lib/uoc2/state/proxy/game_proxy.pyc
   lib/uoc2/common/scalables.pyc
   lib/uoc2/main_screen/opt_ctrl.pyc
   _packages/base/config/ui/yml/options_general.yml
   _packages/base/config/tooltips.yml
   ```

   Steam's *Verify integrity of game files* restores them, so the replacement
   is reversible. Verification may also overwrite other mods — back those up
   first.
4. **Extract the downloaded ZIP** into a separate temporary folder. It must
   contain `lib`, `_packages`, `产品清单.json` and the README.
5. **Copy only the extracted `lib` and `_packages` folders** into the game root
   folder. When prompted, merge the folders and replace files with the same
   names. Do not delete the original folders before copying.
6. Launch the game and confirm that the preview mode selector appears to the
   right of the **Language** option.
7. Open a scenario you know, then compare a preview with the executed result
   for a supported engagement from a unit's actual position.

The package contains a file manifest (`产品清单.json`) listing all 15 files:
eight replacements and seven new files.

### Upgrading

Uninstall the old version **first**, including the files it added, then install
the new one. Steam's file verification generally does **not** remove files
that a mod added, so remove them yourself using the old manifest.

### Uninstalling

1. Exit the game.
2. Restore the eight overwritten files from your backups, or use Steam's
   *Verify integrity of game files*. If the game was updated since you made the
   backups, prefer verification so that you get the current original files.
3. After confirming that no other mod uses them, delete **only** these seven
   added files:

   ```
   lib/uoc2/state/game/wysiwyg.pyc
   lib/uoc2/state/game/preview_settings.pyc
   lib/uoc2/state/game/preview_options.pyc
   _packages/base/localization/eng/wysiwyg_preview.yml
   _packages/base/localization/chi/wysiwyg_preview.yml
   _packages/base/localization/ger/wysiwyg_preview.yml
   _packages/base/localization/rus/wysiwyg_preview.yml
   ```

> **Never delete the entire `lib`, `_packages` or `base` directory.**

The mod-specific settings file `uoc2_wysiwyg_settings.yml` in the game's user
data folder may be left in place; it cannot do anything on its own once the mod
is uninstalled. Remove or rename only that file to reset the preferences. Do
not delete your save-game folder.

---

## Troubleshooting

**The preview mode selector is missing.** Check whether you copied an extra
folder level, installed into the wrong Steam Library, or whether a game update,
file verification or another mod overwrote the files. Do not overwrite files
at random.

**The preview still shows probabilities.** Check the selected preview mode, the
fog-of-war state, whether you are hovering over a possible movement
destination, and whether the action is supported at all.

**The game reports an error on startup.** Exit the game, keep the error details
and the current files, then restore the game using the uninstall instructions.
Never replace files while the game is running.

**The F or L hotkey does not work.** Your input method may be intercepting the
key. Switch to an English input and check whether other game hotkeys work.

---

## Compatibility

Validated against the registered Windows baseline for this version only.
Compatibility with later game updates, other platforms, or other code mods that
replace the same files is **not** guaranteed.

---

## Feedback

Please include: game version and platform, language, mod version, preview mode,
fog-of-war state, combat type, the sequence of actions, the difference between
the preview and the actual outcome, any other mods installed, and screenshots
or logs.

---

## License

The mod's own source files and this repository's documentation are released
under the MIT License — see [LICENSE](LICENSE).

The mod **replaces and adds files inside the game's own installation
directory**. Those game files remain the property of their respective
copyright holders; this project does not redistribute the original game
files. Please read [NOTICE.md](NOTICE.md) for the full attribution and
disclaimer.

---

## Credits

* *Unity of Command II* is developed by **Chancellors Foundry** and published by
  **Matrix Games**. This project is a fan-made modification and is not
  affiliated with, endorsed by, or supported by either party.
* The build and verification tooling uses **PyYAML** (MIT License).
* The Chinese, English, German and Russian option strings and native tooltips
  are provided by this project.

---

# 中文简介

**下令之前，先看清这一仗。**

"预计损失"适合判断实力；但准备点击进攻时，你也许更想知道：**这一次究竟会怎样？**

本 Mod 为 *Unity of Command II* 提供所见即所得战斗预览：在支持的交战中，预览缓存原版准备结果，随后行动复用同一结果，让预览与实际结果一致。**保留原版战斗公式，不把战斗改成低随机。**

## 下载

当前版本 **1.8.3-preview-mode-localization**，请前往
[Releases 页面](https://github.com/misprit/uoc2-actual-outcome/releases) 下载。
每个 release 包含 ZIP 与 `SHA256SUMS.txt`，安装前请自行校验。

> **本仓库不含任何游戏文件**，只提供发布包与安装说明；你需要自备游戏。

## 三种预览，一个选项

选项位于主菜单／游戏内选项的**语言选择框右侧**，选择保存在 Mod 私有设置中，
不扩展原版设置或存档格式。模式名称与原生悬停提示支持**英／中／德／俄**。

| 模式 | 行为 |
|---|---|
| 原版预览 | 保留原版概率与期望值。 |
| 所见即所得预览 | 查看受支持交战的实际结果；切换战争迷雾显示不改变预览模式。 |
| 融合模式 | 战争迷雾显示**开启**时看原版，**关闭**时看实际结果。 |

融合模式跟随战争迷雾功能的**真实状态**，不限于默认 `F` 快捷键；重绑快捷键后依然有效。
切换模式或切换战争迷雾**不会额外消耗随机数**，它不是"重抽"按钮。

## 当前范围

**已支持**：实际当前位置的普通地面战斗、HQ pindown、HQ 压制射击、HQ 定位攻击、
强渡、登陆（按你瞄定的那一格）、普通空降（按你选的落格）、空袭族（普通空袭／
饱和打击／空中炮击／精确轰炸）、舰炮轰炸（预览口径与实际结算一致），以及战术卡牌
（战术空降／战术舰炮，含师级卡）；包含撤退、被困、奇袭及城市／工事／堑壕相关
预览显示整理。

**预览失败会明说**：某个交战的精确预览备不出来时，本版不会悄悄显示概率估计——
地图标签改用另一种颜色显示，战斗面板会注明这是原版估计。看到异色标签或面板上的
“原版估计”字样，就是这一格不是确定结果；行动本身仍可正常执行。

**不包含**：移动落点的精确预览（移动悬停保留原版期望值，方便比较位置；实际移动后
再按所选模式查看当前位置交战）；其他未列出的路径不作保证。**本 Mod 不是新战斗规则。**

**L 键联动**：原有隐藏地图标签功能（默认 `L`）保留，并在允许的玩家行动阶段联动
消耗一个随机值、清除旧预览供重新查看。它不重置种子，不保证每次数字改变，
且在 AI 回合、历史回放与部署阶段不生效。

## 安装前必读：本版本需要手动安装

订阅工坊**不等于安装**，取消订阅**不等于卸载**。详细步骤见上方英文说明与包内
`README-Installmethod.txt`／`必看-中文安装说明.txt`：

1. 退出游戏，备份说明中列出的八个原文件。
2. 解压后**只**将 `lib` 和 `_packages` 合并复制到游戏根目录（`uoc2.exe` 所在层）。
3. 启动游戏，在语言选项右侧选择预览模式。

卸载须恢复八个覆盖文件，并按说明删除七个新增文件；**不要删除整个目录**。

## 兼容性

按登记的 Windows 基线验收。不保证适配后续游戏更新、其他平台，或覆盖同名文件的其他 Mod。

## 反馈

请附游戏版本、语言、模式、战争迷雾状态、战斗类型、操作步骤、预览与实际结果的差异、
其他 Mod，以及截图／日志。

## 许可与致谢

本仓库的文档与本项目原创源文件采用 MIT 许可（见 [LICENSE](LICENSE)）。本 Mod
**替换并新增游戏安装目录内的文件**，这些游戏文件的所有权仍属各自权利人；本项目
**不分发原版游戏文件**。完整署名与免责声明见 [NOTICE.md](NOTICE.md)。

*《Unity of Command II》由 **Chancellors Foundry** 开发、**Matrix Games** 发行。
本项目为非官方粉丝修改，与两方无隶属、认可或支持关系。
