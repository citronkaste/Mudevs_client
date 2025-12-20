# BridgeFunction_OnInterfaceRender

**CRÍTICO**: Chamado a cada frame do jogo para renderização da UI.

## Assinatura

```lua
function BridgeFunction_OnInterfaceRender()
    -- Sua lógica de renderização aqui
end
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Ideal para:
- Renderizar UI customizada
- Desenhar texto e imagens
- Processar input do usuário
- Atualizar elementos visuais
- Criar HUDs personalizados

## Exemplos

### Exemplo Básico

```lua
function BridgeFunction_OnInterfaceRender()
    -- Renderizar texto customizado
    UIRenderText_SetTextColor(255, 255, 0, 255) -- Amarelo
    UIRenderText_RenderText(100, 100, "Minha UI Customizada", 200, 20, 1)
end
```

### HUD de Informações do Jogador

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
    
    -- Barra de HP
    UIRenderText_SetTextColor(255, 0, 0, 255)
    local hpText = string.format("HP: %.1f%%", hpPercent)
    UIRenderText_RenderText(10, 35, hpText, 300, 20, 1)
    
    -- Barra de MP
    UIRenderText_SetTextColor(0, 100, 255, 255)
    local mpText = string.format("MP: %.1f%%", mpPercent)
    UIRenderText_RenderText(10, 60, mpText, 300, 20, 1)
end
```

### Sistema de Input

```lua
local uiVisible = false

function BridgeFunction_OnInterfaceRender()
    -- Toggle UI com tecla M
    if SEASON3B_IsPress(0x4D) then -- VK_M
        uiVisible = not uiVisible
    end
    
    if uiVisible then
        -- Renderizar UI
        UIRenderText_RenderText(10, 10, "UI Ativa", 100, 20, 1)
    end
end
```

### Sistema de Botões com Mouse

```lua
function BridgeFunction_OnInterfaceRender()
    -- Verificar clique do mouse em área específica
    if IsMouseClicked() and CheckMouseIn(100, 100, 200, 50) then
        -- Botão clicado
        UIRenderText_RenderText(100, 200, "Botão Clicado!", 150, 20, 1)
    end
    
    -- Desenhar botão visual
    RenderImage(buttonTextureId, 100, 100, 200, 50)
end
```

### Tooltip Seguindo Mouse

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
end
```

## Boas Práticas

### 1. Validação de Objetos

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    -- Usar Hero com segurança
    local level = Hero.Level
end
```

### 2. Otimização de Performance

```lua
local lastUpdate = 0
local updateInterval = 1000 -- 1 segundo

function BridgeFunction_OnInterfaceRender()
    local currentTime = GetTickCount() -- Se disponível
    
    -- Atualizar apenas a cada segundo
    if currentTime - lastUpdate > updateInterval then
        lastUpdate = currentTime
        -- Lógica pesada aqui
    end
    
    -- Renderização leve a cada frame
    UIRenderText_RenderText(10, 10, "UI", 100, 20, 1)
end
```

### 3. Organização de Código

```lua
-- Variáveis globais
local uiVisible = true
local buttonTextureId = 100

-- Função de renderização
function BridgeFunction_OnInterfaceRender()
    if uiVisible then
        RenderImage(buttonTextureId, 100, 100, 200, 50)
    end
end
```

### 4. Tratamento de Erros

```lua
function BridgeFunction_OnInterfaceRender()
    local success, error = pcall(function()
        -- Sua lógica aqui
        if Hero then
            -- Fazer algo
        end
    end)
    
    if not success then
        -- Log de erro (se disponível)
        -- LogAdd(2, "Erro: " .. tostring(error))
    end
end
```

## Notas Importantes

1. **Performance**: Esta função é chamada a cada frame. Mantenha a lógica leve!
2. **Renderização**: Configure estados de renderização antes de desenhar
3. **Validação**: Sempre valide objetos antes de usar (Hero, GetCharacter, etc.)
4. **Ordem**: A ordem de renderização importa (use o parâmetro `sort`)
5. **Não bloqueie**: Evite operações que possam travar o frame

## Funções Relacionadas

- [BridgeFunction_OnLoadInterface](BridgeFunction_OnLoadInterface.md) - Inicialização de recursos
- [BridgeFunction_OnPacketRecv](BridgeFunction_OnPacketRecv.md) - Processamento de pacotes
- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renderização de texto
- [RenderBitmap](RenderBitmap.md) - Renderização de imagens
- [Bridge Functions](../05-Bridge-Functions.md) - Documentação completa dos hooks

