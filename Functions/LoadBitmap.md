# LoadBitmap

Carrega uma textura de um arquivo de imagem.

## Assinatura

```lua
LoadBitmap(path, id, filter, wrap, chk, full) -> int
```

## Parâmetros

- `path` (string): Caminho do arquivo de imagem
- `id` (int): ID único da textura (para referência posterior)
- `filter` (int): Filtro de textura (0 = sem filtro, 1 = linear)
- `wrap` (int): Modo de wrap (0 = clamp, 1 = repeat)
- `chk` (int): Flag de verificação (0 ou 1)
- `full` (int): Flag de caminho completo (0 = relativo, 1 = absoluto)

## Retorno

`int` - Status da operação (0 = sucesso, outros = erro).

## Uso

Carrega uma textura de um arquivo de imagem para uso posterior. Ideal para carregar recursos na inicialização.

## Exemplos

### Carregar Textura na Inicialização

```lua
local buttonTextureId = 100
local backgroundTextureId = 101

function BridgeFunction_OnLoadInterface()
    -- Carregar texturas
    local status1 = LoadBitmap("Interface\\CustomUI\\button.bmp", buttonTextureId, 1, 0, 0, 1)
    local status2 = LoadBitmap("Interface\\CustomUI\\background.bmp", backgroundTextureId, 1, 0, 0, 1)
    
    if status1 == 0 and status2 == 0 then
        -- Texturas carregadas com sucesso
        print("Texturas carregadas")
    else
        -- Erro ao carregar
        print("Erro ao carregar texturas")
    end
end

function BridgeFunction_OnInterfaceRender()
    -- Usar texturas carregadas
    RenderImage(buttonTextureId, 100, 100, 200, 50)
    RenderImage(backgroundTextureId, 0, 0, 800, 600)
end
```

### Múltiplas Texturas

```lua
local textures = {
    button = 100,
    icon = 101,
    background = 102
}

function BridgeFunction_OnLoadInterface()
    -- Carregar múltiplas texturas
    LoadBitmap("Interface\\button.bmp", textures.button, 1, 0, 0, 1)
    LoadBitmap("Interface\\icon.bmp", textures.icon, 1, 0, 0, 1)
    LoadBitmap("Interface\\background.bmp", textures.background, 1, 0, 0, 1)
end
```

## Parâmetros Detalhados

### filter
- `0`: Sem filtro (pixelado)
- `1`: Filtro linear (suave)

### wrap
- `0`: Clamp (não repete)
- `1`: Repeat (repetição)

### full
- `0`: Caminho relativo (relativo à pasta do jogo)
- `1`: Caminho absoluto (caminho completo)

## Notas Importantes

1. **Carregue na inicialização**: Use `BridgeFunction_OnLoadInterface` para carregar recursos
2. **IDs únicos**: Use IDs únicos para cada textura
3. **Verifique status**: Sempre verifique o retorno para garantir que a textura foi carregada
4. **Caminhos**: Use caminhos relativos quando possível

## Funções Relacionadas

- [RenderBitmap](RenderBitmap.md) - Renderiza textura carregada
- [RenderImage](RenderImage.md) - Renderiza textura simplificada
- [BindTexture](BindTexture.md) - Vincula textura
- [BridgeFunction_OnLoadInterface](BridgeFunction_OnLoadInterface.md) - Hook de inicialização
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

