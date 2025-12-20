# GetCharacter

Obtém um objeto de personagem (player, monster, NPC) a partir de seu índice.

## Assinatura

```lua
GetCharacter(index) -> GameCharacter
```

## Parâmetros

- `index` (number): O índice do personagem no jogo

## Retorno

`GameCharacter` ou `nil` - O objeto de personagem se existir, ou `nil` se o índice for inválido ou o personagem não existir.

## Exemplos

### Uso Básico

```lua
function BridgeFunction_OnInterfaceRender()
    local character = GetCharacter(0) -- Exemplo de índice
    if character then
        -- Personagem encontrado
        local text = string.format("Nome: %s, Level: %d", character.ID, character.Level)
        UIRenderText_RenderText(100, 100, text, 300, 20, 1)
    end
end
```

### Verificação de Tipo

```lua
function BridgeFunction_OnInterfaceRender()
    local character = GetCharacter(index)
    if character then
        if character.Kind == 0 then
            -- É um jogador
            UIRenderText_RenderText(10, 10, "Jogador: " .. character.ID, 300, 20, 1)
        elseif character.Kind == 1 then
            -- É um monstro
            UIRenderText_RenderText(10, 10, "Monstro: " .. character.Class, 300, 20, 1)
        elseif character.Kind == 2 then
            -- É um NPC
            UIRenderText_RenderText(10, 10, "NPC", 300, 20, 1)
        end
    end
end
```

### Usando Hero (Jogador Local)

```lua
function BridgeFunction_OnInterfaceRender()
    -- Hero é equivalente a GetCharacter(index) para o jogador local
    if Hero then
        local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
        local text = string.format("%s - HP: %.1f%%", Hero.ID, hpPercent)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
    end
end
```

### Verificação de Alvo Selecionado

```lua
function BridgeFunction_OnInterfaceRender()
    -- Usar SelectedCharacter (variável global) é mais eficiente
    if SelectedCharacter then
        local text = string.format("Alvo: %s (Lv.%d)", 
            SelectedCharacter.ID, SelectedCharacter.Level)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
        
        -- Mostrar HP do alvo
        if SelectedCharacter.CurHP > 0 then
            local hpPercent = (SelectedCharacter.CurHP / SelectedCharacter.MaxHP) * 100
            local hpText = string.format("HP: %.1f%%", hpPercent)
            UIRenderText_RenderText(10, 35, hpText, 200, 20, 1)
        end
    end
end
```

## Propriedades do Objeto Retornado

O objeto retornado possui várias propriedades dependendo do tipo:

### Propriedades Comuns

- `ID` (string): Nome/ID do personagem
- `Class` (int): Código da classe
- `Level` (int): Nível do personagem
- `Kind` (int): Tipo de entidade (0=Player, 1=Monster, 2=NPC)
- `PositionX`, `PositionY` (int): Coordenadas no mundo
- `CurHP`, `MaxHP` (float): Vida atual e máxima
- `Dead` (int): 1 se morto, 0 caso contrário

### Propriedades Específicas de Jogadores

- `CtlCode` (int): Código de controle (0=Normal, 8=GM, 32=Admin)
- `PK` (int): Nível PK (3=Common, 6=Phonomania)
- `GuildStatus` (int): Status na guild
- `SafeZone` (int): 1 se está em Safe Zone

Veja [GameCharacter](../04-Objetos-Game.md#gamecharacter) para lista completa de propriedades.

## Notas Importantes

1. **Sempre valide o retorno**: `GetCharacter` pode retornar `nil` se o índice for inválido
2. **Use Hero para jogador local**: A variável global `Hero` é mais eficiente que `GetCharacter` para o jogador local
3. **Use SelectedCharacter para alvo**: A variável global `SelectedCharacter` é mais eficiente para o alvo selecionado
4. **Verifique o tipo**: Use `character.Kind` para verificar se é o tipo esperado
5. **Performance**: A função é rápida, mas evite chamá-la múltiplas vezes no mesmo frame para o mesmo índice

## Funções Relacionadas

- [GetModel](GetModel.md) - Obtém objeto de modelo 3D
- [Hero](../10-Variaveis-Globais.md#hero) - Variável global do jogador local
- [SelectedCharacter](../10-Variaveis-Globais.md#selectedcharacter) - Variável global do alvo selecionado
- [Objetos do Jogo](../04-Objetos-Game.md) - Documentação completa dos objetos

