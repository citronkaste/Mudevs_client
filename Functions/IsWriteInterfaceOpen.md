# IsWriteInterfaceOpen

Checks whether the writing interface (chat/input) is open.

## Signature

```lua
IsWriteInterfaceOpen() -> bool
```

## Parameters

None.

## Return

`bool ` - ` true `if the writing interface is open,` false`otherwise.

## Usage

Checks whether the player is typing in chat or in an input interface. Useful for disabling certain features when the player is typing.

## Examples

### Disable Custom Input During Chat

```lua
function BridgeFunction_OnInterfaceRender()
    --Do not process custom input if chat is open
    if IsWriteInterfaceOpen() then
        return
    end
    
    --Process custom input only when chat is closed
    if SEASON3B_IsPress(0x4D) then --VK_M
        --Do something
    end
end
```### Show Indicator```lua
function BridgeFunction_OnInterfaceRender()
    if IsWriteInterfaceOpen() then
        --Show typing indicator
        UIRenderText_SetTextColor(255, 255, 0, 255)
        UIRenderText_RenderText(10, 10, "Typing...", 150, 20, 1)
    end
end
```### Pause UI During Input```lua
function BridgeFunction_OnInterfaceRender()
    --Pause custom UI during input
    if IsWriteInterfaceOpen() then
        --Do not render custom UI
        return
    end
    
    --Render UI normally
    -- ...
end
```

## Important Notes

1. **Chat/Input**: Checks if any writing interface is open
2. **Disable features**: Use to disable features during input
3. **Performance**: Very fast function, can be called every frame
4. **UX**: Improves user experience by avoiding input conflicts

## Related Functions

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Checks if key was pressed
- [SetBlockInput](SetBlockInput.md) - Blocks game input
- [Input System](../07-Input-System.md) - Complete documentation of the input system

