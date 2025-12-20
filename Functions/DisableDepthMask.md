# DisableDepthMask

Desabilita a escrita no Z-buffer.

## Assinatura

```lua
DisableDepthMask() -> void
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Desabilita a escrita no Z-buffer, permitindo que objetos sejam renderizados sem afetar o depth buffer. Útil para elementos que não devem interferir no depth test de outros objetos.

## Exemplos

### Elementos que Não Afetam Depth

```lua
function BridgeFunction_OnInterfaceRender()
    -- Desabilitar escrita no Z-buffer
    DisableDepthMask()
    
    -- Renderizar elementos que não devem afetar o depth buffer
    RenderBitmap(overlayTexture, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    
    -- Reabilitar (se necessário)
    EnableDepthMask()
end
```

## Notas Importantes

1. **Não afeta depth**: Objetos renderizados não atualizam o Z-buffer
2. **Use para overlays**: Ideal para elementos que não devem interferir no depth test
3. **Performance**: Pode melhorar performance em alguns casos
4. **Combine com outras funções**: Use junto com outras funções de depth para controle completo

## Funções Relacionadas

- [EnableDepthMask](EnableDepthMask.md) - Habilita escrita no Z-buffer
- [DisableDepthTest](DisableDepthTest.md) - Desabilita teste de profundidade
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

