# TankBuddy (Turtle WoW 1.12.1)

A Turtle WoW 1.12.1 tank announcement addon based on **Tank Buddy 2.0.1** (by Kolthor from Doomhammer EU, originally **Taunt Buddy v1.33** by Artun Subasi), extended with Raid Target Icon callouts, Bear Druid **Berserk**, and merged **ParryMissAnnouncer** support for Paladin and Shaman tanks.

## Requirements & Optional Integrations

- **Client DLL Mods:** None required. Runs on stock Vanilla WoW 1.12.1 / Turtle WoW using pure Lua 5.0 and standard game APIs.
- **Optional Addon:** `CT_RaidAssist` (if loaded, enables the `CTRaid` announcement channel).

## Features

- **Class-Specific Combat & Cooldown Announcements:**
  - **Warrior:** `Taunt` (resisted / immune), `Mocking Blow` (failed), `Last Stand`, `Shield Wall`, `Lifegiving Gem`.
  - **Druid:** `Growl` (resisted / immune), `Faerie Fire` & `Faerie Fire (Feral)` (resisted), `Berserk` (Bear / Dire Bear Form only), `Lifegiving Gem`.
  - **Paladin:** `Holy Strike` (dodged / parried / blocked / missed), `Hand of Reckoning` (resisted / immune), `Lifegiving Gem`.
  - **Shaman:** `Earth Shock` (resisted / immune), `Lifegiving Gem`.
- **Raid Target Icon Callouts:** Automatically wraps `$tn` with the target's raid icon label (`STAR`, `CIRCLE`, `DIAMOND`, `TRIANGLE`, `MOON`, `SQUARE`, `CROSS`, `SKULL`).
- **Context-Aware Channel Routing:** Configure separate announcement channels for **Raid**, **Party**, and **Alone** (`CTRaid`, `Raid Warning`, `Raid`, `Party`, `Yell`, `Say`, and `Custom` channels).
- **Custom Message Variables:**
  - `$tn`: Target name (with raid icon if marked)
  - `$tl`: Target level
  - `$tt`: Target creature type
  - `$res`: Combat result for `Holy Strike` (`DODGED`, `PARRIED`, `BLOCKED`, `MISSED`)
  - `$sec`: Duration in seconds (`Shield Wall`, `Last Stand`, `Lifegiving Gem`)
  - `$hp`: Hitpoints gained (`Last Stand`, `Lifegiving Gem`)
- **Auto-Remove Blessing of Salvation:** Automatically cancels Salvation buffs, with an option to only remove while in Defensive Stance (Warrior) or Bear Form (Druid).
- **Slash Commands:** `/tankbuddy` or `/tb` (open options UI), `/tb on`, `/tb off`.

## What Was Added & Fixed

- **Merged ParryMissAnnouncer:** Added `Holy Strike` (Dodge/Parry/Block/Miss), `Hand of Reckoning` (Resist/Immune) for Paladin, and `Earth Shock` (Resist/Immune) for Shaman.
- **Added Bear Druid Berserk:** Announces `You gain Berserk.` only while in Bear / Dire Bear Form.
- **Added `Immune` Detection:** `Taunt`, `Growl`, `Hand of Reckoning`, and `Earth Shock` now announce both resisted and immune outcomes.
- **Added `Lifegiving Gem` Tab:** Available to Druid, Paladin, and Shaman in addition to Warrior (fixes nil crash when triggering Gift of Life).
- **Fixed WoW 1.12 Bugs:**
  - Fixed `TB_PlayerBuff` to use `GetPlayerBuff` / `GetPlayerBuffTexture` for accurate `CancelPlayerBuff` indexing.
  - Fixed raid detection when solo in a raid subgroup (`UnitInRaid("player")` checked before `GetNumPartyMembers()`).
  - Fixed `TB_GetSWDuration` nil arithmetic on `GetTalentInfo(1, 18)` in 1.12.
  - Fixed `Last Stand` and `Lifegiving Gem` overwriting `TBText` when both `$sec` and `$hp` are used.
  - Added `Raid Warning` fallback to `RAID` when the player is neither Raid Leader nor Officer.
  - Guarded empty/nil `Custom` channel strings and allowed clearing custom channels in the UI.
  - Scoped `Icon` as `local` to avoid polluting the global namespace.
  - Updated `## Interface: 11200` and removed unused backup files.

## Credits

- **Tank Buddy 2.0.1:** Kolthor (Doomhammer EU)
- **Taunt Buddy v1.33:** Artun Subasi & Kane (Magtherion EU)
- **Raid Icon Fork:** Based on [curseforge.com/projects/tank-buddy](https://wow.curseforge.com/projects/tank-buddy)
