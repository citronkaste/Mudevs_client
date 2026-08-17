# Color4f

Creates a color value based on float components.

## Signature

```lua
Color4f(r, g, b, a) -> DWORD
```

## Parameters

- `r `, ` g `, ` b `, ` a`(float): Color components (0.0 - 1.0)

## Return

`DWORD`- Color value in DWORD format.

## Usage

Creates a color value using float components (0.0 to 1.0). Useful for color and interpolation calculations.

## Examples

### Create Colors

```lua
--Dull red
local red = Color4f(1.0, 0.0, 0.0, 1.0)

--Semi-transparent green
local green = Color4f(0.0, 1.0, 0.0, 0.5)

--opaque blue
local blue = Color4f(0.0, 0.0, 1.0, 1.0)

--Opaque white
local white = Color4f(1.0, 1.0, 1.0, 1.0)
```### Color Interpolation```lua
function InterpolateColor(color1, color2, t)
    --Linear interpolation between two colors
    local r = color1.r + (color2.r - color1.r) * t
    local g = color1.g + (color2.g - color1.g) * t
    local b = color1.b + (color2.b - color1.b) * t
    local a = color1.a + (color2.a - color1.a) * t
    return Color4f(r, g, b, a)
end
```

## Important Notes

1. **Float-based**: Uses values ​​from 0.0 to 1.0 instead of 0-255
2. **Calculations**: Ideal for mathematical calculations and interpolation
3. **DWORD**: Returns DWORD value compatible with the system
4. **Accuracy**: More accurate for calculations that `RGBA`

## Related Functions

- [RGBA](RGBA.md) - Creates color using values ​​0-255
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Set text color
- [Rendering System](../06-Rendering-System.md) - Complete rendering system documentation

