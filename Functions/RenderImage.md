# RenderImage

Versão simplificada de renderização de imagem.

## Assinatura

```lua
RenderImage(id, x, y, w, h) -> void
```

## Parâmetros

- `id` (number): ID da textura
- `x`, `y` (number): Posição na tela (pixels)
- `w`, `h` (number): Largura e altura (pixels)

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Renderiza uma imagem 2D de forma simplificada, sem controle de UV. Use para renderização rápida quando não precisa de controle avançado.

## Exemplos

### Renderização Básica

```lua
function BridgeFunction_OnInterfaceRender()
    -- Renderizar imagem simples
    RenderImage(textureId, 100, 100, 200, 200)
end
```

### Botões de UI

```lua
local buttonTextureId = 100

function BridgeFunction_OnInterfaceRender()
    -- Renderizar botão
    RenderImage(buttonTextureId, 100, 100, 200, 50)
    
    -- Renderizar texto sobre o botão
    UIRenderText_RenderText(150, 115, "Botão", 100, 20, 1)
end
```

### Múltiplas Imagens

```lua
function BridgeFunction_OnInterfaceRender()
    -- Renderizar múltiplas imagens
    RenderImage(icon1, 10, 10, 32, 32)
    RenderImage(icon2, 50, 10, 32, 32)
    RenderImage(icon3, 90, 10, 32, 32)
end
```

## Diferença entre RenderImage e RenderBitmap

- **RenderImage**: Simplificado, renderiza textura completa, sem controle de UV
- **RenderBitmap**: Completo, permite controle de UV, escala e transparência

**Quando usar:**
- Use `RenderImage` para renderização simples e rápida
- Use `RenderBitmap` quando precisar de controle de UV ou transparência

## Notas Importantes

1. **Simples e rápido**: Versão simplificada para renderização rápida
2. **Textura completa**: Sempre renderiza a textura completa
3. **Sem UV**: Não permite controle de coordenadas UV
4. **Performance**: Mais rápido que `RenderBitmap` para casos simples

## Funções Relacionadas

- [RenderBitmap](RenderBitmap.md) - Versão completa com controle de UV
- [LoadBitmap](LoadBitmap.md) - Carrega textura
- [BindTexture](BindTexture.md) - Vincula textura
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

