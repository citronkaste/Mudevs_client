# SEASON3B_IsRepeat

Checks whether a key is being held down (repeat).

## Signature

```lua
SEASON3B_IsRepeat(key) -> bool
```

## Parameters

- `key `(number): VK code of the key (ex:` 0x4D`for M)

## Return

`bool ` - ` true `if the key is being held down,` false`otherwise.

## Features

- Return `true` continuously while the key is pressed
- Useful for continuous movement, scrolling, repetitive actions
- Must be called within `BridgeFunction_OnInterfaceRender`

## Examples

### Continuous Movement

```lua
function BridgeFunction_OnInterfaceRender()
    --Continuous movement with arrows
    if SEASON3B_IsRepeat(0x25) then --VK_LEFT
        --Move left continuously
        print("Moving left")
    elseif SEASON3B_IsRepeat(0x27) then --VK_RIGHT
        --Move right continuously
        print("Moving right")
    end
    
    if SEASON3B_IsRepeat(0x26) then --VK_UP
        --Move up continuously
        print("Moving up")
    elseif SEASON3B_IsRepeat(0x28) then --VK_DOWN
        --Move down continuously
        print("Moving down")
    end
end
```### Continuous Scroll```lua
local scrollPosition = 0

function BridgeFunction_OnInterfaceRender()
    --Scroll with Page Up/Down
    if SEASON3B_IsRepeat(0x21) then --VK_PRIOR (Page Up)
        scrollPosition = scrollPosition - 1
    elseif SEASON3B_IsRepeat(0x22) then --VK_NEXT (Page Down)
        scrollPosition = scrollPosition + 1
    end
    
    --Render content with scroll
    -- ...
end
```### Repetitive Action```lua
function BridgeFunction_OnInterfaceRender()
    --Action that is repeated while the key is pressed
    if SEASON3B_IsRepeat(0x20) then --VK_SPACE
        --Execute action continuously
        --(e.g. shooting, running, etc.)
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
        print("M held pressed")
    end
end
```

## Important Notes

1. **Call on OnInterfaceRender**: This function must be called within `BridgeFunction_OnInterfaceRender`
2. **Continuous**: Returns `true` continuously while the key is pressed
3. **Use for movement**: Ideal for continuous movement and repetitive actions
4. **Performance**: The function is very fast, but avoid heavy logic inside the loop

## Related Functions

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Checks if key was pressed
- [SEASON3B_IsRelease](SEASON3B_IsRelease.md) - Checks if the key has been released
- [SEASON3B_IsNone](SEASON3B_IsNone.md) - Checks if the key is not pressed
- [Enumerations](../02-Enumerations.md) - Complete VK codes
- [Input System](../07-Input-System.md) - Complete documentation of the input system

