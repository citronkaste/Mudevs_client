# UIRenderText_SetBgColor

Define a cor de fundo do texto.

## Assinatura

```lua
UIRenderText_SetBgColor(r, g, b, a) -> void
```

## Parâmetros

- `r`, `g`, `b`, `a` (number): Componentes de cor (0 - 255)

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Define a cor de fundo que será usada para renderizar texto. Cria um fundo colorido atrás do texto, útil para destacar informações importantes.

## Exemplos

### Fundo Básico

```lua
function BridgeFunction_OnInterfaceRender()
    -- Fundo preto semi-transparente
    UIRenderText_SetBgColor(0, 0, 0, 128)
    
    -- Texto branco
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 100, "Texto com fundo", 200, 30, 1)
end
```

### Destaque de Informações

```lua
function BridgeFunction_OnInterfaceRender()
    -- Fundo vermelho para alertas
    UIRenderText_SetBgColor(255, 0, 0, 200)
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 100, "ALERTA!", 200, 30, 1)
    
    -- Fundo verde para sucesso
    UIRenderText_SetBgColor(0, 255, 0, 200)
    UIRenderText_RenderText(100, 140, "Sucesso!", 200, 30, 1)
end
```

### Tooltip com Fundo

```lua
function BridgeFunction_OnInterfaceRender()
    if CheckMouseIn(100, 100, 50, 50) then
        -- Fundo do tooltip
        UIRenderText_SetBgColor(30, 30, 30, 220)
        UIRenderText_RenderText(MouseX + 15, MouseY + 15, "", 200, 80, 10)
        
        -- Texto do tooltip
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(MouseX + 20, MouseY + 20, "Informação do Tooltip", 190, 20, 11)
        UIRenderText_RenderText(MouseX + 20, MouseY + 45, "Mais informações aqui", 190, 20, 11)
    end
end
```

## Notas Importantes

1. **Configure antes de renderizar**: Defina a cor de fundo antes de chamar `UIRenderText_RenderText`
2. **Componentes 0-255**: Use valores de 0 a 255 para cada componente
3. **Alpha**: O componente alpha controla transparência do fundo
4. **Destaque**: Útil para destacar informações importantes

## Funções Relacionadas

- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renderiza texto
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Define cor do texto
- [RenderTipText](RenderTipText.md) - Renderiza tooltip
- [Sistema de UI](../08-Sistema-UI.md) - Documentação completa do sistema de UI

