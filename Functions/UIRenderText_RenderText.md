# UIRenderText_RenderText

Renderiza texto na tela.

## Assinatura

```lua
UIRenderText_RenderText(x, y, text, w, h, sort) -> void
```

## Parâmetros

- `x` (number): Posição X na tela (pixels)
- `y` (number): Posição Y na tela (pixels)
- `text` (string): Texto a ser renderizado
- `w` (number): Largura da área de texto (pixels)
- `h` (number): Altura da área de texto (pixels)
- `sort` (number): Ordem de renderização (z-order, maior = renderizado por cima)

## Retorno

`nil` - Esta função não retorna valor.

## Características

- O texto será renderizado usando a fonte, cor e fundo definidos anteriormente
- O parâmetro `sort` controla a ordem de renderização (z-order)
- Texto muito longo será cortado se exceder a largura especificada
- Deve ser chamado dentro de `BridgeFunction_OnInterfaceRender`

## Exemplos

### Uso Básico

```lua
function BridgeFunction_OnInterfaceRender()
    -- Definir cor do texto
    UIRenderText_SetTextColor(255, 255, 255, 255) -- Branco
    
    -- Renderizar texto
    UIRenderText_RenderText(100, 100, "Hello World!", 200, 20, 1)
end
```

### Texto com Informações do Jogador

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    -- Informações do jogador
    local info = string.format("Level: %d | HP: %.0f/%.0f", 
        Hero.Level, Hero.CurHP, Hero.MaxHP)
    
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(10, 10, info, 300, 20, 1)
end
```

### Múltiplos Textos com Z-Order

```lua
function BridgeFunction_OnInterfaceRender()
    -- Texto de fundo (sort baixo)
    UIRenderText_SetBgColor(0, 0, 0, 200)
    UIRenderText_RenderText(100, 100, "", 200, 100, 1)
    
    -- Texto principal (sort alto, aparece por cima)
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(110, 110, "Texto Principal", 180, 20, 10)
    
    -- Texto secundário
    UIRenderText_SetTextColor(200, 200, 200, 255)
    UIRenderText_RenderText(110, 135, "Texto Secundário", 180, 20, 10)
end
```

### Texto com Cores Diferentes

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero == nil then return end
    
    -- Nome do jogador (branco)
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(10, 10, Hero.ID, 200, 20, 1)
    
    -- Level (amarelo)
    UIRenderText_SetTextColor(255, 255, 0, 255)
    local levelText = "Level: " .. Hero.Level
    UIRenderText_RenderText(10, 35, levelText, 200, 20, 1)
    
    -- HP (verde)
    UIRenderText_SetTextColor(0, 255, 0, 255)
    local hpText = string.format("HP: %.0f/%.0f", Hero.CurHP, Hero.MaxHP)
    UIRenderText_RenderText(10, 60, hpText, 200, 20, 1)
end
```

## Notas Importantes

1. **Configure cor antes**: Sempre defina a cor do texto antes de chamar `RenderText`
2. **Use sort para z-order**: Valores maiores de `sort` renderizam por cima
3. **Formate strings**: Use `string.format` para textos dinâmicos
4. **Valide objetos**: Sempre verifique se objetos não são `nil` antes de usar
5. **Performance**: Evite renderizar texto fora da tela

## Funções Relacionadas

- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Define cor do texto
- [UIRenderText_SetBgColor](UIRenderText_SetBgColor.md) - Define cor de fundo
- [UIRenderText_SetFont](UIRenderText_SetFont.md) - Define fonte
- [RenderTipText](RenderTipText.md) - Renderiza tooltip
- [Sistema de UI](../08-Sistema-UI.md) - Documentação completa do sistema de UI

