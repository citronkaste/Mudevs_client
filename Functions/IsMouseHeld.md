# IsMouseHeld

Verifica se o botão esquerdo do mouse está sendo mantido pressionado.

## Assinatura

```lua
IsMouseHeld() -> bool
```

## Parâmetros

Nenhum.

## Retorno

`bool` - `true` se o botão esquerdo do mouse está sendo mantido pressionado, `false` caso contrário.

## Características

- Retorna `true` continuamente enquanto o botão estiver pressionado
- Útil para drag & drop, seleção contínua, arrastar elementos
- Deve ser chamado dentro de `BridgeFunction_OnInterfaceRender` para funcionar corretamente

## Exemplos

### Uso Básico

```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseHeld() then
        -- Botão está sendo mantido pressionado
        UIRenderText_RenderText(100, 100, "Mouse pressionado", 200, 20, 1)
    end
end
```

### Drag & Drop

```lua
local dragging = false
local dragStartX, dragStartY = 0, 0
local windowX, windowY = 100, 100

function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() and CheckMouseIn(windowX, windowY, 200, 30) then
        -- Iniciar drag
        dragging = true
        dragStartX = MouseX - windowX
        dragStartY = MouseY - windowY
    end
    
    if IsMouseHeld() and dragging then
        -- Atualizar posição da janela
        windowX = MouseX - dragStartX
        windowY = MouseY - dragStartY
    else
        dragging = false
    end
    
    -- Renderizar janela
    RenderImage(windowTextureId, windowX, windowY, 200, 200)
end
```

### Seleção Contínua

```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseHeld() then
        -- Desenhar área de seleção
        local startX, startY = 100, 100
        local endX, endY = MouseX, MouseY
        
        -- Renderizar retângulo de seleção
        -- (usando RenderBitmap ou similar)
    end
end
```

## Diferença entre IsMouseHeld e IsMouseClicked

- **IsMouseClicked**: Retorna `true` apenas uma vez quando o botão é pressionado
- **IsMouseHeld**: Retorna `true` continuamente enquanto o botão está pressionado

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        -- Executa apenas uma vez por clique
        print("Clique detectado")
    end
    
    if IsMouseHeld() then
        -- Executa continuamente enquanto pressionado
        -- Útil para drag & drop, seleção contínua, etc.
    end
end
```

## Notas Importantes

1. **Chamada no OnInterfaceRender**: Esta função deve ser chamada dentro de `BridgeFunction_OnInterfaceRender`
2. **Contínuo**: Retorna `true` continuamente enquanto o botão está pressionado
3. **Combine com CheckMouseIn**: Use `CheckMouseIn` para verificar se o mouse está em uma área específica
4. **Performance**: A função é muito rápida, pode ser chamada a cada frame sem problemas

## Funções Relacionadas

- [IsMouseClicked](IsMouseClicked.md) - Verifica se botão foi clicado
- [CheckMouseIn](CheckMouseIn.md) - Verifica se mouse está em área retangular
- [MouseLButton](../10-Variaveis-Globais.md#mouselbutton) - Variável global do estado do botão esquerdo
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

