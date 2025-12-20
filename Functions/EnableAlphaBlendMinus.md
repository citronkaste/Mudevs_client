# EnableAlphaBlendMinus

Habilita o alpha blending subtrativo.

## Assinatura

```lua
EnableAlphaBlendMinus() -> void
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Habilita o alpha blending subtrativo, que subtrai cores em vez de adicioná-las. Útil para efeitos de escurecimento, sombras e efeitos especiais.

## Exemplos

### Efeito de Escurecimento

```lua
function BridgeFunction_OnInterfaceRender()
    -- Habilitar alpha blending subtrativo
    EnableAlphaBlendMinus()
    
    -- Renderizar overlay escuro
    RenderBitmap(darkOverlayTexture, 0, 0, 800, 600, 0, 0, 1, 1, false, false, 0.3)
    
    -- Desabilitar
    DisableAlphaBlend()
end
```

### Sombra

```lua
function BridgeFunction_OnInterfaceRender()
    -- Renderizar sombra com blending subtrativo
    EnableAlphaBlendMinus()
    RenderBitmap(shadowTexture, 105, 105, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    DisableAlphaBlend()
    
    -- Renderizar objeto normal
    EnableAlphaBlend()
    RenderBitmap(objectTexture, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
    DisableAlphaBlend()
end
```

## Notas Importantes

1. **Efeito subtrativo**: Subtrai cores em vez de adicionar, criando efeito de escurecimento
2. **Use com cuidado**: Pode criar efeitos inesperados se usado incorretamente
3. **Sempre desabilite**: Chame `DisableAlphaBlend()` após usar
4. **Efeitos especiais**: Ideal para sombras, overlays escuros e efeitos visuais especiais

## Funções Relacionadas

- [EnableAlphaBlend](EnableAlphaBlend.md) - Habilita alpha blending padrão
- [DisableAlphaBlend](DisableAlphaBlend.md) - Desabilita alpha blending
- [RenderBitmap](RenderBitmap.md) - Renderiza imagem
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

