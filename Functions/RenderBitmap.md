# RenderBitmap

Renderiza uma imagem 2D com controle completo de UV e transparência.

## Assinatura

```lua
RenderBitmap(id, x, y, w, h, u, v, uw, vh, scale, startScale, alpha) -> void
```

## Parâmetros

- `id` (number): ID da textura
- `x`, `y` (number): Posição na tela (pixels)
- `w`, `h` (number): Largura e altura na tela (pixels)
- `u`, `v` (number): Coordenadas UV iniciais (0.0 - 1.0)
- `uw`, `vh` (number): Tamanho UV (0.0 - 1.0)
- `scale` (bool): Aplicar escala
- `startScale` (bool): Escala inicial
- `alpha` (number): Transparência (0.0 = transparente, 1.0 = opaco)

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Renderiza uma imagem 2D com controle completo sobre coordenadas UV, escala e transparência. Use quando precisar de controle preciso sobre a renderização.

## Exemplos

### Renderização Básica

```lua
function BridgeFunction_OnInterfaceRender()
    -- Renderizar textura completa
    RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```

### Sprite Sheet (Parte da Textura)

```lua
function BridgeFunction_OnInterfaceRender()
    -- Renderizar apenas parte da textura (sprite sheet)
    -- u=0.25, v=0.25, uw=0.5, vh=0.5 = renderiza o quarto central da textura
    RenderBitmap(textureId, 100, 100, 64, 64, 0.25, 0.25, 0.5, 0.5, false, false, 1.0)
end
```

### Com Transparência

```lua
function BridgeFunction_OnInterfaceRender()
    -- Habilitar alpha blending
    EnableAlphaBlend()
    
    -- Renderizar com transparência (50%)
    RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
    
    -- Desabilitar alpha blending
    DisableAlphaBlend()
end
```

### Animação de Sprite

```lua
local frame = 0
local frameTime = 0

function BridgeFunction_OnInterfaceRender()
    -- Atualizar frame da animação
    frameTime = frameTime + 1
    if frameTime > 10 then
        frame = (frame + 1) % 4 -- 4 frames
        frameTime = 0
    end
    
    -- Calcular UV para o frame atual
    local u = (frame % 2) * 0.5 -- 2 colunas
    local v = math.floor(frame / 2) * 0.5 -- 2 linhas
    
    -- Renderizar frame da animação
    RenderBitmap(spriteSheetId, 100, 100, 64, 64, u, v, 0.5, 0.5, false, false, 1.0)
end
```

## Parâmetros UV

- `u`, `v`: Coordenadas iniciais na textura (0.0 = início, 1.0 = fim)
- `uw`, `vh`: Tamanho da área a renderizar (0.0 = nada, 1.0 = textura completa)

**Exemplo de UV:**
- `u=0, v=0, uw=1, vh=1`: Textura completa
- `u=0.25, v=0.25, uw=0.5, vh=0.5`: Centro da textura (25% de cada lado)

## Notas Importantes

1. **Controle completo**: Oferece controle total sobre UV, escala e transparência
2. **Sprite sheets**: Ideal para sprite sheets e animações
3. **Alpha blending**: Habilite `EnableAlphaBlend()` antes de usar transparência
4. **Performance**: Mais custoso que `RenderImage`, use apenas quando necessário

## Funções Relacionadas

- [RenderImage](RenderImage.md) - Versão simplificada de renderização
- [EnableAlphaBlend](EnableAlphaBlend.md) - Habilita transparência
- [LoadBitmap](LoadBitmap.md) - Carrega textura
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

