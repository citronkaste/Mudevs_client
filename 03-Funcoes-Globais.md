# Funções Globais de Utilidade

Este documento descreve as funções globais básicas disponíveis na API Lua do Client.

## Visão Geral

As funções globais são funções auxiliares que podem ser chamadas de qualquer parte do script sem necessidade de instanciar objetos. Elas são organizadas em categorias:

- **Input & Mouse**: Funções para capturar entrada do usuário
- **Rendering & Graphics**: Funções para renderização e gráficos
- **Text & UI**: Funções para renderização de texto e UI
- **Object Management**: Funções para gerenciar objetos do jogo

## Input & Mouse

Funções para capturar e processar entrada do usuário (mouse e teclado).

### IsMouseClicked

Verifica se o botão esquerdo do mouse foi clicado no frame atual.

```lua
IsMouseClicked() -> bool
```

**Retorno**: `true` se o botão foi clicado, `false` caso contrário.

**Exemplo:**
```lua
if IsMouseClicked() then
    -- Mouse foi clicado
end
```

### IsMouseHeld

Verifica se o botão esquerdo do mouse está sendo mantido pressionado.

```lua
IsMouseHeld() -> bool
```

**Retorno**: `true` se o botão está pressionado, `false` caso contrário.

### CheckMouseIn

Verifica se o cursor do mouse está dentro de uma área retangular.

```lua
CheckMouseIn(x, y, w, h) -> bool
```

**Parâmetros:**
- `x` (number): Coordenada X do canto superior esquerdo
- `y` (number): Coordenada Y do canto superior esquerdo
- `w` (number): Largura do retângulo
- `h` (number): Altura do retângulo

**Retorno**: `true` se o mouse está dentro da área, `false` caso contrário.

**Exemplo:**
```lua
if CheckMouseIn(100, 100, 200, 50) then
    -- Mouse está sobre o botão
end
```

### SetBlockInput

Bloqueia ou desbloqueia o input do jogo (útil para UI customizada).

```lua
SetBlockInput(block) -> void
```

**Parâmetros:**
- `block` (bool): `true` para bloquear, `false` para desbloquear

### SEASON3B_IsPress

Verifica se uma tecla foi pressionada no frame atual.

```lua
SEASON3B_IsPress(key) -> bool
```

**Parâmetros:**
- `key` (number): Código VK da tecla (ex: `0x4D` para M)

**Retorno**: `true` se a tecla foi pressionada, `false` caso contrário.

### SEASON3B_IsRelease

Verifica se uma tecla foi solta no frame atual.

```lua
SEASON3B_IsRelease(key) -> bool
```

### SEASON3B_IsRepeat

Verifica se uma tecla está sendo mantida pressionada (repetição).

```lua
SEASON3B_IsRepeat(key) -> bool
```

### SEASON3B_IsNone

Verifica se uma tecla não está sendo pressionada.

```lua
SEASON3B_IsNone(key) -> bool
```

## Rendering & Graphics

Funções para controle de renderização e gráficos.

### EnableAlphaBlend

Habilita o alpha blending padrão.

```lua
EnableAlphaBlend() -> void
```

### EnableAlphaBlendMinus

Habilita o alpha blending subtrativo.

```lua
EnableAlphaBlendMinus() -> void
```

### DisableAlphaBlend

Desabilita o alpha blending.

```lua
DisableAlphaBlend() -> void
```

### DisableDepthTest

Desabilita o teste de profundidade Z-buffer (desenha por cima).

```lua
DisableDepthTest() -> void
```

### EnableDepthMask

Habilita a escrita no Z-buffer.

```lua
EnableDepthMask() -> void
```

### DisableDepthMask

Desabilita a escrita no Z-buffer.

```lua
DisableDepthMask() -> void
```

### DisableTexture

Desabilita texturização (desenha cores sólidas).

```lua
DisableTexture(disable) -> void
```

**Parâmetros:**
- `disable` (bool): `true` para desabilitar texturas

### EnableLightMap

Habilita lightmapping.

```lua
EnableLightMap() -> void
```

### BindTexture

Vincula uma textura para renderização.

```lua
BindTexture(textureId) -> void
```

**Parâmetros:**
- `textureId` (number): ID da textura a ser vinculada

### LoadBitmap

Carrega uma textura de um arquivo.

```lua
LoadBitmap(path, id, filter, wrap, chk, full) -> int
```

**Parâmetros:**
- `path` (string): Caminho do arquivo de imagem
- `id` (number): ID da textura
- `filter` (number): Filtro de textura
- `wrap` (number): Modo de wrap
- `chk` (number): Flag de verificação
- `full` (number): Flag de caminho completo

**Retorno**: Status da operação (0 = sucesso).

### RenderBitmap

Renderiza uma imagem 2D.

```lua
RenderBitmap(id, x, y, w, h, u, v, uw, vh, scale, startScale, alpha) -> void
```

**Parâmetros:**
- `id` (number): ID da textura
- `x`, `y` (number): Posição na tela
- `w`, `h` (number): Largura e altura
- `u`, `v` (number): Coordenadas UV iniciais
- `uw`, `vh` (number): Tamanho UV
- `scale` (bool): Aplicar escala
- `startScale` (bool): Escala inicial
- `alpha` (number): Transparência (0.0 - 1.0)

### RenderImage

Versão simplificada de renderização de imagem.

```lua
RenderImage(id, x, y, w, h) -> void
```

### Color4f

Cria um valor de cor baseado em float.

```lua
Color4f(r, g, b, a) -> DWORD
```

**Parâmetros:**
- `r`, `g`, `b`, `a` (float): Componentes de cor (0.0 - 1.0)

**Retorno**: Valor de cor DWORD.

### RGBA

Cria um valor de cor RGBA padrão.

```lua
RGBA(r, g, b, a) -> DWORD
```

**Parâmetros:**
- `r`, `g`, `b`, `a` (number): Componentes de cor (0 - 255)

**Retorno**: Valor de cor DWORD.

## Text & UI

Funções para renderização de texto e interface de usuário.

### UIRenderText_SetFont

Define a fonte atual para renderização de texto.

```lua
UIRenderText_SetFont(fontHandle) -> void
```

**Parâmetros:**
- `fontHandle` (number): Handle da fonte

### UIRenderText_SetTextColor

Define a cor do texto.

```lua
UIRenderText_SetTextColor(r, g, b, a) -> void
```

**Parâmetros:**
- `r`, `g`, `b`, `a` (number): Componentes de cor (0 - 255)

### UIRenderText_SetBgColor

Define a cor de fundo do texto.

```lua
UIRenderText_SetBgColor(r, g, b, a) -> void
```

### UIRenderText_RenderText

Renderiza texto na tela.

```lua
UIRenderText_RenderText(x, y, text, w, h, sort) -> void
```

**Parâmetros:**
- `x`, `y` (number): Posição na tela
- `text` (string): Texto a ser renderizado
- `w`, `h` (number): Largura e altura da área de texto
- `sort` (number): Ordem de renderização

### RenderTipText

Renderiza um texto estilo tooltip.

```lua
RenderTipText(x, y, text) -> void
```

**Parâmetros:**
- `x`, `y` (number): Posição na tela
- `text` (string): Texto do tooltip

### IsWriteInterfaceOpen

Verifica se a interface de escrita (chat/input) está aberta.

```lua
IsWriteInterfaceOpen() -> bool
```

**Retorno**: `true` se a interface está aberta, `false` caso contrário.

## Object Management

Funções para gerenciar objetos do jogo.

### GetCharacter

Obtém um objeto de personagem (player, monster, NPC).

```lua
GetCharacter(index) -> GameCharacter
```

**Parâmetros:**
- `index` (number): Índice do personagem

**Retorno**: Objeto `GameCharacter` ou `nil`.

### GetModel

Obtém um objeto de modelo 3D.

```lua
GetModel(index) -> GameBMD
```

**Parâmetros:**
- `index` (number): Índice do modelo

**Retorno**: Objeto `GameBMD` ou `nil`.

## Funções Relacionadas

- [Input & Mouse](../Functions/README.md#-input--mouse) - Documentação detalhada de funções de input
- [Rendering & Graphics](../Functions/README.md#-rendering--graphics) - Documentação detalhada de renderização
- [Text & UI](../Functions/README.md#-text--ui) - Documentação detalhada de UI
- [Object Management](../Functions/README.md#-object-management) - Documentação detalhada de objetos

