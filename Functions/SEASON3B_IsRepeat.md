# SEASON3B_IsRepeat

Verifica se uma tecla está sendo mantida pressionada (repetição).

## Assinatura

```lua
SEASON3B_IsRepeat(key) -> bool
```

## Parâmetros

- `key` (number): Código VK da tecla (ex: `0x4D` para M)

## Retorno

`bool` - `true` se a tecla está sendo mantida pressionada, `false` caso contrário.

## Características

- Retorna `true` continuamente enquanto a tecla estiver pressionada
- Útil para movimento contínuo, scroll, ações repetitivas
- Deve ser chamado dentro de `BridgeFunction_OnInterfaceRender`

## Exemplos

### Movimento Contínuo

```lua
function BridgeFunction_OnInterfaceRender()
    -- Movimento contínuo com setas
    if SEASON3B_IsRepeat(0x25) then -- VK_LEFT
        -- Mover para esquerda continuamente
        print("Movendo para esquerda")
    elseif SEASON3B_IsRepeat(0x27) then -- VK_RIGHT
        -- Mover para direita continuamente
        print("Movendo para direita")
    end
    
    if SEASON3B_IsRepeat(0x26) then -- VK_UP
        -- Mover para cima continuamente
        print("Movendo para cima")
    elseif SEASON3B_IsRepeat(0x28) then -- VK_DOWN
        -- Mover para baixo continuamente
        print("Movendo para baixo")
    end
end
```

### Scroll Contínuo

```lua
local scrollPosition = 0

function BridgeFunction_OnInterfaceRender()
    -- Scroll com Page Up/Down
    if SEASON3B_IsRepeat(0x21) then -- VK_PRIOR (Page Up)
        scrollPosition = scrollPosition - 1
    elseif SEASON3B_IsRepeat(0x22) then -- VK_NEXT (Page Down)
        scrollPosition = scrollPosition + 1
    end
    
    -- Renderizar conteúdo com scroll
    -- ...
end
```

### Ação Repetitiva

```lua
function BridgeFunction_OnInterfaceRender()
    -- Ação que se repete enquanto tecla está pressionada
    if SEASON3B_IsRepeat(0x20) then -- VK_SPACE
        -- Executar ação continuamente
        -- (ex: atirar, correr, etc.)
    end
end
```

## Diferença entre IsPress, IsRelease, IsRepeat e IsNone

- **IsPress**: Retorna `true` uma vez quando a tecla é pressionada
- **IsRelease**: Retorna `true` uma vez quando a tecla é solta
- **IsRepeat**: Retorna `true` continuamente enquanto a tecla está pressionada
- **IsNone**: Retorna `true` quando a tecla não está pressionada

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsPress(0x4D) then
        -- Executa uma vez quando M é pressionado
        print("M pressionado")
    end
    
    if SEASON3B_IsRepeat(0x4D) then
        -- Executa continuamente enquanto M está pressionado
        print("M mantido pressionado")
    end
end
```

## Notas Importantes

1. **Chamada no OnInterfaceRender**: Esta função deve ser chamada dentro de `BridgeFunction_OnInterfaceRender`
2. **Contínuo**: Retorna `true` continuamente enquanto a tecla está pressionada
3. **Use para movimento**: Ideal para movimento contínuo e ações repetitivas
4. **Performance**: A função é muito rápida, mas evite lógica pesada dentro do loop

## Funções Relacionadas

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Verifica se tecla foi pressionada
- [SEASON3B_IsRelease](SEASON3B_IsRelease.md) - Verifica se tecla foi solta
- [SEASON3B_IsNone](SEASON3B_IsNone.md) - Verifica se tecla não está pressionada
- [Enumerações](../02-Enumeracoes.md) - Códigos VK completos
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

