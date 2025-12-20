# CheckMouseIn

Verifica se o cursor do mouse está dentro de uma área retangular.

## Assinatura

```lua
CheckMouseIn(x, y, w, h) -> bool
```

## Parâmetros

- `x` (number): Coordenada X do canto superior esquerdo do retângulo
- `y` (number): Coordenada Y do canto superior esquerdo do retângulo
- `w` (number): Largura do retângulo
- `h` (number): Altura do retângulo

## Retorno

`bool` - `true` se o mouse está dentro da área retangular, `false` caso contrário.

## Exemplos

### Verificação de Hover

```lua
function BridgeFunction_OnInterfaceRender()
    local buttonX, buttonY = 100, 100
    local buttonW, buttonH = 200, 50
    
    -- Verificar se mouse está sobre o botão
    if CheckMouseIn(buttonX, buttonY, buttonW, buttonH) then
        -- Mouse está sobre o botão (hover)
        -- Renderizar botão destacado
        UIRenderText_SetTextColor(255, 255, 0, 255) -- Amarelo
    else
        -- Mouse não está sobre o botão
        UIRenderText_SetTextColor(255, 255, 255, 255) -- Branco
    end
    
    UIRenderText_RenderText(buttonX, buttonY, "Botão", buttonW, buttonH, 1)
end
```

### Clique em Botão

```lua
function BridgeFunction_OnInterfaceRender()
    local buttonX, buttonY = 100, 100
    local buttonW, buttonH = 200, 50
    
    -- Verificar clique no botão
    if IsMouseClicked() and CheckMouseIn(buttonX, buttonY, buttonW, buttonH) then
        -- Botão foi clicado
        print("Botão clicado!")
    end
end
```

### Sistema de Múltiplos Botões

```lua
local buttons = {
    {x = 100, y = 100, w = 200, h = 50, text = "Botão 1"},
    {x = 100, y = 160, w = 200, h = 50, text = "Botão 2"},
    {x = 100, y = 220, w = 200, h = 50, text = "Botão 3"}
}

function BridgeFunction_OnInterfaceRender()
    for i, button in ipairs(buttons) do
        local hovered = CheckMouseIn(button.x, button.y, button.w, button.h)
        
        -- Renderizar botão com cor diferente se hover
        local color = hovered and RGBA(100, 150, 255, 255) or RGBA(50, 100, 200, 255)
        
        -- Verificar clique
        if IsMouseClicked() and hovered then
            print("Botão clicado: " .. button.text)
        end
    end
end
```

## Notas Importantes

1. **Coordenadas**: As coordenadas são em pixels da tela (0,0 = canto superior esquerdo)
2. **Área inclusiva**: A verificação inclui as bordas do retângulo
3. **Performance**: A função é muito rápida, pode ser chamada múltiplas vezes por frame
4. **Combine com IsMouseClicked**: Use junto com `IsMouseClicked` para detectar cliques em áreas específicas

## Funções Relacionadas

- [IsMouseClicked](IsMouseClicked.md) - Verifica se botão foi clicado
- [IsMouseHeld](IsMouseHeld.md) - Verifica se botão está pressionado
- [MouseX](../10-Variaveis-Globais.md#mousex) - Posição X do mouse
- [MouseY](../10-Variaveis-Globais.md#mousey) - Posição Y do mouse
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

