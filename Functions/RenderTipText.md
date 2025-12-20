# RenderTipText

Renderiza um texto estilo tooltip.

## Assinatura

```lua
RenderTipText(x, y, text) -> void
```

## Parâmetros

- `x`, `y` (number): Posição na tela (pixels)
- `text` (string): Texto do tooltip

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Renderiza texto em formato de tooltip (geralmente com fundo e borda). Útil para informações contextuais que aparecem quando o mouse está sobre algo.

## Exemplos

### Tooltip Básico

```lua
function BridgeFunction_OnInterfaceRender()
    -- Verificar hover sobre item
    if CheckMouseIn(100, 100, 50, 50) then
        -- Mostrar tooltip
        RenderTipText(MouseX + 10, MouseY + 10, "Item: Espada +15")
    end
end
```

### Tooltip com Informações

```lua
function BridgeFunction_OnInterfaceRender()
    if CheckMouseIn(100, 100, 50, 50) then
        -- Tooltip com múltiplas informações
        RenderTipText(MouseX + 10, MouseY + 10, "Espada +15\nDano: 150-200\nDurabilidade: 200/200")
    end
end
```

### Tooltip Condicional

```lua
function BridgeFunction_OnInterfaceRender()
    -- Verificar diferentes áreas
    if CheckMouseIn(100, 100, 50, 50) then
        RenderTipText(MouseX + 10, MouseY + 10, "Botão 1")
    elseif CheckMouseIn(160, 100, 50, 50) then
        RenderTipText(MouseX + 10, MouseY + 10, "Botão 2")
    elseif CheckMouseIn(220, 100, 50, 50) then
        RenderTipText(MouseX + 10, MouseY + 10, "Botão 3")
    end
end
```

## Notas Importantes

1. **Formato tooltip**: Renderiza em formato específico de tooltip (com fundo e borda)
2. **Posição**: Geralmente posicionado próximo ao mouse
3. **Informações contextuais**: Ideal para informações que aparecem ao passar o mouse
4. **Simples**: Versão simplificada, use `UIRenderText_RenderText` para mais controle

## Funções Relacionadas

- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renderiza texto com controle completo
- [CheckMouseIn](CheckMouseIn.md) - Verifica se mouse está em área
- [Sistema de UI](../08-Sistema-UI.md) - Documentação completa do sistema de UI

