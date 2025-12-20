# Sistema de Pacotes

Este documento descreve o sistema completo de manipulação de pacotes de rede disponível na API Lua do Client.

## Visão Geral

O sistema de pacotes permite ler pacotes recebidos do servidor e criar pacotes customizados para enviar. Isso permite comunicação bidirecional entre cliente e servidor através de pacotes customizados.

## Objeto Packet

O objeto `Packet` é usado para ler e escrever dados de pacotes de rede. É idêntico ao `CPacket` do servidor.

### Criação

```lua
local packet = Packet()
```

Cria um novo objeto Packet vazio.

## Leitura de Pacotes

No hook `BridgeFunction_OnPacketRecv`, você recebe um objeto `Packet` que pode ser lido.

### ReadByte

Lê um byte (8 bits) do pacote.

```lua
local value = packet:ReadByte() -> number
```

**Retorno:** Valor de 0 a 255.

### ReadWord

Lê uma word (16 bits) do pacote.

```lua
local value = packet:ReadWord() -> number
```

**Retorno:** Valor de 0 a 65535.

### ReadDword

Lê um dword (32 bits) do pacote.

```lua
local value = packet:ReadDword() -> number
```

**Retorno:** Valor de 0 a 4294967295.

### ReadString

Lê uma string do pacote.

```lua
local value = packet:ReadString() -> string
```

**Retorno:** String lida do pacote.

**Nota:** A string geralmente é precedida por um byte ou word indicando seu tamanho.

## Escrita de Pacotes

Para criar pacotes customizados (geralmente para enviar ao servidor).

### WriteByte

Escreve um byte no pacote.

```lua
packet:WriteByte(value) -> void
```

**Parâmetros:**
- `value` (number): Valor de 0 a 255

### WriteWord

Escreve uma word no pacote.

```lua
packet:WriteWord(value) -> void
```

**Parâmetros:**
- `value` (number): Valor de 0 a 65535

### WriteDword

Escreve um dword no pacote.

```lua
packet:WriteDword(value) -> void
```

**Parâmetros:**
- `value` (number): Valor de 0 a 4294967295

### WriteString

Escreve uma string no pacote.

```lua
packet:WriteString(value) -> void
```

**Parâmetros:**
- `value` (string): String a ser escrita

**Nota:** Geralmente é necessário escrever o tamanho da string antes (byte ou word).

## BridgeFunction_OnPacketRecv

Hook chamado quando um pacote específico é recebido do servidor.

### Assinatura

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    -- Processar pacote
    return 0 -- ou 1 para consumir
end
```

### Parâmetros

- `index` (number): Índice do personagem relacionado
- `head` (number): Cabeçalho do pacote (header/opcode)
- `packet` (Packet): Objeto Packet com os dados

### Retorno

- `0`: Continua processamento normal do pacote
- `1`: Consome o pacote (bloqueia processamento padrão)

### Exemplo Básico

```lua
-- Constante do header customizado
local CUSTOM_HEADER = 0x1234

function BridgeFunction_OnPacketRecv(index, head, packet)
    -- Verificar se é nosso pacote customizado
    if head == CUSTOM_HEADER then
        -- Ler dados do pacote
        local subCode = packet:ReadByte()
        local message = packet:ReadString()
        
        -- Processar mensagem
        if subCode == 0x01 then
            -- Mostrar notificação
            UIRenderText_RenderText(100, 100, message, 300, 20, 1)
        end
        
        -- Consumir pacote (bloquear processamento padrão)
        return 1
    end
    
    -- Continuar processamento normal para outros pacotes
    return 0
end
```

## Exemplo: Sistema de Notificações

```lua
-- Headers customizados
local NOTIFICATION_HEADER = 0x1234
local NOTIFICATION_TYPE_INFO = 0x01
local NOTIFICATION_TYPE_WARNING = 0x02
local NOTIFICATION_TYPE_ERROR = 0x03

function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == NOTIFICATION_HEADER then
        local type = packet:ReadByte()
        local title = packet:ReadString()
        local message = packet:ReadString()
        
        -- Determinar cor baseado no tipo
        local r, g, b = 255, 255, 255 -- Padrão branco
        if type == NOTIFICATION_TYPE_INFO then
            r, g, b = 100, 150, 255 -- Azul
        elseif type == NOTIFICATION_TYPE_WARNING then
            r, g, b = 255, 200, 0 -- Amarelo
        elseif type == NOTIFICATION_TYPE_ERROR then
            r, g, b = 255, 0, 0 -- Vermelho
        end
        
        -- Mostrar notificação
        UIRenderText_SetTextColor(r, g, b, 255)
        UIRenderText_RenderText(100, 100, title, 400, 25, 10)
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(100, 130, message, 400, 20, 10)
        
        return 1
    end
    
    return 0
end
```

## Exemplo: Sistema de Dados Customizados

```lua
-- Header para dados de personagem customizados
local CUSTOM_CHAR_DATA_HEADER = 0x5678

function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == CUSTOM_CHAR_DATA_HEADER then
        -- Ler dados customizados
        local customLevel = packet:ReadDword()
        local customExp = packet:ReadDword()
        local customPoints = packet:ReadWord()
        local customName = packet:ReadString()
        
        -- Armazenar dados (em variável global ou estrutura)
        customPlayerData = {
            level = customLevel,
            exp = customExp,
            points = customPoints,
            name = customName
        }
        
        -- Atualizar UI com dados customizados
        -- ...
        
        return 1
    end
    
    return 0
end
```

## Exemplo: Múltiplos Pacotes

```lua
-- Múltiplos headers
local HEADER_CHAT = 0x1001
local HEADER_ITEM = 0x1002
local HEADER_SKILL = 0x1003

function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == HEADER_CHAT then
        local channel = packet:ReadByte()
        local sender = packet:ReadString()
        local message = packet:ReadString()
        
        -- Processar chat customizado
        ProcessCustomChat(channel, sender, message)
        return 1
        
    elseif head == HEADER_ITEM then
        local itemId = packet:ReadWord()
        local itemLevel = packet:ReadByte()
        local itemOptions = packet:ReadDword()
        
        -- Processar item customizado
        ProcessCustomItem(itemId, itemLevel, itemOptions)
        return 1
        
    elseif head == HEADER_SKILL then
        local skillId = packet:ReadWord()
        local skillLevel = packet:ReadByte()
        
        -- Processar skill customizado
        ProcessCustomSkill(skillId, skillLevel)
        return 1
    end
    
    return 0
end
```

## Envio de Pacotes

**Nota:** O envio de pacotes geralmente requer uma função específica do cliente que pode não estar disponível na API Lua padrão. Consulte a documentação do seu cliente específico.

**Exemplo conceitual:**
```lua
function SendCustomPacket(header, packet)
    -- Função específica do cliente (pode variar)
    -- SendPacketToServer(header, packet)
end

-- Criar e enviar pacote
local packet = Packet()
packet:WriteByte(0x01) -- SubCode
packet:WriteString("Mensagem customizada")
SendCustomPacket(0x1234, packet)
```

## Boas Práticas

1. **Use constantes para headers**: Defina constantes para headers de pacotes customizados
2. **Valide dados antes de ler**: Sempre verifique se há dados suficientes no pacote
3. **Leia na ordem correta**: Leia os dados na mesma ordem que foram escritos no servidor
4. **Consuma pacotes quando necessário**: Retorne `1` para bloquear processamento padrão
5. **Trate erros**: Use `pcall` para proteger contra erros de leitura
6. **Documente formatos**: Documente o formato de cada pacote customizado

## Tratamento de Erros

```lua
function BridgeFunction_OnPacketRecv(index, head, packet)
    if head == CUSTOM_HEADER then
        local success, error = pcall(function()
            -- Ler dados do pacote
            local subCode = packet:ReadByte()
            local message = packet:ReadString()
            
            -- Processar
            ProcessMessage(subCode, message)
        end)
        
        if not success then
            -- Erro ao processar pacote
            -- Log de erro (se disponível)
            return 1 -- Consumir mesmo com erro
        end
        
        return 1
    end
    
    return 0
end
```

## Funções Relacionadas

- [BridgeFunction_OnPacketRecv](../Functions/BridgeFunction_OnPacketRecv.md) - Documentação detalhada
- [Packet](04-Objetos-Game.md#packet) - Documentação do objeto Packet
- [Bridge Functions](05-Bridge-Functions.md) - Sistema completo de hooks

