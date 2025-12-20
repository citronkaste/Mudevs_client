# SEASON3B_IsNone

Verifica se uma tecla não está sendo pressionada.

## Assinatura

```lua
SEASON3B_IsNone(key) -> bool
```

## Parâmetros

- `key` (number): Código VK da tecla (ex: `0x4D` para M)

## Retorno

`bool` - `true` se a tecla não está pressionada, `false` caso contrário.

## Características

- Retorna `true` quando a tecla não está sendo pressionada
- Útil para resetar estados, detectar quando uma ação para
- Deve ser chamado dentro de `BridgeFunction_OnInterfaceRender`

## Exemplos

### Resetar Estado

```lua
local isRunning = false

function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsPress(0x20) then -- VK_SPACE
        isRunning = true
    end
    
    if SEASON3B_IsNone(0x20) then -- VK_SPACE
        isRunning = false
        -- Resetar estado quando tecla não está pressionada
    end
end
```

### Detectar Quando Ação Para

```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsNone(0x4D) then -- VK_M
        -- Tecla M não está pressionada
        -- Executar ação quando para de pressionar
    end
end
```

### Estado de Tecla

```lua
function BridgeFunction_OnInterfaceRender()
    -- Verificar estado de múltiplas teclas
    if SEASON3B_IsNone(0x20) and SEASON3B_IsNone(0x4D) then
        -- Nenhuma tecla está pressionada
        -- Estado padrão
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
        print("M pressionado")
    end
    
    if SEASON3B_IsRepeat(0x4D) then
        print("M mantido pressionado")
    end
    
    if SEASON3B_IsNone(0x4D) then
        print("M não está pressionado")
    end
end
```

## Notas Importantes

1. **Chamada no OnInterfaceRender**: Esta função deve ser chamada dentro de `BridgeFunction_OnInterfaceRender`
2. **Estado padrão**: Retorna `true` quando a tecla está no estado padrão (não pressionada)
3. **Use para resetar**: Ideal para resetar estados quando uma tecla não está sendo usada
4. **Performance**: A função é muito rápida, pode ser chamada a cada frame

## Funções Relacionadas

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Verifica se tecla foi pressionada
- [SEASON3B_IsRelease](SEASON3B_IsRelease.md) - Verifica se tecla foi solta
- [SEASON3B_IsRepeat](SEASON3B_IsRepeat.md) - Verifica se tecla está sendo mantida
- [Enumerações](../02-Enumeracoes.md) - Códigos VK completos
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

