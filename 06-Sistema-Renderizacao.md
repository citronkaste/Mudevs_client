# Sistema de Renderização

Este documento descreve o sistema completo de renderização e gráficos disponível na API Lua do Client.

## Visão Geral

O sistema de renderização permite controlar estados de renderização, carregar texturas, renderizar imagens 2D e manipular propriedades visuais dos objetos 3D.

## Estados de Renderização

### Alpha Blending

Controla a transparência e mistura de cores.

#### EnableAlphaBlend

Habilita o alpha blending padrão (aditivo).

```lua
EnableAlphaBlend() -> void
```

**Uso:**
```lua
EnableAlphaBlend()
RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5) -- 50% transparente
DisableAlphaBlend()
```

#### EnableAlphaBlendMinus

Habilita o alpha blending subtrativo.

```lua
EnableAlphaBlendMinus() -> void
```

**Uso:** Para efeitos de subtração de cor (escurecimento).

#### DisableAlphaBlend

Desabilita o alpha blending.

```lua
DisableAlphaBlend() -> void
```

### Depth Testing

Controla o teste de profundidade Z-buffer.

#### DisableDepthTest

Desabilita o teste de profundidade (desenha por cima de tudo).

```lua
DisableDepthTest() -> void
```

**Uso:** Para UI que sempre deve aparecer na frente.

#### EnableDepthMask

Habilita a escrita no Z-buffer.

```lua
EnableDepthMask() -> void
```

#### DisableDepthMask

Desabilita a escrita no Z-buffer.

```lua
DisableDepthMask() -> void
```

**Uso:** Para objetos que não devem afetar o depth buffer.

### Texturização

#### DisableTexture

Desabilita texturização (permite desenhar cores sólidas).

```lua
DisableTexture(disable) -> void
```

**Parâmetros:**
- `disable` (bool): `true` para desabilitar texturas

**Uso:**
```lua
DisableTexture(true)
-- Desenhar formas sólidas sem textura
DisableTexture(false)
```

#### EnableLightMap

Habilita lightmapping.

```lua
EnableLightMap() -> void
```

## Carregamento de Texturas

### LoadBitmap

Carrega uma textura de um arquivo de imagem.

```lua
LoadBitmap(path, id, filter, wrap, chk, full) -> int
```

**Parâmetros:**
- `path` (string): Caminho do arquivo de imagem
- `id` (number): ID único da textura (para referência posterior)
- `filter` (number): Filtro de textura (0 = sem filtro, 1 = linear)
- `wrap` (number): Modo de wrap (0 = clamp, 1 = repeat)
- `chk` (number): Flag de verificação (0 ou 1)
- `full` (number): Flag de caminho completo (0 = relativo, 1 = absoluto)

**Retorno:** Status da operação (0 = sucesso, outros = erro).

**Exemplo:**
```lua
function BridgeFunction_OnLoadInterface()
    local status = LoadBitmap("Interface\\CustomUI\\button.bmp", 100, 1, 0, 0, 1)
    if status == 0 then
        -- Textura carregada com sucesso
    end
end
```

### BindTexture

Vincula uma textura para renderização.

```lua
BindTexture(textureId) -> void
```

**Parâmetros:**
- `textureId` (number): ID da textura a ser vinculada

**Uso:** Geralmente chamado automaticamente, mas pode ser usado para trocar texturas manualmente.

## Renderização 2D

### RenderBitmap

Renderiza uma imagem 2D com controle completo de UV e transparência.

```lua
RenderBitmap(id, x, y, w, h, u, v, uw, vh, scale, startScale, alpha) -> void
```

**Parâmetros:**
- `id` (number): ID da textura
- `x`, `y` (number): Posição na tela (pixels)
- `w`, `h` (number): Largura e altura na tela (pixels)
- `u`, `v` (number): Coordenadas UV iniciais (0.0 - 1.0)
- `uw`, `vh` (number): Tamanho UV (0.0 - 1.0)
- `scale` (bool): Aplicar escala
- `startScale` (bool): Escala inicial
- `alpha` (number): Transparência (0.0 = transparente, 1.0 = opaco)

**Exemplo:**
```lua
-- Renderizar textura completa
RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)

-- Renderizar apenas parte da textura (sprite sheet)
RenderBitmap(textureId, 100, 100, 64, 64, 0.25, 0.25, 0.5, 0.5, false, false, 1.0)

-- Renderizar com transparência
EnableAlphaBlend()
RenderBitmap(textureId, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 0.5)
DisableAlphaBlend()
```

### RenderImage

Versão simplificada de renderização de imagem.

```lua
RenderImage(id, x, y, w, h) -> void
```

**Parâmetros:**
- `id` (number): ID da textura
- `x`, `y` (number): Posição na tela
- `w`, `h` (number): Largura e altura

**Uso:** Para renderização rápida sem controle de UV.

**Exemplo:**
```lua
RenderImage(buttonTextureId, 100, 100, 200, 50)
```

## Cores

### Color4f

Cria um valor de cor baseado em componentes float.

```lua
Color4f(r, g, b, a) -> DWORD
```

**Parâmetros:**
- `r`, `g`, `b`, `a` (float): Componentes de cor (0.0 - 1.0)

**Retorno:** Valor de cor DWORD.

**Exemplo:**
```lua
local red = Color4f(1.0, 0.0, 0.0, 1.0) -- Vermelho opaco
local semiTransparent = Color4f(0.0, 1.0, 0.0, 0.5) -- Verde semi-transparente
```

### RGBA

Cria um valor de cor RGBA padrão.

```lua
RGBA(r, g, b, a) -> DWORD
```

**Parâmetros:**
- `r`, `g`, `b`, `a` (number): Componentes de cor (0 - 255)

**Retorno:** Valor de cor DWORD.

**Exemplo:**
```lua
local red = RGBA(255, 0, 0, 255) -- Vermelho opaco
local green = RGBA(0, 255, 0, 128) -- Verde semi-transparente
```

## Manipulação de Modelos 3D

### Propriedades de GameBMD

Através do objeto `GameBMD` (obtido via `GetModel(index)`), você pode manipular propriedades visuais:

```lua
local model = GetModel(index)
if model then
    model.Visible = true          -- Visibilidade
    model.Alpha = 0.8             -- Transparência (0.0 - 1.0)
    model.Scale = 1.5             -- Escala
    model.LightEnable = true      -- Iluminação
    model.ContrastEnable = false  -- Contraste
end
```

## Exemplo Completo: Sistema de UI

```lua
-- Variáveis globais
local buttonTextureId = 100
local backgroundTextureId = 101
local buttonHovered = false

-- Carregar texturas
function BridgeFunction_OnLoadInterface()
    LoadBitmap("Interface\\button.bmp", buttonTextureId, 1, 0, 0, 1)
    LoadBitmap("Interface\\background.bmp", backgroundTextureId, 1, 0, 0, 1)
end

-- Renderizar UI
function BridgeFunction_OnInterfaceRender()
    -- Desabilitar depth test para UI sempre na frente
    DisableDepthTest()
    
    -- Renderizar background
    EnableAlphaBlend()
    RenderImage(backgroundTextureId, 0, 0, 800, 600)
    
    -- Verificar hover do botão
    buttonHovered = CheckMouseIn(100, 100, 200, 50)
    
    -- Renderizar botão com transparência se hover
    local alpha = buttonHovered and 0.8 or 1.0
    RenderBitmap(buttonTextureId, 100, 100, 200, 50, 0, 0, 1, 1, false, false, alpha)
    
    DisableAlphaBlend()
    -- Reabilitar depth test (se necessário)
end
```

## Boas Práticas

1. **Sempre configure estados antes de renderizar**: Habilite/desabilite alpha blending, depth test, etc.
2. **Restaura estados**: Se você desabilitar algo, reabilite quando terminar
3. **Carregue texturas na inicialização**: Use `OnLoadInterface` para carregar recursos
4. **Otimize renderização**: Evite renderizar coisas fora da tela
5. **Use RenderImage para simplicidade**: Use `RenderBitmap` apenas quando precisar de controle de UV

## Funções Relacionadas

- [EnableAlphaBlend](../Functions/EnableAlphaBlend.md) - Documentação detalhada
- [LoadBitmap](../Functions/LoadBitmap.md) - Documentação detalhada
- [RenderBitmap](../Functions/RenderBitmap.md) - Documentação detalhada
- [RenderImage](../Functions/RenderImage.md) - Documentação detalhada
- [GetModel](../Functions/GetModel.md) - Obtém objeto de modelo 3D
- [Objetos do Jogo](04-Objetos-Game.md) - Documentação de GameBMD

