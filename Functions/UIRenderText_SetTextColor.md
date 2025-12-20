# UIRenderText_SetTextColor

Define a cor do texto.

## Assinatura

```lua
UIRenderText_SetTextColor(r, g, b, a) -> void
```

## Parâmetros

- `r`, `g`, `b`, `a` (number): Componentes de cor (0 - 255)

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Define a cor que será usada para renderizar texto. Configure a cor antes de chamar `UIRenderText_RenderText`.

## Exemplos

### Cores Básicas

```lua
function BridgeFunction_OnInterfaceRender()
    -- Texto vermelho
    UIRenderText_SetTextColor(255, 0, 0, 255)
    UIRenderText_RenderText(100, 100, "Texto Vermelho", 200, 20, 1)
    
    -- Texto verde
    UIRenderText_SetTextColor(0, 255, 0, 255)
    UIRenderText_RenderText(100, 130, "Texto Verde", 200, 20, 1)
    
    -- Texto azul
    UIRenderText_SetTextColor(0, 0, 255, 255)
    UIRenderText_RenderText(100, 160, "Texto Azul", 200, 20, 1)
    
    -- Texto branco
    UIRenderText_SetTextColor(255, 255, 255, 255)
    UIRenderText_RenderText(100, 190, "Texto Branco", 200, 20, 1)
end
```

### Texto com Transparência

```lua
function BridgeFunction_OnInterfaceRender()
    -- Texto semi-transparente (50%)
    UIRenderText_SetTextColor(255, 255, 255, 128)
    UIRenderText_RenderText(100, 100, "Texto Semi-transparente", 250, 20, 1)
end
```

### Cores Dinâmicas

```lua
function BridgeFunction_OnInterfaceRender()
    if Hero then
        -- Cor baseada no HP
        local hpPercent = (Hero.CurHP / Hero.MaxHP) * 100
        local r, g, b = 255, 255, 255
        
        if hpPercent < 30 then
            r, g, b = 255, 0, 0 -- Vermelho (pouco HP)
        elseif hpPercent < 60 then
            r, g, b = 255, 255, 0 -- Amarelo (HP médio)
        else
            r, g, b = 0, 255, 0 -- Verde (HP alto)
        end
        
        UIRenderText_SetTextColor(r, g, b, 255)
        local hpText = string.format("HP: %.0f%%", hpPercent)
        UIRenderText_RenderText(10, 10, hpText, 200, 20, 1)
    end
end
```

## Notas Importantes

1. **Configure antes de renderizar**: Defina a cor antes de chamar `UIRenderText_RenderText`
2. **Componentes 0-255**: Use valores de 0 a 255 para cada componente
3. **Alpha**: O componente alpha controla transparência (255 = opaco, 0 = transparente)
4. **Persistência**: A cor definida será usada até que seja alterada

## Funções Relacionadas

- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renderiza texto
- [UIRenderText_SetBgColor](UIRenderText_SetBgColor.md) - Define cor de fundo
- [RGBA](RGBA.md) - Cria valor de cor
- [Sistema de UI](../08-Sistema-UI.md) - Documentação completa do sistema de UI

