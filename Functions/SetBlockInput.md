# SetBlockInput

Locks or unlocks the game input.

## Signature

```lua
SetBlockInput(block) -> void
```

## Parameters

- `block `(bool):` true `to block game input,` false`to unlock

## Return

`nil`- This function does not return a value.

## Usage

Useful when you have a modal UI that must capture all input, preventing the player from interacting with the game while the UI is open.

## Examples

### Modal with Input Blocking

```lua
local modalOpen = false

function BridgeFunction_OnInterfaceRender()
    if modalOpen then
        --Block game input
        SetBlockInput(true)
        
        --Render modal
        UIRenderText_SetBgColor(0, 0, 0, 200)
        UIRenderText_RenderText(100, 100, "", 400, 300, 10)
        
        --Title
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(120, 120, "Open Modal", 360, 25, 11)
        
        --Close modal with ESC
        if SEASON3B_IsPress(0x1B) then --VK_ESCAPE
            modalOpen = false
            SetBlockInput(false)
        end
    end
end
```### Options Menu```lua
local menuVisible = false

function BridgeFunction_OnInterfaceRender()
    --Toggle menu with key M
    if not menuVisible and SEASON3B_IsPress(0x4D) then --VK_M
        menuVisible = true
        SetBlockInput(true)
    end
    
    if menuVisible then
        --Render menu
        -- ...
        
        --Close menu
        if SEASON3B_IsPress(0x1B) then --VK_ESCAPE
            menuVisible = false
            SetBlockInput(false)
        end
    end
end
```### Dialog Box```lua
local dialogOpen = false
local dialogText = ""

function BridgeFunction_OnInterfaceRender()
    if dialogOpen then
        --Block input
        SetBlockInput(true)
        
        --Render dialog
        UIRenderText_SetBgColor(50, 50, 50, 220)
        UIRenderText_RenderText(200, 200, "", 400, 200, 10)
        
        --Dialog text
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(220, 220, dialogText, 360, 100, 11)
        
        --OK button
        if IsMouseClicked() and CheckMouseIn(350, 350, 100, 30) then
            dialogOpen = false
            SetBlockInput(false)
        end
        
        --Render OK button
        UIRenderText_RenderText(350, 350, "OK", 100, 30, 11)
    end
end
```

## Important Notes

1. **Always Unlock**: Always Call `SetBlockInput(false)` when to close the modal UI
2. **Use with modals**: Ideal for menus, dialogs and UIs that must capture all input
3. **Do not block permanently**: Avoid blocking input without a way to unlock it
4. **Combine with ESC**: Use ESC as the default key to close modals and unlock input

## Related Functions

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Checks if key was pressed
- [IsMouseClicked](IsMouseClicked.md) - Checks if mouse was clicked
- [Input System](../07-Input-System.md) - Complete documentation of the input system

