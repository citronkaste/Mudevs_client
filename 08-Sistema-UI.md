# Sistema de UI

Este documento descreve o sistema completo de interface de usuário e renderização de texto disponível na API Lua do Client.

## Visão Geral

O sistema de UI permite renderizar texto, configurar fontes, cores e criar interfaces de usuário customizadas diretamente no cliente.

## Renderização de Texto

### UIRenderText_SetFont

Define a fonte atual para renderização de texto.

```lua
UIRenderText_SetFont(fontHandle) -> void
```

**Parâmetros:**
- `fontHandle` (number): Handle da fonte a ser usada

**Uso:** Configure a fonte antes de renderizar texto. O handle geralmente é obtido do sistema de fontes do jogo.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Definir fonte (exemplo: handle 0 = fonte padrão)
    UIRenderText_SetFont(0)
    
    -- Renderizar texto com a fonte definida
    UIRenderText_RenderText(100, 100, "Texto com fonte padrão", 200, 20, 1)
end
```

### UIRenderText_SetTextColor

Define a cor do texto.

```lua
UIRenderText_SetTextColor(r, g, b, a) -> void
```

**Parâmetros:**
- `r`, `g`, `b`, `a` (number): Componentes de cor (0 - 255)

**Características:**
- A cor definida será usada para todo texto renderizado até que seja alterada
- Componente alpha controla transparência (255 = opaco, 0 = transparente)

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Texto vermelho
    UIRenderText_SetTextColor(255, 0, 0, 255)
    UIRenderText_RenderText(100, 100, "Texto Vermelho", 200, 20, 1)
    
    -- Texto verde semi-transparente
    UIRenderText_SetTextColor(0, 255, 0, 128)
    UIRenderText_RenderText(100, 130, "Texto Verde", 200, 20, 1)
    
    -- Texto branco
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 160, "Texto Branco", 200, 20, 1)
end
```

### UIRenderText_SetBgColor

Define a cor de fundo do texto.

```lua
UIRenderText_SetBgColor(r, g, b, a) -> void
```

**Parâmetros:**
- `r`, `g`, `b`, `a` (number): Componentes de cor (0 - 255)

**Uso:** Cria um fundo colorido atrás do texto, útil para destacar informações importantes.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Fundo preto semi-transparente
    UIRenderText_SetBgColor(0, 0, 0, 128)
    
    -- Texto branco
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 100, "Texto com fundo", 200, 30, 1)
end
```

### UIRenderText_RenderText

Renderiza texto na tela.

```lua
UIRenderText_RenderText(x, y, text, w, h, sort) -> void
```

**Parâmetros:**
- `x`, `y` (number): Posição na tela (pixels)
- `text` (string): Texto a ser renderizado
- `w`, `h` (number): Largura e altura da área de texto (pixels)
- `sort` (number): Ordem de renderização (maior = renderizado por último/por cima)

**Características:**
- O texto será renderizado usando a fonte, cor e fundo definidos anteriormente
- O parâmetro `sort` controla a ordem de renderização (z-order)
- Texto muito longo será cortado se exceder a largura especificada

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if Hero then
        -- Informações do jogador
        local info = string.format("Level: %d | HP: %.0f/%.0f", 
            Hero.Level, Hero.CurHP, Hero.MaxHP)
        
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(10, 10, info, 300, 20, 1)
    end
end
```

### RenderTipText

Renderiza um texto estilo tooltip.

```lua
RenderTipText(x, y, text) -> void
```

**Parâmetros:**
- `x`, `y` (number): Posição na tela (pixels)
- `text` (string): Texto do tooltip

**Uso:** Renderiza texto em formato de tooltip (geralmente com fundo e borda).

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Verificar hover sobre item
    if CheckMouseIn(100, 100, 50, 50) then
        -- Mostrar tooltip
        RenderTipText(MouseX + 10, MouseY + 10, "Item: Espada +15")
    end
end
```

## Verificação de Interface

### IsWriteInterfaceOpen

Verifica se a interface de escrita (chat/input) está aberta.

```lua
IsWriteInterfaceOpen() -> bool
```

**Retorno:** `true` se a interface de escrita está aberta, `false` caso contrário.

**Uso:** Útil para desabilitar certas funcionalidades quando o jogador está digitando.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Não processar input customizado se chat está aberto
    if IsWriteInterfaceOpen() then
        return
    end
    
    -- Processar input customizado
    if SEASON3B_IsPress(0x4D) then -- M
        -- Fazer algo
    end
end
```

## Exemplo Completo: HUD Customizado

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    -- Calcular percentuais
    local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
    local mpPercent = (Hero.CurMP / Hero.MaxMP) * 100
    
    -- Fundo semi-transparente
    UIRenderText_SetBgColor(0, 0, 0, 150)
    
    -- Informações do jogador
    UIRenderText_SetTextColor(255, 255, 255, 255)
    local playerInfo = string.format("%s (Level %d)", Hero.ID, Hero.Level)
    UIRenderText_RenderText(10, 10, playerInfo, 300, 20, 1)
    
    -- Barra de HP (vermelho)
    UIRenderText_SetTextColor(255, 0, 0, 255)
    local hpText = string.format("HP: %.1f%%", hpPercent)
    UIRenderText_RenderText(10, 35, hpText, 300, 20, 1)
    
    -- Barra de MP (azul)
    UIRenderText_SetTextColor(0, 100, 255, 255)
    local mpText = string.format("MP: %.1f%%", mpPercent)
    UIRenderText_RenderText(10, 60, mpText, 300, 20, 1)
    
    -- Status PK
    if Hero.PK > 3 then
        UIRenderText_SetTextColor(255, 0, 0, 255)
        UIRenderText_RenderText(10, 85, "PK Status: " .. Hero.PK, 300, 20, 1)
    end
end
```

## Exemplo: Menu de Opções

```lua
local menuVisible = false
local menuX, menuY = 100, 100
local menuW, menuH = 200, 300

function BridgeFunction_OnInterfaceRender()
    -- Toggle menu com tecla M
    if SEASON3B_IsPress(0x4D) then -- VK_M
        menuVisible = not menuVisible
    end
    
    if menuVisible then
        -- Bloquear input do jogo
        SetBlockInput(true)
        
        -- Fundo do menu
        UIRenderText_SetBgColor(50, 50, 50, 200)
        UIRenderText_RenderText(menuX, menuY, "", menuW, menuH, 1)
        
        -- Título
        UIRenderText_SetTextColor(255, 255, 0, 255)
        UIRenderText_RenderText(menuX + 10, menuY + 10, "Menu de Opções", menuW - 20, 25, 2)
        
        -- Opções
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(menuX + 10, menuY + 40, "Opção 1", menuW - 20, 20, 2)
        UIRenderText_RenderText(menuX + 10, menuY + 65, "Opção 2", menuW - 20, 20, 2)
        UIRenderText_RenderText(menuX + 10, menuY + 90, "Opção 3", menuW - 20, 20, 2)
        
        -- Fechar com ESC
        if SEASON3B_IsPress(0x1B) then -- VK_ESCAPE
            menuVisible = false
            SetBlockInput(false)
        end
    end
end
```

## Exemplo: Tooltip de Item

```lua
function BridgeFunction_OnInterfaceRender()
    -- Verificar se mouse está sobre área de item
    local itemX, itemY = 100, 100
    local itemW, itemH = 50, 50
    
    if CheckMouseIn(itemX, itemY, itemW, itemH) then
        -- Mostrar tooltip
        local tooltipX = MouseX + 15
        local tooltipY = MouseY + 15
        
        -- Fundo do tooltip
        UIRenderText_SetBgColor(30, 30, 30, 220)
        UIRenderText_RenderText(tooltipX, tooltipY, "", 200, 100, 10)
        
        -- Texto do tooltip
        UIRenderText_SetTextColor(255, 215, 0, 255) -- Dourado
        UIRenderText_RenderText(tooltipX + 5, tooltipY + 5, "Espada +15", 190, 20, 11)
        
        UIRenderText_SetTextColor(200, 200, 200, 255)
        UIRenderText_RenderText(tooltipX + 5, tooltipY + 30, "Dano: 150-200", 190, 20, 11)
        UIRenderText_RenderText(tooltipX + 5, tooltipY + 55, "Durabilidade: 200/200", 190, 20, 11)
    end
end
```

## Boas Práticas

1. **Configure cor antes de renderizar**: Sempre defina a cor do texto antes de chamar `RenderText`
2. **Use sort para z-order**: Valores maiores de `sort` renderizam por cima
3. **Formate strings eficientemente**: Use `string.format` para textos dinâmicos
4. **Valide objetos antes de usar**: Sempre verifique se `Hero` não é `nil`
5. **Evite renderizar fora da tela**: Verifique se elementos estão visíveis antes de renderizar
6. **Use tooltips para informações extras**: `RenderTipText` é ideal para informações contextuais

## Funções Relacionadas

- [UIRenderText_SetFont](../Functions/UIRenderText_SetFont.md) - Documentação detalhada
- [UIRenderText_SetTextColor](../Functions/UIRenderText_SetTextColor.md) - Documentação detalhada
- [UIRenderText_RenderText](../Functions/UIRenderText_RenderText.md) - Documentação detalhada
- [RenderTipText](../Functions/RenderTipText.md) - Documentação detalhada
- [IsWriteInterfaceOpen](../Functions/IsWriteInterfaceOpen.md) - Documentação detalhada
- [Sistema de Renderização](06-Sistema-Renderizacao.md) - Renderização de imagens e gráficos

