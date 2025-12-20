# DisableDepthTest

Desabilita o teste de profundidade Z-buffer (desenha por cima de tudo).

## Assinatura

```lua
DisableDepthTest() -> void
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Desabilita o teste de profundidade, permitindo que elementos sejam renderizados por cima de tudo, independente da distância. Útil para UI que sempre deve aparecer na frente.

## Exemplos

### UI Sempre na Frente

```lua
function BridgeFunction_OnInterfaceRender()
    -- Desabilitar depth test para UI
    DisableDepthTest()
    
    -- Renderizar UI (sempre na frente)
    RenderImage(uiTexture, 100, 100, 200, 200)
    UIRenderText_RenderText(110, 110, "UI Text", 180, 20, 1)
    
    -- Reabilitar depth test (se necessário)
    -- EnableDepthTest() -- Se disponível
end
```

### Overlay de UI

```lua
function BridgeFunction_OnInterfaceRender()
    -- Desabilitar depth test
    DisableDepthTest()
    
    -- Renderizar overlay
    EnableAlphaBlend()
    RenderBitmap(overlayTexture, 0, 0, 800, 600, 0, 0, 1, 1, false, false, 0.5)
    DisableAlphaBlend()
    
    -- Renderizar elementos de UI
    UIRenderText_RenderText(10, 10, "Overlay UI", 200, 20, 1)
end
```

## Notas Importantes

1. **UI sempre na frente**: Use para elementos de UI que sempre devem aparecer na frente
2. **Performance**: Desabilitar depth test pode melhorar performance para elementos 2D
3. **Use com cuidado**: Pode causar problemas se usado incorretamente com elementos 3D
4. **Combine com UI**: Ideal para interfaces de usuário e overlays

## Funções Relacionadas

- [EnableDepthMask](EnableDepthMask.md) - Habilita escrita no Z-buffer
- [DisableDepthMask](DisableDepthMask.md) - Desabilita escrita no Z-buffer
- [RenderBitmap](RenderBitmap.md) - Renderiza imagem
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

