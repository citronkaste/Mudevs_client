# BindTexture

Vincula uma textura para renderização.

## Assinatura

```lua
BindTexture(textureId) -> void
```

## Parâmetros

- `textureId` (number): ID da textura a ser vinculada

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Vincula uma textura para renderização. Geralmente chamado automaticamente pelas funções de renderização, mas pode ser usado para trocar texturas manualmente.

## Exemplos

### Vinculação Manual

```lua
function BridgeFunction_OnInterfaceRender()
    -- Vincular textura manualmente
    BindTexture(textureId1)
    
    -- Renderizar usando textura vinculada
    RenderBitmap(textureId1, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
    
    -- Trocar textura
    BindTexture(textureId2)
    RenderBitmap(textureId2, 300, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```

## Notas Importantes

1. **Vinculação**: Define qual textura será usada nas próximas renderizações
2. **Automático**: Geralmente não é necessário chamar manualmente
3. **Performance**: Pode ser útil para otimização em alguns casos
4. **Use com cuidado**: Pode afetar renderizações subsequentes

## Funções Relacionadas

- [LoadBitmap](LoadBitmap.md) - Carrega textura
- [RenderBitmap](RenderBitmap.md) - Renderiza imagem
- [RenderImage](RenderImage.md) - Renderiza imagem simplificada
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

