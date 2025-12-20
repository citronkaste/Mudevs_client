# EnableAlphaBlend

Habilita o alpha blending padrão (aditivo).

## Assinatura

```lua
EnableAlphaBlend() -> void
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Habilita o alpha blending padrão, permitindo renderizar objetos com transparência. Use antes de renderizar elementos transparentes e desabilite depois com `DisableAlphaBlend`.

## Exemplos

### Renderização com Transparência

```lua
function BridgeFunction_OnInterfaceRender()
    -- Habilitar alpha blending
    EnableAlphaBlend()
    
    -- Renderizar imagem com transparência (50%)
    RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    
    -- Desabilitar alpha blending
    DisableAlphaBlend()
end
```

### Múltiplos Elementos Transparentes

```lua
function BridgeFunction_OnInterfaceRender()
    EnableAlphaBlend()
    
    -- Renderizar múltiplos elementos transparentes
    RenderBitmap(texture1, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.7)
    RenderBitmap(texture2, 150, 150, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    RenderBitmap(texture3, 200, 200, 200, 200, 0, 0, 1, 1, false, false, 0.3)
    
    DisableAlphaBlend()
end
```

### Fade In/Out

```lua
local alpha = 0.0
local fadingIn = true

function BridgeFunction_OnInterfaceRender()
    -- Atualizar alpha
    if fadingIn then
        alpha = alpha + 0.01
        if alpha >= 1.0 then
            alpha = 1.0
            fadingIn = false
        end
    else
        alpha = alpha - 0.01
        if alpha <= 0.0 then
            alpha = 0.0
            fadingIn = true
        end
    end
    
    -- Renderizar com fade
    EnableAlphaBlend()
    RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, alpha)
    DisableAlphaBlend()
end
```

## Notas Importantes

1. **Sempre desabilite depois**: Chame `DisableAlphaBlend()` após renderizar elementos transparentes
2. **Performance**: Alpha blending tem um custo de performance, use apenas quando necessário
3. **Ordem importa**: Configure o estado antes de renderizar
4. **Combine com RenderBitmap**: Use o parâmetro `alpha` de `RenderBitmap` para controlar transparência

## Funções Relacionadas

- [DisableAlphaBlend](DisableAlphaBlend.md) - Desabilita alpha blending
- [EnableAlphaBlendMinus](EnableAlphaBlendMinus.md) - Habilita alpha blending subtrativo
- [RenderBitmap](RenderBitmap.md) - Renderiza imagem com controle de alpha
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

