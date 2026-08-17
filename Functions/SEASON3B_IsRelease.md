# SEASON3B_IsRelease

Checks whether a key was released in the current frame.

## Signature

```lua
SEASON3B_IsRelease(key) -> bool
```

## Parameters

- `key `(number): VK code of the key (ex:` 0x4D`for M)

## Return

`bool ` - ` true `if the key was released in the current frame,` false`otherwise.

## Features

- Return `true` only once when the key is released
- Useful for detecting when the player stops pressing a key
- Must be called within `BridgeFunction_OnInterfaceRender`

## Examples

### Detect Key Release

```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsRelease(0x1B) then --VK_ESCAPE
        --ESC key was released
        print("ESC loose")
    end
end
```### Toggle on Release```lua
local holdingSpace = false

function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsPress(0x20) then --VK_SPACE
        holdingSpace = true
    end
    
    if SEASON3B_IsRelease(0x20) then --VK_SPACE
        holdingSpace = false
        --Take action when release
        print("Loose space - take action")
    end
end
```### Hold System```lua
local holdingKey = false

function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsPress(0x4D) then --VK_M
        holdingKey = true
        print("M key pressed")
    end
    
    if SEASON3B_IsRelease(0x4D) then --VK_M
        holdingKey = false
        print("M key loose")
    end
    
    --Do something while pressed
    if holdingKey then
        -- ...
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
        print("M pressed")
    end
    
    if SEASON3B_IsRelease(0x4D) then
        print("M loose")
    end
    
    if SEASON3B_IsRepeat(0x4D) then
        print("M held pressed")
    end
    
    if SEASON3B_IsNone(0x4D) then
        --M is not pressed
    end
end
```

## Important Notes

1. **Call on OnInterfaceRender**: This function must be called within `BridgeFunction_OnInterfaceRender`
2. **Once per frame**: Returns `true` only once when the key is released
3. **Use constants**: Define constants for common VK codes
4. **Performance**: The function is very fast, it can be called every frame

## Related Functions

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Checks if key was pressed
- [SEASON3B_IsRepeat](SEASON3B_IsRepeat.md) - Checks if the key is being held
- [SEASON3B_IsNone](SEASON3B_IsNone.md) - Checks if the key is not pressed
- [Enumerations](../02-Enumerations.md) - Complete VK codes
- [Input System](../07-Input-System.md) - Complete documentation of the input system

