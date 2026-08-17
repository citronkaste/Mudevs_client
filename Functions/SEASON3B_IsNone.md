# SEASON3B_IsNone

Checks whether a key is not being pressed.

## Signature

```lua
SEASON3B_IsNone(key) -> bool
```

## Parameters

- `key `(number): VK code of the key (ex:` 0x4D`for M)

## Return

`bool ` - ` true `if the key is not pressed,` false`otherwise.

## Features

- Return `true` when the key is not being pressed
- Useful for resetting states, detecting when an action stops
- Must be called within `BridgeFunction_OnInterfaceRender`

## Examples

### Reset Status

```lua
local isRunning = false

function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsPress(0x20) then --VK_SPACE
        isRunning = true
    end
    
    if SEASON3B_IsNone(0x20) then --VK_SPACE
        isRunning = false
        --Reset state when key is not pressed
    end
end
```### Detect When Action Stops```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsNone(0x4D) then --VK_M
        --M key is not pressed
        --Take action when you stop pressing
    end
end
```### Key State```lua
function BridgeFunction_OnInterfaceRender()
    --Check status of multiple keys
    if SEASON3B_IsNone(0x20) and SEASON3B_IsNone(0x4D) then
        --No keys are pressed
        --Default state
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
    
    if SEASON3B_IsRepeat(0x4D) then
        print("M held pressed")
    end
    
    if SEASON3B_IsNone(0x4D) then
        print("M is not pressed")
    end
end
```

## Important Notes

1. **Call on OnInterfaceRender**: This function must be called within `BridgeFunction_OnInterfaceRender`
2. **Default State**: Returns `true` when the key is in the default state (not pressed)
3. **Use to reset**: Ideal for resetting states when a key is not being used
4. **Performance**: The function is very fast, it can be called every frame

## Related Functions

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Checks if key was pressed
- [SEASON3B_IsRelease](SEASON3B_IsRelease.md) - Checks if the key has been released
- [SEASON3B_IsRepeat](SEASON3B_IsRepeat.md) - Checks if the key is being held
- [Enumerations](../02-Enumerations.md) - Complete VK codes
- [Input System](../07-Input-System.md) - Complete documentation of the input system

