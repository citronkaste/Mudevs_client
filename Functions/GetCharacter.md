# GetCharacter

Gets a character object (player, monster, NPC) from its index.

## Signature

```lua
GetCharacter(index) -> GameCharacter
```

## Parameters

- `index`(number): The character's index in the game

## Return

`GameCharacter ` or`nil `- The character object if it exists, or` nil`if the index is invalid or the character does not exist.

## Examples

### Basic Use

```lua
function BridgeFunction_OnInterfaceRender()
    local character = GetCharacter(0) --Index example
    if character then
        --Character found
        local text = string.format("Nome: %s, Level: %d", character.ID, character.Level)
        UIRenderText_RenderText(100, 100, text, 300, 20, 1)
    end
end
```### Type Check```lua
function BridgeFunction_OnInterfaceRender()
    local character = GetCharacter(index)
    if character then
        if character.Kind == 0 then
            --He's a player
            UIRenderText_RenderText(10, 10, "Player:" .. character.ID, 300, 20, 1)
        elseif character.Kind == 1 then
            --It's a monster
            UIRenderText_RenderText(10, 10, "Monster:" .. character.Class, 300, 20, 1)
        elseif character.Kind == 2 then
            --It's an NPC
            UIRenderText_RenderText(10, 10, "NPC", 300, 20, 1)
        end
    end
end
```### Using Hero (Local Player)```lua
function BridgeFunction_OnInterfaceRender()
    --Hero is equivalent to GetCharacter(index) for local player
    if Hero then
        local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
        local text = string.format("%s - HP: %.1f%%", Hero.ID, hpPercent)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
    end
end
```### Selected Target Check```lua
function BridgeFunction_OnInterfaceRender()
    --Using SelectedCharacter (global variable) is more efficient
    if SelectedCharacter then
        local text = string.format("Alvo: %s (Lv.%d)", 
            SelectedCharacter.ID, SelectedCharacter.Level)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
        
        --Show target's HP
        if SelectedCharacter.CurHP > 0 then
            local hpPercent = (SelectedCharacter.CurHP / SelectedCharacter.MaxHP) * 100
            local hpText = string.format("HP: %.1f%%", hpPercent)
            UIRenderText_RenderText(10, 35, hpText, 200, 20, 1)
        end
    end
end
```

## Returned Object Properties

The returned object has several properties depending on the type:

### Common Properties

- `ID`(string): Character name/ID
- `Class`(int): Class code
- `Level`(int): Character level
- `Kind`(int): Entity type (0=Player, 1=Monster, 2=NPC)
- `PositionX `, ` PositionY`(int): Coordinates in the world
- `CurHP `, ` MaxHP`(float): Current and maximum health
- `Dead`(int): 1 if killed, 0 otherwise

### Player Specific Properties

- `CtlCode`(int): Control code (0=Normal, 8=GM, 32=Admin)
- `PK`(int): PK Level (3=Common, 6=Phonomania)
- `GuildStatus`(int): Status na guild
- `SafeZone`(int): 1 if you are in Safe Zone

Look[GameCharacter](../04-Game-Objects.md#gamecharacter)for full list of properties.

## Important Notes

1. **Always validate the return**:`GetCharacter ` can return`nil` if the index is invalid
2. **Use Hero for local player**: The global variable `Hero` is more efficient than `GetCharacter` for local player
3. **Use SelectedCharacter to target**: The global variable `SelectedCharacter` is more efficient for the selected target
4. **Check type**: Use `character.Kind` to check if it is the expected type
5. **Performance**: The function is fast, but avoid calling it multiple times in the same frame for the same index

## Related Functions

- [GetModel](GetModel.md) - Gets 3D model object
- [Hero](../10-Global-Variables.md#hero) - Local player global variable
- [SelectedCharacter](../10-Global-Variables.md#selectedcharacter) - Global variable of the selected target
- [Game Objects](../04-Game-Objects.md) - Complete documentation of objects

