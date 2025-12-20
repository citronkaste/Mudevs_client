# Variáveis Globais

Este documento descreve todas as variáveis globais disponíveis na API Lua do Client.

## Visão Geral

As variáveis globais são objetos e valores que estão sempre disponíveis em qualquer parte do script, sem necessidade de chamar funções para obtê-los.

## Hero

O objeto do jogador local (personagem do jogador).

**Tipo:** `GameCharacter`

**Descrição:** Representa o personagem do jogador que está jogando. É equivalente a chamar `GetCharacter(index)` para o índice do jogador local.

**Propriedades:** Veja [GameCharacter](04-Objetos-Game.md#gamecharacter) para lista completa.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if Hero then
        -- Acessar propriedades do jogador
        local level = Hero.Level
        local name = Hero.ID
        local hp = Hero.CurHP
        local maxHp = Hero.MaxHP
        
        -- Calcular percentual de HP
        local hpPercent = (hp / maxHp) * 100
        
        -- Renderizar informações
        local text = string.format("%s (Lv.%d) - HP: %.1f%%", name, level, hpPercent)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
    end
end
```

**Nota:** Sempre valide se `Hero` não é `nil` antes de usar, especialmente durante carregamento ou desconexão.

## MouseX

Posição X atual do cursor do mouse na tela.

**Tipo:** `int`

**Descrição:** Coordenada X do mouse em pixels (0 = esquerda da tela).

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Mostrar posição do mouse
    local text = string.format("Mouse X: %d", MouseX)
    UIRenderText_RenderText(MouseX + 10, MouseY + 10, text, 150, 20, 1)
end
```

## MouseY

Posição Y atual do cursor do mouse na tela.

**Tipo:** `int`

**Descrição:** Coordenada Y do mouse em pixels (0 = topo da tela).

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Mostrar posição do mouse
    local text = string.format("Mouse Y: %d", MouseY)
    UIRenderText_RenderText(MouseX + 10, MouseY + 10, text, 150, 20, 1)
end
```

## MouseLButton

Estado do botão esquerdo do mouse.

**Tipo:** `int`

**Valores:**
- `0`: Botão não pressionado
- `1`: Botão pressionado

**Descrição:** Indica se o botão esquerdo do mouse está atualmente pressionado.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if MouseLButton == 1 then
        -- Botão esquerdo está pressionado
        UIRenderText_RenderText(10, 10, "Botão Esquerdo Pressionado", 250, 20, 1)
    end
end
```

**Nota:** Para detectar cliques únicos, use `IsMouseClicked()` em vez de verificar esta variável.

## MouseRButton

Estado do botão direito do mouse.

**Tipo:** `int`

**Valores:**
- `0`: Botão não pressionado
- `1`: Botão pressionado

**Descrição:** Indica se o botão direito do mouse está atualmente pressionado.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if MouseRButton == 1 then
        -- Botão direito está pressionado
        UIRenderText_RenderText(10, 10, "Botão Direito Pressionado", 250, 20, 1)
    end
end
```

## SelectedCharacter

O personagem atualmente selecionado pelo jogador.

**Tipo:** `GameCharacter` ou `nil`

**Descrição:** Representa o personagem (player, monster, NPC) que está atualmente selecionado pelo jogador. Pode ser `nil` se nenhum personagem estiver selecionado.

**Propriedades:** Veja [GameCharacter](04-Objetos-Game.md#gamecharacter) para lista completa.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SelectedCharacter then
        -- Mostrar informações do personagem selecionado
        local text = string.format("Selecionado: %s (Lv.%d)", 
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

## SelectedItem

O item atualmente selecionado pelo jogador.

**Tipo:** `GameItem` ou `nil`

**Descrição:** Representa o item que está atualmente selecionado pelo jogador. Pode ser `nil` se nenhum item estiver selecionado.

**Propriedades:** Veja [GameItem](04-Objetos-Game.md#gameitem) para lista completa.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SelectedItem then
        -- Mostrar informações do item selecionado
        local text = string.format("Item: Type %d, Level +%d", 
            SelectedItem.Type, SelectedItem.Level)
        UIRenderText_RenderText(10, 10, text, 300, 20, 1)
        
        -- Mostrar durabilidade
        local durText = string.format("Durabilidade: %d", SelectedItem.Durability)
        UIRenderText_RenderText(10, 35, durText, 200, 20, 1)
    end
end
```

## Exemplo Completo: HUD com Variáveis Globais

```lua
function BridgeFunction_OnInterfaceRender()
    -- Informações do jogador
    if Hero then
        -- HP Bar
        local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
        UIRenderText_SetTextColor(255, 0, 0, 255)
        local hpText = string.format("HP: %.0f/%.0f (%.1f%%)", 
            Hero.CurHP, Hero.MaxHP, hpPercent)
        UIRenderText_RenderText(10, 10, hpText, 300, 20, 1)
        
        -- Informações básicas
        UIRenderText_SetTextColor(255, 255, 255, 255)
        local infoText = string.format("%s - Level %d", Hero.ID, Hero.Level)
        UIRenderText_RenderText(10, 35, infoText, 300, 20, 1)
    end
    
    -- Informações do alvo
    if SelectedCharacter then
        UIRenderText_SetTextColor(255, 255, 0, 255)
        local targetText = string.format("Alvo: %s (Lv.%d)", 
            SelectedCharacter.ID, SelectedCharacter.Level)
        UIRenderText_RenderText(10, 60, targetText, 300, 20, 1)
    end
    
    -- Posição do mouse
    UIRenderText_SetTextColor(200, 200, 200, 255)
    local mouseText = string.format("Mouse: %d, %d", MouseX, MouseY)
    UIRenderText_RenderText(MouseX + 15, MouseY + 15, mouseText, 150, 20, 1)
    
    -- Estado dos botões do mouse
    if MouseLButton == 1 then
        UIRenderText_SetTextColor(0, 255, 0, 255)
        UIRenderText_RenderText(10, 500, "Botão Esquerdo", 150, 20, 1)
    end
    if MouseRButton == 1 then
        UIRenderText_SetTextColor(0, 255, 0, 255)
        UIRenderText_RenderText(170, 500, "Botão Direito", 150, 20, 1)
    end
end
```

## Exemplo: Tooltip Seguindo Mouse

```lua
function BridgeFunction_OnInterfaceRender()
    -- Tooltip que segue o mouse
    local tooltipText = "Informação do Tooltip"
    
    -- Posição do tooltip (ao lado do mouse)
    local tooltipX = MouseX + 15
    local tooltipY = MouseY + 15
    
    -- Fundo do tooltip
    UIRenderText_SetBgColor(30, 30, 30, 200)
    UIRenderText_RenderText(tooltipX, tooltipY, "", 200, 50, 10)
    
    -- Texto do tooltip
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(tooltipX + 5, tooltipY + 5, tooltipText, 190, 20, 11)
    
    -- Informações adicionais baseadas no estado
    if Hero then
        local info = string.format("Level: %d", Hero.Level)
        UIRenderText_RenderText(tooltipX + 5, tooltipY + 30, info, 190, 20, 11)
    end
end
```

## Notas Importantes

1. **Validação**: Sempre valide se as variáveis não são `nil` antes de usar (especialmente `Hero`, `SelectedCharacter`, `SelectedItem`)
2. **Atualização**: As variáveis são atualizadas a cada frame no `OnInterfaceRender`
3. **Performance**: Acessar variáveis globais é muito rápido, mas evite cálculos pesados em loops
4. **Thread Safety**: As variáveis são acessíveis apenas no thread principal do cliente

## Funções Relacionadas

- [GetCharacter](../Functions/GetCharacter.md) - Obtém personagem por índice
- [IsMouseClicked](../Functions/IsMouseClicked.md) - Detecta cliques do mouse
- [CheckMouseIn](../Functions/CheckMouseIn.md) - Verifica posição do mouse
- [Objetos do Jogo](04-Objetos-Game.md) - Documentação completa dos objetos

