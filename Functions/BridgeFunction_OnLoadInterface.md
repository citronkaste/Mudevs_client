# BridgeFunction_OnLoadInterface

Called when the interface is being initialized.

## Signature

```lua
function BridgeFunction_OnLoadInterface()
    --Your initialization logic here
end
```

## Parameters

None.

## Return

`nil`- This function does not return a value.

## Usage

Ideal for:
- Load textures and resources
- Initialize global variables
- Configure initial states
- Prepare data for later use

## Examples

### Load Textures

```lua
local buttonTextureId = 100
local backgroundTextureId = 101
local iconTextureId = 102

function BridgeFunction_OnLoadInterface()
    --Load custom textures
    local status1 = LoadBitmap("Interface\\CustomUI\\button.bmp", buttonTextureId, 1, 0, 0, 1)
    local status2 = LoadBitmap("Interface\\CustomUI\\background.bmp", backgroundTextureId, 1, 0, 0, 1)
    local status3 = LoadBitmap("Interface\\CustomUI\\icon.bmp", iconTextureId, 1, 0, 0, 1)
    
    if status1 == 0 and status2 == 0 and status3 == 0 then
        --Textures loaded successfully
        print("Resources loaded successfully")
    else
        --Error loading
        print("Error loading resources")
    end
end
```### Initialize Global Variables```lua
--Global variables
local uiVisible = false
local menuOpen = false
local customData = {}

function BridgeFunction_OnLoadInterface()
    --Initialize variables
    uiVisible = true
    menuOpen = false
    customData = {
        level = 0,
        exp = 0,
        points = 0
    }
    
    print("System initialized")
end
```### Configure Initial States```lua
local config = {
    showFPS = false,
    showHP = true,
    showMP = true,
    theme = "dark"
}

function BridgeFunction_OnLoadInterface()
    --Load settings (example)
    --config = LoadConfig() -- If available
    
    --Configure initial states
    print("Loaded Settings")
end
```### Prepare Data```lua
local itemDatabase = {}

function BridgeFunction_OnLoadInterface()
    --Prepare data (example)
    itemDatabase = {
        [1] = {name = "Espada", damage = 100},
        [2] = {name = "shield", defense = 50},
        -- ...
    }
    
    print("Prepared database")
end
```

## Good Practices

### 1. Load Resources

```lua
function BridgeFunction_OnLoadInterface()
    --Load all required resources
    LoadBitmap("path1", id1, 1, 0, 0, 1)
    LoadBitmap("path2", id2, 1, 0, 0, 1)
    -- ...
end
```### 2. Validation```lua
function BridgeFunction_OnLoadInterface()
    local success = true
    
    --Upload resources and verify
    if LoadBitmap("path", id, 1, 0, 0, 1) ~= 0 then
        success = false
    end
    
    if not success then
        print("Error loading resources")
    end
end
```### 3. Organization```lua
--Group related resources
local uiTextures = {
    button = 100,
    background = 101,
    icon = 102
}

function BridgeFunction_OnLoadInterface()
    --Load resource group
    LoadBitmap("UI\\button.bmp", uiTextures.button, 1, 0, 0, 1)
    LoadBitmap("UI\\background.bmp", uiTextures.background, 1, 0, 0, 1)
    LoadBitmap("UI\\icon.bmp", uiTextures.icon, 1, 0, 0, 1)
end
```

## Important Notes

1. **Called once**: This function is called only once during initialization
2. **Load Resources**: Use to load textures, data and resources
3. **Initialization**: Ideal for configuring initial states
4. **Errors**: Handle errors when loading resources

## Related Functions

- [LoadBitmap](LoadBitmap.md) - Load texture
- [BridgeFunction_OnInterfaceRender](BridgeFunction_OnInterfaceRender.md) - Rendering loop
- [Bridge Functions](../05-Bridge-Functions.md) - Complete documentation of hooks

