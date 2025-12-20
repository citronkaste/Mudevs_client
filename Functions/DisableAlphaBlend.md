# DisableAlphaBlend

Desabilita o alpha blending.

## Assinatura

```lua
DisableAlphaBlend() -> void
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Desabilita o alpha blending, retornando ao modo de renderização padrão (sem transparência). Sempre chame esta função após renderizar elementos transparentes.

## Exemplos

### Padrão de Uso

```lua
function BridgeFunction_OnInterfaceRender()
    -- Habilitar alpha blending
    EnableAlphaBlend()
    
    -- Renderizar elementos transparentes
    RenderBitmap(texture1, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    RenderBitmap(texture2, 150, 150, 200, 200, 0, 0, 1, 1, false, false, 0.7)
    
    -- Desabilitar alpha blending
    DisableAlphaBlend()
    
    -- Renderizar elementos opacos (sem transparência)
    RenderBitmap(texture3, 200, 200, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```

### Múltiplos Grupos

```lua
function BridgeFunction_OnInterfaceRender()
    -- Grupo 1: Elementos transparentes
    EnableAlphaBlend()
    RenderBitmap(transparent1, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    DisableAlphaBlend()
    
    -- Grupo 2: Elementos opacos
    RenderBitmap(opaque1, 300, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
    
    -- Grupo 3: Mais elementos transparentes
    EnableAlphaBlend()
    RenderBitmap(transparent2, 100, 300, 200, 200, 0, 0, 1, 1, false, false, 0.7)
    DisableAlphaBlend()
end
```

## Notas Importantes

1. **Sempre desabilite**: Sempre chame `DisableAlphaBlend()` após renderizar elementos transparentes
2. **Performance**: Desabilitar quando não necessário melhora a performance
3. **Estado padrão**: O estado padrão é com alpha blending desabilitado
4. **Ordem importa**: Configure o estado antes de renderizar

## Funções Relacionadas

- [EnableAlphaBlend](EnableAlphaBlend.md) - Habilita alpha blending padrão
- [EnableAlphaBlendMinus](EnableAlphaBlendMinus.md) - Habilita alpha blending subtrativo
- [RenderBitmap](RenderBitmap.md) - Renderiza imagem
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

