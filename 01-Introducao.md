# Introdução e Princípios de Design

## Visão Geral

Esta documentação descreve a API Lua disponível para scripting no cliente Mu Online. O sistema permite criar scripts personalizados que interagem com o motor do jogo (C++) através de uma interface segura e poderosa, permitindo renderização customizada de UI, manipulação de input e processamento de pacotes de rede.

## Princípios de Design

### 1. Baseado em sol2

A API utiliza a biblioteca `sol2` para vincular C++ com Lua, oferecendo uma interface segura e potente. Isso permite:

- **Tipagem segura**: Validação automática de tipos de parâmetros
- **Gerenciamento de memória**: Automático e seguro
- **Performance**: Overhead mínimo na comunicação entre Lua e C++

### 2. Orientado a Objetos

O sistema expõe objetos chave do jogo como entidades de primeira classe:

- `Hero` - Representa o jogador local
- `GameCharacter` - Representa um personagem (player, monster, NPC)
- `GameBMD` - Representa um modelo 3D
- `GameItem` - Representa um item do jogo
- `Packet` - Representa um pacote de rede

### 3. Renderização em Tempo Real

O sistema permite renderização customizada através do hook `BridgeFunction_OnInterfaceRender`, que é chamado a cada frame do jogo. Isso permite:

- Criar interfaces de usuário personalizadas
- Renderizar texto e imagens customizadas
- Manipular estados de renderização (alpha, depth, etc.)

**Exemplo básico:**
```lua
function BridgeFunction_OnInterfaceRender()
    -- Renderizar texto customizado
    UIRenderText_SetTextColor(255, 255, 0, 255) -- Amarelo
    UIRenderText_RenderText(100, 100, "Minha UI Customizada", 200, 20, 1)
end
```

### 4. Event-Driven (Baseado em Eventos)

O sistema se baseia em *hooks* ou *callbacks* que são executados em resposta a eventos específicos do jogo:

- `OnLoadInterface` - Quando a UI está sendo inicializada
- `OnInterfaceRender` - Chamado a cada frame para renderização
- `OnPacketRecv` - Quando um pacote específico é recebido

### 5. Input Handling

O sistema fornece funções para capturar input do usuário:

- Mouse (cliques, posição, hover)
- Teclado (pressionamento, release, repeat)
- Bloqueio de input para UI customizada

## Estrutura da Documentação

A documentação está organizada da seguinte forma:

1. **Funções Globais**: Funções de utilidade acessíveis de qualquer parte de um script
2. **Enumerações (Enums)**: Constantes globais que representam valores fixos do jogo
3. **Tipos de Dados (Userdata)**: Descrição dos objetos C++ expostos a Lua
4. **Hooks do Jogo**: Funções especiais que o Client chama em momentos chave
5. **Variáveis Globais**: Variáveis globais disponíveis (Hero, MouseX, etc.)

## Convenções de Nomenclatura

- **Funções globais**: `PascalCase` (ex: `GetCharacter`, `RenderBitmap`)
- **Objetos**: `camelCase` (ex: `Hero.Level`, `character.ID`)
- **Constantes**: `UPPER_SNAKE_CASE` (ex: `VK_M`, `VK_SPACE`)
- **Bridge Functions**: `BridgeFunction_On...` (ex: `BridgeFunction_OnInterfaceRender`)

## Diferenças entre Client e Server

### Client-Side
- Foco em renderização e UI
- Manipulação de input do usuário
- Processamento de pacotes recebidos
- Acesso limitado a dados do jogo (apenas visualização)

### Server-Side
- Foco em lógica de jogo
- Manipulação de dados do servidor
- Processamento completo de eventos
- Acesso completo aos dados do jogo

## Próximos Passos

- Leia sobre [Enumerações e Constantes](02-Enumeracoes.md)
- Explore as [Funções Globais](03-Funcoes-Globais.md)
- Entenda os [Objetos do Jogo](04-Objetos-Game.md)
- Aprenda sobre [Bridge Functions](05-Bridge-Functions.md)

