# EnableLightMap

Habilita lightmapping.

## Assinatura

```lua
EnableLightMap() -> void
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Habilita o lightmapping, permitindo que objetos sejam afetados por mapas de luz. Use para renderização com iluminação pré-calculada.

## Exemplos

### Renderização com Lightmap

```lua
function BridgeFunction_OnInterfaceRender()
    -- Habilitar lightmapping
    EnableLightMap()
    
    -- Renderizar objetos com lightmap
    RenderBitmap(objectWithLightmap, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```

## Notas Importantes

1. **Lightmapping**: Sistema de iluminação pré-calculada
2. **Performance**: Pode melhorar performance em alguns casos
3. **Use com objetos 3D**: Ideal para objetos que usam lightmaps
4. **Específico do motor**: Funcionalidade específica do motor de renderização

## Funções Relacionadas

- [RenderBitmap](RenderBitmap.md) - Renderiza imagem
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

