# Bridge Functions (Hooks)

Este documento descreve as funções de callback (hooks) disponíveis na API Lua do Client.

## Visão Geral

As Bridge Functions são funções especiais que o cliente chama automaticamente em momentos específicos. Você deve implementar essas funções em seu script Lua para responder a esses eventos.

## BridgeFunction_OnLoadInterface

Chamado quando a interface está sendo inicializada.

### Assinatura

```lua
function BridgeFunction_OnLoadInterface()
    -- Sua lógica aqui
end
```

### Parâmetros

Nenhum.

### Retorno

`nil` - Esta função não retorna valor.

### Uso

Ideal para:
- Carregar texturas e recursos
- Inicializar variáveis globais
- Configurar estados iniciais

### Exemplo

```lua
local myTextureId = 100

function BridgeFunction_OnLoadInterface()
    -- Carregar textura customizada
    LoadBitmap("Interface\\CustomUI\\button.bmp", myTextureId, 0, 0, 0, 1)
end
```

## BridgeFunction_OnInterfaceRender

**CRÍTICO**: Chamado a cada frame do jogo para renderização da UI.

### Assinatura

```lua
function BridgeFunction_OnInterfaceRender()
    -- Sua lógica de renderização aqui
end
```

### Parâmetros

Nenhum.

### Retorno

`nil` - Esta função não retorna valor.

### Uso

Ideal para:
- Renderizar UI customizada
- Desenhar texto e imagens
- Processar input do usuário
- Atualizar elementos visuais

### Exemplo Básico

```lua
function BridgeFunction_OnInterfaceRender()
    -- Renderizar texto customizado
    UIRenderText_SetTextColor(255, 255, 0, 255) -- Amarelo
    UIRenderText_RenderText(100, 100, "Minha UI Customizada", 200, 20, 1)
end
```

### Exemplo com Input

```lua
function BridgeFunction_OnInterfaceRender()
    -- Verificar tecla M
    if SEASON3B_IsPress(0x4D) then -- VK_M
        -- Toggle UI
        showUI = not showUI
    end
    
    if showUI then
        -- Renderizar UI
        UIRenderText_RenderText(10, 10, "UI Ativa", 100, 20, 1)
    end
end
```

### Exemplo com Mouse

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

### Exemplo com Hero

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    -- Mostrar informações do jogador
    local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
    local text = string.format("HP: %.1f%% | Level: %d", hpPercent, Hero.Level)
    
    UIRenderText_SetTextColor(0, 255, 0, 255) -- Verde
    UIRenderText_RenderText(10, 10, text, 300, 20, 1)
end
```

### Notas Importantes

1. **Performance**: Esta função é chamada a cada frame. Mantenha a lógica leve!
2. **Renderização**: Configure estados de renderização antes de desenhar
3. **Validação**: Sempre valide objetos antes de usar (Hero, GetCharacter, etc.)
4. **Ordem**: A ordem de renderização importa (use o parâmetro `sort`)

## BridgeFunction_OnPacketRecv

Chamado quando um pacote específico é recebido do servidor.

### Assinatura

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    -- Sua lógica aqui
end
```

### Parâmetros

- `index` (number): Índice do personagem relacionado
- `head` (number): Cabeçalho do pacote (header)
- `packet` (Packet): Objeto Packet com os dados

### Retorno

`number` - Retorne `1` para consumir o pacote (bloquear processamento padrão) ou `0` para continuar processamento normal.

### Uso

Ideal para:
- Processar pacotes customizados do servidor
- Interceptar e modificar pacotes existentes
- Implementar funcionalidades client-side baseadas em pacotes

### Exemplo

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    -- Interceptar pacote customizado (header 0x1234)
    if head == 0x1234 then
        local subCode = packet:ReadByte()
        local message = packet:ReadString()
        
        -- Processar mensagem customizada
        if subCode == 0x01 then
            -- Mostrar notificação
            UIRenderText_RenderText(100, 100, message, 300, 20, 1)
        end
        
        -- Consumir pacote (bloquear processamento padrão)
        return 1
    end
    
    -- Continuar processamento normal
    return 0
end
```

### Exemplo com Múltiplos Pacotes

```lua
-- Constantes de headers
local CUSTOM_HEADER_1 = 0x1234
local CUSTOM_HEADER_2 = 0x5678

function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == CUSTOM_HEADER_1 then
        -- Processar primeiro tipo de pacote
        local data = packet:ReadDword()
        -- Fazer algo com data
        return 1
    elseif head == CUSTOM_HEADER_2 then
        -- Processar segundo tipo de pacote
        local text = packet:ReadString()
        -- Fazer algo com text
        return 1
    end
    
    return 0
end
```

### Notas Importantes

1. **Consumo**: Retornar `1` bloqueia o processamento padrão do pacote
2. **Leitura**: Leia os dados na ordem correta (como foram escritos no servidor)
3. **Validação**: Sempre valide o tamanho dos dados antes de ler
4. **Performance**: Processe pacotes rapidamente para não travar o cliente

## Boas Práticas

### 1. Validação de Objetos

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    -- Usar Hero com segurança
    local level = Hero.Level
end
```

### 2. Tratamento de Erros

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

### 3. Otimização de Performance

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

### 4. Organização de Código

```lua
-- Variáveis globais
local uiVisible = true
local buttonTextureId = 100

-- Função de inicialização
function BridgeFunction_OnLoadInterface()
    LoadBitmap("Interface\\button.bmp", buttonTextureId, 0, 0, 0, 1)
end

-- Função de renderização
function BridgeFunction_OnInterfaceRender()
    if uiVisible then
        RenderImage(buttonTextureId, 100, 100, 200, 50)
    end
end

-- Função de processamento de pacotes
function BridgeFunction_OnPacketRecv(index, head, packet)
    -- Processar pacotes
    return 0
end
```

## Funções Relacionadas

- [OnLoadInterface](../Functions/BridgeFunction_OnLoadInterface.md) - Documentação detalhada
- [OnInterfaceRender](../Functions/BridgeFunction_OnInterfaceRender.md) - Documentação detalhada
- [OnPacketRecv](../Functions/BridgeFunction_OnPacketRecv.md) - Documentação detalhada
- [Packet](04-Objetos-Game.md#packet) - Documentação do objeto Packet
- [Sistema de Pacotes](09-Sistema-Pacotes.md) - Sistema completo de pacotes

