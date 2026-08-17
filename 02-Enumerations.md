# Enumerations and Constants

This document lists all constants and enumerations available in the Lua Client API.

## Keyboard Codes (VK Codes)

Virtual Windows key codes used with `SEASON3B_IsPress `, ` SEASON3B_IsRelease`, etc.

| Constant | Value | Description |
| :-------- | :---- | :-------- |
| `VK_LBUTTON`| 0x01 | Left mouse button |
| `VK_RBUTTON`| 0x02 | Right mouse button |
| `VK_CANCEL`| 0x03 | Cancel |
| `VK_MBUTTON`| 0x04 | Middle mouse button |
| `VK_BACK`| 0x08 | Backspace |
| `VK_TAB`| 0x09 | Tab |
| `VK_RETURN`| 0x0D | Enter |
| `VK_SHIFT`| 0x10 | Shift |
| `VK_CONTROL`| 0x11 | Ctrl |
| `VK_MENU`| 0x12 | Alt |
| `VK_PAUSE`| 0x13 | break |
| `VK_CAPITAL`| 0x14 | Caps Lock |
| `VK_ESCAPE`| 0x1B | Esc |
| `VK_SPACE`| 0x20 | Space |
| `VK_PRIOR`| 0x21 | Page Up |
| `VK_NEXT`| 0x22 | Page Down |
| `VK_END`| 0x23 | End |
| `VK_HOME`| 0x24 | Home |
| `VK_LEFT`| 0x25 | Left Arrow |
| `VK_UP`| 0x26 | Up Arrow |
| `VK_RIGHT`| 0x27 | Right Arrow |
| `VK_DOWN`| 0x28 | Down Arrow |
| `VK_0 ` until`VK_9`| 0x30-0x39 | Numbers 0-9 |
| `VK_A ` until`VK_Z`| 0x41-0x5A | Letras A-Z |
| `VK_F1 ` until`VK_F12`| 0x70-0x7B | Function keys F1-F12 |

## Entity Types (Kind)

Used on the property `Kind` of `GameCharacter`.

| Value | Description |
| :---- | :-------- |
| 0 | Player |
| 1 | Monster |
| 2 | NPC |

## Class Codes

Character class codes used in `GameCharacter.Class`.

| Value | Class |
| :---- | :----- |
| 0 | Dark Wizard (DW) |
| 1 | Dark Knight (DK) |
| 2 | Fairy Elf (FE) |
| 3 | Magic Gladiator (MG) |
| 4 | Dark Lord (DL) |
| 5 | Summoner (SU) |
| 6 | Rage Fighter (RF) |
| 7 | Grow Lancer (GL) |
| 8 | Rune Wizard (RW) |
| 9 | Slayer (SL) |
| 10 | Gun Crusher (GC) |
| 11 | Light Wizard (LW) |
| 12 | Lemuria Mage (LM) |
| 13 | Illusion Knight (IK) |
| 14 | Mystic Knight (MK) |
| 15 | Dark Knight (DK) |
| 16 | Magic Knight (MK) |
| 17 | Dark Wizard (DW) |
| 18 | Soul Master (SM) |
| 19 | Grand Master (GM) |
| 20 | High Elf (HE) |
| 21 | Muse Elf (ME) |
| 22 | Blade Knight (BK) |
| 23 | Blade Master (BM) |
| 24 | Dark Wizard (DW) |
| 25 | Soul Master (SM) |
| 26 | Grand Master (GM) |
| 27 | Dark Knight (DK) |
| 28 | Blade Knight (BK) |
| 29 | Blade Master (BM) |
| 30 | Fairy Elf (FE) |
| 31 | Muse Elf (ME) |
| 32 | High Elf (HE) |
| 33 | Magic Gladiator (MG) |
| 34 | Dark Lord (DL) |
| 35 | Summoner (SU) |
| 36 | Rage Fighter (RF) |
| 37 | Grow Lancer (GL) |
| 38 | Rune Wizard (RW) |
| 39 | Slayer (SL) |
| 40 | Gun Crusher (GC) |
| 41 | Light Wizard (LW) |
| 42 | Lemuria Mage (LM) |
| 43 | Illusion Knight (IK) |
| 44 | Mystic Knight (MK) |

## Control Codes (CtlCode)

Used in `GameCharacter.CtlCode` to identify administrative status.

| Value | Description |
| :---- | :-------- |
| 0 | Normal Player |
| 8 | Game Master (GM) |
| 32 | Administrator |

## PK Levels

Used in `GameCharacter.PK` to identify PK status.

| Value | Description |
| :---- | :-------- |
| 3 | Common (Normal) |
| 6 | Phonomania (PK) |

## Important Notes

1. **VK Codes**: Use hexadecimal values ​​directly or define constants in your script
2. **Kind**: Always check the entity type before accessing specific properties
3. **Class**: Values ​​may vary depending on client version
4. **CtlCode**: Use to identify GMs and administrators

## Usage Examples

```lua
--Check if the M key was pressed
if SEASON3B_IsPress(0x4D) then --VK_M
    --Do something
end

--Check entity type
local character = GetCharacter(index)
if character and character.Kind == 0 then
    --He's a player
end

--Check if it is GM
if Hero and Hero.CtlCode == 8 then
    --He's a Game Master
end
```

## Related Functions

- [SEASON3B_IsPress](../Functions/SEASON3B_IsPress.md) - Checks if key was pressed
- [GetCharacter](../Functions/GetCharacter.md) - Gets character object
- [Global Variables](10-Global-Variables.md) - Documentation of global variables

