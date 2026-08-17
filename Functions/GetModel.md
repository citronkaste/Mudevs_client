# GetModel

Gets a 3D model object.

## Signature

```lua
GetModel(index) -> GameBMD
```

## Parameters

- `index`(number): Model index

## Return

`GameBMD ` or`nil `- The model object if it exists, or` nil`if the index is invalid or the model does not exist.

## Usage

Gets a 3D model object that allows you to manipulate visual properties such as visibility, transparency, scale, etc.

## Examples

### Manipulate Model Properties

```lua
function BridgeFunction_OnInterfaceRender()
    local model = GetModel(0) --Index example
    if model then
        --Change model properties
        model.Visible = true
        model.Alpha = 0.8
        model.Scale = 1.5
        model.LightEnable = true
    end
end
```### Fade In/Out```lua
local fadeAlpha = 0.0
local fadingIn = true

function BridgeFunction_OnInterfaceRender()
    local model = GetModel(modelIndex)
    if model then
        --Update alpha
        if fadingIn then
            fadeAlpha = fadeAlpha + 0.01
            if fadeAlpha >= 1.0 then
                fadeAlpha = 1.0
                fadingIn = false
            end
        else
            fadeAlpha = fadeAlpha - 0.01
            if fadeAlpha <= 0.0 then
                fadeAlpha = 0.0
                fadingIn = true
            end
        end
        
        model.Alpha = fadeAlpha
    end
end
```### Control Visibility```lua
function BridgeFunction_OnInterfaceRender()
    local model = GetModel(modelIndex)
    if model then
        --Toggle visibility with key
        if SEASON3B_IsPress(0x56) then --VK_V
            model.Visible = not model.Visible
        end
    end
end
```

## Returned Object Properties

The object `GameBMD` has the following properties:

- `Visible`(bool): Visibility flag
- `Alpha`(float): Alpha Transparency (0.0 - 1.0)
- `Scale`(float): Model scale
- `Position`(Vector3): Position (x, y, z)
- `Velocity`(float): Speed
- `Gravity`(float): Gravity
- `AnimationFrame`(float): Current frame of the animation
- `PlaySpeed`(float): Animation speed
- `LightEnable`(bool): Lighting enabled
- `ContrastEnable`(bool): Contrast enabled

Look[GameBMD](../04-Game-Objects.md#gamebmd-model)for complete documentation.

## Important Notes

1. **Always validate the return**:`GetModel ` can return`nil` if the index is invalid
2. **Visual manipulation**: Allows you to manipulate visual properties of the model
3. **Performance**: Accessing properties is fast, but avoid unnecessary loops
4. **Index**: The index is usually obtained from other game systems

## Related Functions

- [GetCharacter](GetCharacter.md) - Gets character object
- [Game Objects](../04-Game-Objects.md) - Complete documentation of objects

