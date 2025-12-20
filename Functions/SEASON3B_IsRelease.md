# SEASON3B_IsRelease

Verifica se uma tecla foi solta no frame atual.

## Assinatura

```lua
SEASON3B_IsRelease(key) -> bool
```

## Parâmetros

- `key` (number): Código VK da tecla (ex: `0x4D` para M)

## Retorno

`bool` - `true` se a tecla foi solta no frame atual, `false` caso contrário.

## Características

- Retorna `true` apenas uma vez quando a tecla é solta
- Útil para detectar quando o jogador para de pressionar uma tecla
- Deve ser chamado dentro de `BridgeFunction_OnInterfaceRender`

## Exemplos

### Detectar Soltura de Tecla

```lua
function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsRelease(0x1B) then -- VK_ESCAPE
        -- Tecla ESC foi solta
        print("ESC solto")
    end
end
```

### Toggle ao Soltar

```lua
local holdingSpace = false

function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsPress(0x20) then -- VK_SPACE
        holdingSpace = true
    end
    
    if SEASON3B_IsRelease(0x20) then -- VK_SPACE
        holdingSpace = false
        -- Executar ação quando soltar
        print("Espaço solto - executar ação")
    end
end
```

### Sistema de Hold

```lua
local holdingKey = false

function BridgeFunction_OnInterfaceRender()
    if SEASON3B_IsPress(0x4D) then -- VK_M
        holdingKey = true
        print("Tecla M pressionada")
    end
    
    if SEASON3B_IsRelease(0x4D) then -- VK_M
        holdingKey = false
        print("Tecla M solta")
    end
    
    -- Fazer algo enquanto está pressionado
    if holdingKey then
        -- ...
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
    
    if SEASON3B_IsRelease(0x4D) then
        print("M solto")
    end
    
    if SEASON3B_IsRepeat(0x4D) then
        print("M mantido pressionado")
    end
    
    if SEASON3B_IsNone(0x4D) then
        -- M não está pressionado
    end
end
```

## Notas Importantes

1. **Chamada no OnInterfaceRender**: Esta função deve ser chamada dentro de `BridgeFunction_OnInterfaceRender`
2. **Uma vez por frame**: Retorna `true` apenas uma vez quando a tecla é solta
3. **Use constantes**: Defina constantes para códigos VK comuns
4. **Performance**: A função é muito rápida, pode ser chamada a cada frame

## Funções Relacionadas

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Verifica se tecla foi pressionada
- [SEASON3B_IsRepeat](SEASON3B_IsRepeat.md) - Verifica se tecla está sendo mantida
- [SEASON3B_IsNone](SEASON3B_IsNone.md) - Verifica se tecla não está pressionada
- [Enumerações](../02-Enumeracoes.md) - Códigos VK completos
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

