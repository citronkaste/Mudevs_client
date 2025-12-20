# GetModel

Obtém um objeto de modelo 3D.

## Assinatura

```lua
GetModel(index) -> GameBMD
```

## Parâmetros

- `index` (number): Índice do modelo

## Retorno

`GameBMD` ou `nil` - O objeto de modelo se existir, ou `nil` se o índice for inválido ou o modelo não existir.

## Uso

Obtém um objeto de modelo 3D que permite manipular propriedades visuais como visibilidade, transparência, escala, etc.

## Exemplos

### Manipular Propriedades do Modelo

```lua
function BridgeFunction_OnInterfaceRender()
    local model = GetModel(0) -- Exemplo de índice
    if model then
        -- Alterar propriedades do modelo
        model.Visible = true
        model.Alpha = 0.8
        model.Scale = 1.5
        model.LightEnable = true
    end
end
```

### Fade In/Out

```lua
local fadeAlpha = 0.0
local fadingIn = true

function BridgeFunction_OnInterfaceRender()
    local model = GetModel(modelIndex)
    if model then
        -- Atualizar alpha
        if fadingIn then
            fadeAlpha = fadeAlpha + 0.01
            if fadeAlpha >= 1.0 then
                fadeAlpha = 1.0
                fadingIn = false
            end
        else
            fadeAlpha = fadeAlpha - 0.01
            if fadeAlpha <= 0.0 then
                fadeAlpha = 0.0
                fadingIn = true
            end
        end
        
        model.Alpha = fadeAlpha
    end
end
```

### Controlar Visibilidade

```lua
function BridgeFunction_OnInterfaceRender()
    local model = GetModel(modelIndex)
    if model then
        -- Toggle visibilidade com tecla
        if SEASON3B_IsPress(0x56) then -- VK_V
            model.Visible = not model.Visible
        end
    end
end
```

## Propriedades do Objeto Retornado

O objeto `GameBMD` possui as seguintes propriedades:

- `Visible` (bool): Flag de visibilidade
- `Alpha` (float): Transparência Alpha (0.0 - 1.0)
- `Scale` (float): Escala do modelo
- `Position` (Vector3): Posição (x, y, z)
- `Velocity` (float): Velocidade
- `Gravity` (float): Gravidade
- `AnimationFrame` (float): Frame atual da animação
- `PlaySpeed` (float): Velocidade da animação
- `LightEnable` (bool): Iluminação habilitada
- `ContrastEnable` (bool): Contraste habilitado

Veja [GameBMD](../04-Objetos-Game.md#gamebmd-model) para documentação completa.

## Notas Importantes

1. **Sempre valide o retorno**: `GetModel` pode retornar `nil` se o índice for inválido
2. **Manipulação visual**: Permite manipular propriedades visuais do modelo
3. **Performance**: Acessar propriedades é rápido, mas evite loops desnecessários
4. **Índice**: O índice geralmente é obtido de outros sistemas do jogo

## Funções Relacionadas

- [GetCharacter](GetCharacter.md) - Obtém objeto de personagem
- [Objetos do Jogo](../04-Objetos-Game.md) - Documentação completa dos objetos

