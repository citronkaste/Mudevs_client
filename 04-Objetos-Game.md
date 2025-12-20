# Objetos do Jogo

Este documento descreve os objetos principais expostos pela API Lua do Client.

## Visão Geral

Os objetos do jogo são entidades C++ expostas a Lua através da biblioteca sol2. Eles representam elementos do jogo como personagens, modelos 3D e itens.

## GameCharacter

Representa um personagem no jogo (player, monster, NPC). Acessível via `GetCharacter(index)` ou através da variável global `Hero` (jogador local).

### Propriedades

| Propriedade | Tipo | Descrição |
| :---------- | :--- | :-------- |
| `ID` | `string` | Nome/ID do personagem |
| `Class` | `int` | Código da classe do personagem |
| `Skin` | `int` | ID do modelo/skin atual |
| `CtlCode` | `int` | Código de controle (GM/Normal) |
| `Level` | `int` | Nível do personagem |
| `GuildStatus` | `int` | Configurações de posição na guild |
| `PK` | `int` | Nível/Status PK |
| `Dead` | `int` | 1 se morto, 0 caso contrário |
| `Run` | `int` | 1 se está correndo |
| `PositionX` | `int` | Coordenada X (Mundo) |
| `PositionY` | `int` | Coordenada Y (Mundo) |
| `TargetX` | `int` | X do alvo (Movimento) |
| `TargetY` | `int` | Y do alvo (Movimento) |
| `MaxHP` | `float` | Vida máxima |
| `CurHP` | `float` | Vida atual |
| `MoveSpeed` | `float` | Velocidade de movimento |
| `Rot` | `float` | Rotação |
| `SafeZone` | `int` | 1 se está em Safe Zone |
| `Wing` | `int` | ID do item de asa (Visual) |
| `Helper` | `int` | ID do pet/helper (Visual) |
| `CurrentSkill` | `int` | ID da habilidade em uso |
| `MonsterIndex` | `int` | Índice da tabela de monstros |
| `Kind` | `int` | Tipo de entidade (Player/Monster/NPC) |

### Exemplos

```lua
-- Acessar jogador local
if Hero then
    local level = Hero.Level
    local name = Hero.ID
    local hp = Hero.CurHP / Hero.MaxHP * 100
end

-- Acessar personagem por índice
local character = GetCharacter(index)
if character then
    if character.Kind == 0 then -- Player
        -- Fazer algo com jogador
    elseif character.Kind == 1 then -- Monster
        -- Fazer algo com monstro
    end
end
```

## GameBMD (GameObject/Model)

Representa um objeto visual/modelo 3D no motor. Acessível via `GetModel(index)`.

### Propriedades

| Propriedade | Tipo | Descrição |
| :---------- | :--- | :-------- |
| `Visible` | `bool` | Flag de visibilidade |
| `Alpha` | `float` | Transparência Alpha (0.0 - 1.0) |
| `Scale` | `float` | Escala do modelo |
| `Position` | `Vector3` | Posição (x, y, z) |
| `Velocity` | `float` | Velocidade |
| `Gravity` | `float` | Gravidade |
| `AnimationFrame` | `float` | Frame atual da animação |
| `PlaySpeed` | `float` | Velocidade da animação |
| `LightEnable` | `bool` | Iluminação habilitada |
| `ContrastEnable` | `bool` | Contraste habilitado |

### Exemplos

```lua
local model = GetModel(index)
if model then
    model.Visible = true
    model.Alpha = 0.8
    model.Scale = 1.5
end
```

## GameItem

Representa um item no cliente.

### Propriedades

| Propriedade | Tipo | Descrição |
| :---------- | :--- | :-------- |
| `Type` | `int` | ID do item (Section*512 + Index) |
| `Level` | `int` | Nível do item |
| `Durability` | `int` | Durabilidade atual |
| `DamageMin` | `int` | Dano mínimo |
| `DamageMax` | `int` | Dano máximo |
| `RequireLevel` | `int` | Nível necessário |
| `SocketCount` | `int` | Número de sockets |
| `Option1` | `int` | Opção Excellent/Skill |

### Exemplos

```lua
-- Acessar item selecionado
if SelectedItem then
    local itemLevel = SelectedItem.Level
    local itemType = SelectedItem.Type
end
```

## Packet

Usado para construir e ler pacotes de rede. Idêntico ao `CPacket` do servidor.

### Métodos

#### Construtor

```lua
Packet() -> Packet
```

Cria um novo objeto Packet.

#### Escrita

```lua
packet:WriteByte(val) -> void
packet:WriteWord(val) -> void
packet:WriteDword(val) -> void
packet:WriteString(val) -> void
```

Escreve dados no pacote.

**Parâmetros:**
- `val`: Valor a ser escrito (byte, word, dword ou string)

#### Leitura

```lua
packet:ReadByte() -> number
packet:ReadWord() -> number
packet:ReadDword() -> number
packet:ReadString() -> string
```

Lê dados do pacote.

**Retorno**: Valor lido do tipo correspondente.

### Exemplos

```lua
-- Criar e enviar pacote (no hook OnPacketRecv)
function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == 0x1234 then
        local subCode = packet:ReadByte()
        local message = packet:ReadString()
        
        -- Criar resposta
        local response = Packet()
        response:WriteByte(0x01) -- Success
        response:WriteString("OK")
        
        -- Enviar resposta (função específica do cliente)
        -- SendPacket(index, 0x5678, response)
    end
end
```

## Variáveis Globais

Alguns objetos estão disponíveis como variáveis globais:

| Variável | Tipo | Descrição |
| :------- | :--- | :-------- |
| `Hero` | `GameCharacter` | Objeto do jogador local |
| `MouseX` | `int` | Posição X atual do mouse |
| `MouseY` | `int` | Posição Y atual do mouse |
| `MouseLButton` | `int` | Estado do botão esquerdo do mouse |
| `MouseRButton` | `int` | Estado do botão direito do mouse |
| `SelectedCharacter` | `GameCharacter` | Personagem atualmente selecionado |
| `SelectedItem` | `GameItem` | Item atualmente selecionado |

### Exemplos

```lua
function BridgeFunction_OnInterfaceRender()
    -- Usar Hero diretamente
    if Hero then
        local text = string.format("Level: %d", Hero.Level)
        UIRenderText_RenderText(10, 10, text, 200, 20, 1)
    end
    
    -- Usar posição do mouse
    local mouseText = string.format("Mouse: %d, %d", MouseX, MouseY)
    UIRenderText_RenderText(MouseX + 10, MouseY + 10, mouseText, 150, 20, 1)
end
```

## Notas Importantes

1. **Validação**: Sempre valide se os objetos não são `nil` antes de usar
2. **Propriedades somente leitura**: Algumas propriedades podem ser somente leitura no cliente
3. **Performance**: Acessar propriedades é rápido, mas evite loops desnecessários
4. **Thread Safety**: Os objetos são acessíveis apenas no thread principal do cliente

## Funções Relacionadas

- [GetCharacter](../Functions/GetCharacter.md) - Obtém objeto de personagem
- [GetModel](../Functions/GetModel.md) - Obtém objeto de modelo
- [Variáveis Globais](10-Variaveis-Globais.md) - Documentação completa de variáveis globais
- [Bridge Functions](05-Bridge-Functions.md) - Hooks que usam esses objetos

