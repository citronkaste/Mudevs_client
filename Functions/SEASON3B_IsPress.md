# SEASON3B_IsPress

Checks whether a key has been pressed in the current frame.

## Signature

```lua
SEASON3B_IsPress(key) -> bool
```

## Parameters

- `key `(number): VK code of the key (ex:` 0x4D`for M)

## Return

`bool ` - ` true `if the key was pressed in the current frame,` false`otherwise.

## Features

- Return `true` just once per press
- Useful for toggles, shortcuts, single actions
- Must be called within `BridgeFunction_OnInterfaceRender`

## Common VK Codes

| Code | Key |
| :----- | :---- |
| `0x4D`| M |
| `0x1B`| ESC |
| `0x20`| Space |
| `0x0D`| Enter |
| `0x25`| Left Arrow |
| `0x26`| Up Arrow |
| `0x27`| Right Arrow |
| `0x28`| Down Arrow |
| `0x70`| F1 |
| `0x7B`| F12 |

Look[02-Enumerations.md](../02-Enumerations.md)for complete list.

## Examples

### UI Toggle

```lua
local uiVisible = false

function BridgeFunction_OnInterfaceRender()
    --Toggle UI with M key
    if SEASON3B_IsPress(0x4D) then --VK_M
        uiVisible = not uiVisible
    end
    
    if uiVisible then
        --Render UI
        UIRenderText_RenderText(10, 10, "Active UI", 100, 20, 1)
    end
end
```### Multiple Keys```lua
function BridgeFunction_OnInterfaceRender()
    --Close with ESC
    if SEASON3B_IsPress(0x1B) then --VK_ESCAPE
        --Close menu, etc.
    end
    
    --Open with F1
    if SEASON3B_IsPress(0x70) then --VK_F1
        --Open help menu
    end
end
```### Shortcuts with Modifiers```lua
function BridgeFunction_OnInterfaceRender()
    --Shortcut Ctrl+S (conceptual, may vary)
    if SEASON3B_IsPress(0x11) and SEASON3B_IsPress(0x53) then --Ctrl + S
        --Save something
        print("Saving...")
    end
end
```

## Difference between IsPress, IsRelease, IsRepeat and IsNone

- **IsPress**: Returns `true` once when the key is pressed
- **IsRelease**: Returns `true` once when the key is released
- **IsRepeat**: Returns `true` continuously while the key is pressed
- **IsNone**: Returns `true` when the key is not pressed

**Example:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsPress(0x4D) then
        --Executes once when M is pressed
        print("M pressed")
    end
    
    if SEASON3B_IsRepeat(0x4D) then
        --Runs continuously while M is pressed
        --Useful for continuous movement
    end
end
```

## Important Notes

1. **Call on OnInterfaceRender**: This function must be called within `BridgeFunction_OnInterfaceRender`
2. **Once per frame**: Returns `true` just once per press
3. **Use constants**: Define constants for common VK codes
4. **Performance**: The function is very fast, it can be called every frame

## Related Functions

- [SEASON3B_IsRelease](SEASON3B_IsRelease.md) - Checks if the key has been released
- [SEASON3B_IsRepeat](SEASON3B_IsRepeat.md) - Checks if the key is being held
- [SEASON3B_IsNone](SEASON3B_IsNone.md) - Checks if the key is not pressed
- [SetBlockInput](SetBlockInput.md) - Blocks game input
- [Enumerations](../02-Enumerations.md) - Complete VK codes
- [Input System](../07-Input-System.md) - Complete documentation of the input system

