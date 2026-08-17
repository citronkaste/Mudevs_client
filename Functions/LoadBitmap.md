# LoadBitmap

Loads a texture from an image file.

## Signature

```lua
LoadBitmap(path, id, filter, wrap, chk, full) -> int
```

## Parameters

- `path`(string): Image file path
- `id`(int): Unique ID of the texture (for later reference)
- `filter`(int): Texture filter (0 = no filter, 1 = linear)
- `wrap`(int): Modo de wrap (0 = clamp, 1 = repeat)
- `chk`(int): Check flag (0 or 1)
- `full`(int): Full path flag (0 = relative, 1 = absolute)

## Return

`int`- Operation status (0 = success, others = error).

## Usage

Loads a texture from an image file for later use. Ideal for loading resources at startup.

## Examples

### Load Texture on Startup

```lua
local buttonTextureId = 100
local backgroundTextureId = 101

function BridgeFunction_OnLoadInterface()
    --Load textures
    local status1 = LoadBitmap("Interface\\CustomUI\\button.bmp", buttonTextureId, 1, 0, 0, 1)
    local status2 = LoadBitmap("Interface\\CustomUI\\background.bmp", backgroundTextureId, 1, 0, 0, 1)
    
    if status1 == 0 and status2 == 0 then
        --Textures loaded successfully
        print("Loaded textures")
    else
        --Error loading
        print("Error loading textures")
    end
end

function BridgeFunction_OnInterfaceRender()
    --Use loaded textures
    RenderImage(buttonTextureId, 100, 100, 200, 50)
    RenderImage(backgroundTextureId, 0, 0, 800, 600)
end
```### Multiple Textures```lua
local textures = {
    button = 100,
    icon = 101,
    background = 102
}

function BridgeFunction_OnLoadInterface()
    --Load multiple textures
    LoadBitmap("Interface\\button.bmp", textures.button, 1, 0, 0, 1)
    LoadBitmap("Interface\\icon.bmp", textures.icon, 1, 0, 0, 1)
    LoadBitmap("Interface\\background.bmp", textures.background, 1, 0, 0, 1)
end
```

## Detailed Parameters

### filter
- `0`: No filter (pixelated)
- `1`: Linear filter (smooth)

### wrap
- `0`: Clamp (does not repeat)
- `1`: Repeat (repeat)

### full
- `0`: Relative path (related to the game folder)
- `1`: Absolute path (full path)

## Important Notes

1. **Load on startup**: Use `BridgeFunction_OnLoadInterface` to load resources
2. **Unique IDs**: Use unique IDs for each texture
3. **Check status**: Always check the feedback to ensure the texture has been loaded
4. **Paths**: Use relative paths when possible

## Related Functions

- [RenderBitmap](RenderBitmap.md) - Renders loaded texture
- [RenderImage](RenderImage.md) - Renders simplified texture
- [BindTexture](BindTexture.md) - Links texture
- [BridgeFunction_OnLoadInterface](BridgeFunction_OnLoadInterface.md) - Boot hook
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

