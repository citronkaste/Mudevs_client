# DisableTexture

Desabilita texturização (permite desenhar cores sólidas).

## Assinatura

```lua
DisableTexture(disable) -> void
```

## Parâmetros

- `disable` (bool): `true` para desabilitar texturas, `false` para habilitar

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Desabilita a texturização, permitindo renderizar formas sólidas sem textura. Útil para desenhar formas geométricas simples, retângulos coloridos, etc.

## Exemplos

### Desenhar Retângulo Sólido

```lua
function BridgeFunction_OnInterfaceRender()
    -- Desabilitar texturas
    DisableTexture(true)
    
    -- Configurar cor (usando RenderBitmap ou similar sem textura)
    -- Renderizar retângulo sólido
    -- (implementação específica pode variar)
    
    -- Reabilitar texturas
    DisableTexture(false)
end
```

### Formas Geométricas

```lua
function BridgeFunction_OnInterfaceRender()
    -- Desabilitar texturas para desenhar formas
    DisableTexture(true)
    
    -- Desenhar formas sólidas
    -- (implementação específica pode variar)
    
    -- Reabilitar texturas
    DisableTexture(false)
    
    -- Renderizar elementos com textura normalmente
    RenderImage(textureId, 100, 100, 200, 200)
end
```

## Notas Importantes

1. **Cores sólidas**: Permite renderizar sem textura, apenas cores
2. **Sempre reabilite**: Chame `DisableTexture(false)` após usar
3. **Use para formas simples**: Ideal para retângulos, linhas e formas geométricas básicas
4. **Performance**: Pode melhorar performance para elementos simples

## Funções Relacionadas

- [RenderBitmap](RenderBitmap.md) - Renderiza imagem com textura
- [RenderImage](RenderImage.md) - Renderiza imagem simplificada
- [Color4f](Color4f.md) - Cria cor
- [RGBA](RGBA.md) - Cria cor RGBA
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

