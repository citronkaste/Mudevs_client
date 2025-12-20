# UIRenderText_SetFont

Define a fonte atual para renderização de texto.

## Assinatura

```lua
UIRenderText_SetFont(fontHandle) -> void
```

## Parâmetros

- `fontHandle` (number): Handle da fonte a ser usada

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Define a fonte que será usada para renderizar texto. Configure a fonte antes de chamar `UIRenderText_RenderText`.

## Exemplos

### Definir Fonte

```lua
function BridgeFunction_OnInterfaceRender()
    -- Definir fonte (exemplo: handle 0 = fonte padrão)
    UIRenderText_SetFont(0)
    
    -- Renderizar texto com a fonte definida
    UIRenderText_RenderText(100, 100, "Texto com fonte padrão", 200, 20, 1)
end
```

### Múltiplas Fontes

```lua
function BridgeFunction_OnInterfaceRender()
    -- Texto com fonte padrão
    UIRenderText_SetFont(0)
    UIRenderText_RenderText(100, 100, "Texto Normal", 200, 20, 1)
    
    -- Texto com fonte diferente
    UIRenderText_SetFont(1)
    UIRenderText_RenderText(100, 130, "Texto Diferente", 200, 20, 1)
end
```

## Notas Importantes

1. **Configure antes de renderizar**: Defina a fonte antes de chamar `UIRenderText_RenderText`
2. **Handle da fonte**: O handle geralmente é obtido do sistema de fontes do jogo
3. **Persistência**: A fonte definida será usada até que seja alterada
4. **Fonte padrão**: Geralmente handle 0 é a fonte padrão

## Funções Relacionadas

- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renderiza texto
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Define cor do texto
- [Sistema de UI](../08-Sistema-UI.md) - Documentação completa do sistema de UI

