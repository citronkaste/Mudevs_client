# Sistema de Input

Este documento descreve o sistema completo de captura de input (mouse e teclado) disponível na API Lua do Client.

## Visão Geral

O sistema de input permite capturar eventos de mouse e teclado, permitindo criar interfaces interativas e responder a ações do usuário.

## Mouse

### IsMouseClicked

Verifica se o botão esquerdo do mouse foi clicado no frame atual.

```lua
IsMouseClicked() -> bool
```

**Retorno:** `true` se o botão foi clicado neste frame, `false` caso contrário.

**Características:**
- Retorna `true` apenas uma vez por clique
- Útil para detectar cliques únicos (não mantidos)

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        -- Botão foi clicado neste frame
        print("Mouse clicado!")
    end
end
```

### IsMouseHeld

Verifica se o botão esquerdo do mouse está sendo mantido pressionado.

```lua
IsMouseHeld() -> bool
```

**Retorno:** `true` se o botão está pressionado, `false` caso contrário.

**Características:**
- Retorna `true` enquanto o botão estiver pressionado
- Útil para drag & drop, seleção contínua, etc.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseHeld() then
        -- Botão está sendo mantido pressionado
        -- Fazer algo continuamente
    end
end
```

### CheckMouseIn

Verifica se o cursor do mouse está dentro de uma área retangular.

```lua
CheckMouseIn(x, y, w, h) -> bool
```

**Parâmetros:**
- `x` (number): Coordenada X do canto superior esquerdo
- `y` (number): Coordenada Y do canto superior esquerdo
- `w` (number): Largura do retângulo
- `h` (number): Altura do retângulo

**Retorno:** `true` se o mouse está dentro da área, `false` caso contrário.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    local buttonX, buttonY = 100, 100
    local buttonW, buttonH = 200, 50
    
    -- Verificar se mouse está sobre o botão
    if CheckMouseIn(buttonX, buttonY, buttonW, buttonH) then
        -- Mouse está sobre o botão (hover)
        -- Renderizar botão destacado
    end
    
    -- Verificar clique no botão
    if IsMouseClicked() and CheckMouseIn(buttonX, buttonY, buttonW, buttonH) then
        -- Botão foi clicado
        -- Executar ação
    end
end
```

### Variáveis Globais do Mouse

| Variável | Tipo | Descrição |
| :------- | :--- | :-------- |
| `MouseX` | `int` | Posição X atual do mouse (pixels) |
| `MouseY` | `int` | Posição Y atual do mouse (pixels) |
| `MouseLButton` | `int` | Estado do botão esquerdo (0 ou 1) |
| `MouseRButton` | `int` | Estado do botão direito (0 ou 1) |

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Mostrar posição do mouse
    local text = string.format("Mouse: %d, %d", MouseX, MouseY)
    UIRenderText_RenderText(MouseX + 10, MouseY + 10, text, 150, 20, 1)
    
    -- Verificar botão direito
    if MouseRButton == 1 then
        -- Botão direito pressionado
    end
end
```

## Teclado

### SEASON3B_IsPress

Verifica se uma tecla foi pressionada no frame atual.

```lua
SEASON3B_IsPress(key) -> bool
```

**Parâmetros:**
- `key` (number): Código VK da tecla (ex: `0x4D` para M)

**Retorno:** `true` se a tecla foi pressionada neste frame, `false` caso contrário.

**Características:**
- Retorna `true` apenas uma vez por pressionamento
- Útil para toggles, atalhos, etc.

**Exemplo:**
```lua
local uiVisible = false

function BridgeFunction_OnInterfaceRender()
    -- Toggle UI com tecla M
    if SEASON3B_IsPress(0x4D) then -- VK_M
        uiVisible = not uiVisible
    end
    
    if uiVisible then
        -- Renderizar UI
    end
end
```

### SEASON3B_IsRelease

Verifica se uma tecla foi solta no frame atual.

```lua
SEASON3B_IsRelease(key) -> bool
```

**Parâmetros:**
- `key` (number): Código VK da tecla

**Retorno:** `true` se a tecla foi solta neste frame, `false` caso contrário.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsRelease(0x1B) then -- VK_ESCAPE
        -- Tecla ESC foi solta
        -- Fechar menu, etc.
    end
end
```

### SEASON3B_IsRepeat

Verifica se uma tecla está sendo mantida pressionada (repetição).

```lua
SEASON3B_IsRepeat(key) -> bool
```

**Parâmetros:**
- `key` (number): Código VK da tecla

**Retorno:** `true` se a tecla está sendo mantida pressionada, `false` caso contrário.

**Características:**
- Retorna `true` continuamente enquanto a tecla estiver pressionada
- Útil para movimento contínuo, scroll, etc.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Movimento contínuo com setas
    if SEASON3B_IsRepeat(0x25) then -- VK_LEFT
        -- Mover para esquerda continuamente
    elseif SEASON3B_IsRepeat(0x27) then -- VK_RIGHT
        -- Mover para direita continuamente
    end
end
```

### SEASON3B_IsNone

Verifica se uma tecla não está sendo pressionada.

```lua
SEASON3B_IsNone(key) -> bool
```

**Parâmetros:**
- `key` (number): Código VK da tecla

**Retorno:** `true` se a tecla não está pressionada, `false` caso contrário.

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsNone(0x20) then -- VK_SPACE
        -- Espaço não está pressionado
        -- Resetar estado, etc.
    end
end
```

## Códigos de Teclas (VK Codes)

Códigos virtuais de teclas do Windows. Veja [02-Enumeracoes.md](02-Enumeracoes.md) para lista completa.

**Exemplos comuns:**
- `0x4D` = M
- `0x1B` = ESC
- `0x20` = Espaço
- `0x0D` = Enter
- `0x25` = Seta Esquerda
- `0x26` = Seta Cima
- `0x27` = Seta Direita
- `0x28` = Seta Baixo
- `0x70` = F1
- `0x71` = F2
- ... até `0x7B` = F12

## Bloqueio de Input

### SetBlockInput

Bloqueia ou desbloqueia o input do jogo.

```lua
SetBlockInput(block) -> void
```

**Parâmetros:**
- `block` (bool): `true` para bloquear input do jogo, `false` para desbloquear

**Uso:** Útil quando você tem uma UI modal que deve capturar todo o input.

**Exemplo:**
```lua
local modalOpen = false

function BridgeFunction_OnInterfaceRender()
    if modalOpen then
        -- Bloquear input do jogo
        SetBlockInput(true)
        
        -- Renderizar modal
        -- Processar input customizado
        
        -- Fechar modal com ESC
        if SEASON3B_IsPress(0x1B) then
            modalOpen = false
            SetBlockInput(false)
        end
    end
end
```

## Exemplo Completo: Sistema de Botões

```lua
-- Estrutura de botão
local buttons = {
    {x = 100, y = 100, w = 200, h = 50, text = "Botão 1", clicked = false},
    {x = 100, y = 160, w = 200, h = 50, text = "Botão 2", clicked = false}
}

function BridgeFunction_OnInterfaceRender()
    for i, button in ipairs(buttons) do
        -- Verificar hover
        local hovered = CheckMouseIn(button.x, button.y, button.w, button.h)
        
        -- Verificar clique
        if IsMouseClicked() and hovered then
            button.clicked = true
            -- Executar ação do botão
            print("Botão clicado: " .. button.text)
        end
        
        -- Renderizar botão
        local color = hovered and RGBA(100, 150, 255, 255) or RGBA(50, 100, 200, 255)
        -- Renderizar retângulo (usando RenderBitmap ou similar)
        
        -- Renderizar texto
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(button.x + 10, button.y + 15, button.text, button.w - 20, 20, 1)
    end
end
```

## Exemplo: Sistema de Atalhos

```lua
function BridgeFunction_OnInterfaceRender()
    -- Atalho Ctrl+S
    if SEASON3B_IsPress(0x11) and SEASON3B_IsPress(0x53) then -- Ctrl + S
        -- Salvar algo
        print("Salvando...")
    end
    
    -- Atalho Alt+T
    if SEASON3B_IsPress(0x12) and SEASON3B_IsPress(0x54) then -- Alt + T
        -- Toggle algo
        print("Toggle ativado")
    end
end
```

## Boas Práticas

1. **Use IsMouseClicked para ações únicas**: Evite usar IsMouseHeld para ações que devem acontecer apenas uma vez
2. **Verifique área antes de processar clique**: Use `CheckMouseIn` antes de processar cliques
3. **Bloqueie input quando necessário**: Use `SetBlockInput` para modais e UIs que devem capturar todo o input
4. **Use códigos VK como constantes**: Defina constantes para códigos de teclas comuns
5. **Processe input no OnInterfaceRender**: Input deve ser processado a cada frame

## Funções Relacionadas

- [IsMouseClicked](../Functions/IsMouseClicked.md) - Documentação detalhada
- [CheckMouseIn](../Functions/CheckMouseIn.md) - Documentação detalhada
- [SEASON3B_IsPress](../Functions/SEASON3B_IsPress.md) - Documentação detalhada
- [SetBlockInput](../Functions/SetBlockInput.md) - Documentação detalhada
- [Enumerações](02-Enumeracoes.md) - Códigos VK completos
- [Variáveis Globais](10-Variaveis-Globais.md) - MouseX, MouseY, etc.

