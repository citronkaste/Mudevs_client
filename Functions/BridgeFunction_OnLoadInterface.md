# BridgeFunction_OnLoadInterface

Chamado quando a interface está sendo inicializada.

## Assinatura

```lua
function BridgeFunction_OnLoadInterface()
    -- Sua lógica de inicialização aqui
end
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Ideal para:
- Carregar texturas e recursos
- Inicializar variáveis globais
- Configurar estados iniciais
- Preparar dados para uso posterior

## Exemplos

### Carregar Texturas

```lua
local buttonTextureId = 100
local backgroundTextureId = 101
local iconTextureId = 102

function BridgeFunction_OnLoadInterface()
    -- Carregar texturas customizadas
    local status1 = LoadBitmap("Interface\\CustomUI\\button.bmp", buttonTextureId, 1, 0, 0, 1)
    local status2 = LoadBitmap("Interface\\CustomUI\\background.bmp", backgroundTextureId, 1, 0, 0, 1)
    local status3 = LoadBitmap("Interface\\CustomUI\\icon.bmp", iconTextureId, 1, 0, 0, 1)
    
    if status1 == 0 and status2 == 0 and status3 == 0 then
        -- Texturas carregadas com sucesso
        print("Recursos carregados com sucesso")
    else
        -- Erro ao carregar
        print("Erro ao carregar recursos")
    end
end
```

### Inicializar Variáveis Globais

```lua
-- Variáveis globais
local uiVisible = false
local menuOpen = false
local customData = {}

function BridgeFunction_OnLoadInterface()
    -- Inicializar variáveis
    uiVisible = true
    menuOpen = false
    customData = {
        level = 0,
        exp = 0,
        points = 0
    }
    
    print("Sistema inicializado")
end
```

### Configurar Estados Iniciais

```lua
local config = {
    showFPS = false,
    showHP = true,
    showMP = true,
    theme = "dark"
}

function BridgeFunction_OnLoadInterface()
    -- Carregar configurações (exemplo)
    -- config = LoadConfig() -- Se disponível
    
    -- Configurar estados iniciais
    print("Configurações carregadas")
end
```

### Preparar Dados

```lua
local itemDatabase = {}

function BridgeFunction_OnLoadInterface()
    -- Preparar dados (exemplo)
    itemDatabase = {
        [1] = {name = "Espada", damage = 100},
        [2] = {name = "Escudo", defense = 50},
        -- ...
    }
    
    print("Banco de dados preparado")
end
```

## Boas Práticas

### 1. Carregar Recursos

```lua
function BridgeFunction_OnLoadInterface()
    -- Carregar todos os recursos necessários
    LoadBitmap("path1", id1, 1, 0, 0, 1)
    LoadBitmap("path2", id2, 1, 0, 0, 1)
    -- ...
end
```

### 2. Validação

```lua
function BridgeFunction_OnLoadInterface()
    local success = true
    
    -- Carregar recursos e verificar
    if LoadBitmap("path", id, 1, 0, 0, 1) ~= 0 then
        success = false
    end
    
    if not success then
        print("Erro ao carregar recursos")
    end
end
```

### 3. Organização

```lua
-- Agrupar recursos relacionados
local uiTextures = {
    button = 100,
    background = 101,
    icon = 102
}

function BridgeFunction_OnLoadInterface()
    -- Carregar grupo de recursos
    LoadBitmap("UI\\button.bmp", uiTextures.button, 1, 0, 0, 1)
    LoadBitmap("UI\\background.bmp", uiTextures.background, 1, 0, 0, 1)
    LoadBitmap("UI\\icon.bmp", uiTextures.icon, 1, 0, 0, 1)
end
```

## Notas Importantes

1. **Chamado uma vez**: Esta função é chamada apenas uma vez durante a inicialização
2. **Carregar recursos**: Use para carregar texturas, dados e recursos
3. **Inicialização**: Ideal para configurar estados iniciais
4. **Erros**: Trate erros ao carregar recursos

## Funções Relacionadas

- [LoadBitmap](LoadBitmap.md) - Carrega textura
- [BridgeFunction_OnInterfaceRender](BridgeFunction_OnInterfaceRender.md) - Loop de renderização
- [Bridge Functions](../05-Bridge-Functions.md) - Documentação completa dos hooks

