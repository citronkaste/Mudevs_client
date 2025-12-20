# SEASON3B_IsPress

Verifica se uma tecla foi pressionada no frame atual.

## Assinatura

```lua
SEASON3B_IsPress(key) -> bool
```

## Parâmetros

- `key` (number): Código VK da tecla (ex: `0x4D` para M)

## Retorno

`bool` - `true` se a tecla foi pressionada no frame atual, `false` caso contrário.

## Características

- Retorna `true` apenas uma vez por pressionamento
- Útil para toggles, atalhos, ações únicas
- Deve ser chamado dentro de `BridgeFunction_OnInterfaceRender`

## Códigos VK Comuns

| Código | Tecla |
| :----- | :---- |
| `0x4D` | M |
| `0x1B` | ESC |
| `0x20` | Espaço |
| `0x0D` | Enter |
| `0x25` | Seta Esquerda |
| `0x26` | Seta Cima |
| `0x27` | Seta Direita |
| `0x28` | Seta Baixo |
| `0x70` | F1 |
| `0x7B` | F12 |

Veja [02-Enumeracoes.md](../02-Enumeracoes.md) para lista completa.

## Exemplos

### Toggle de UI

```lua
local uiVisible = false

function BridgeFunction_OnInterfaceRender()
    -- Toggle UI com tecla M
    if SEASON3B_IsPress(0x4D) then -- VK_M
        uiVisible = not uiVisible
    end
    
    if uiVisible then
        -- Renderizar UI
        UIRenderText_RenderText(10, 10, "UI Ativa", 100, 20, 1)
    end
end
```

### Múltiplas Teclas

```lua
function BridgeFunction_OnInterfaceRender()
    -- Fechar com ESC
    if SEASON3B_IsPress(0x1B) then -- VK_ESCAPE
        -- Fechar menu, etc.
    end
    
    -- Abrir com F1
    if SEASON3B_IsPress(0x70) then -- VK_F1
        -- Abrir menu de ajuda
    end
end
```

### Atalhos com Modificadores

```lua
function BridgeFunction_OnInterfaceRender()
    -- Atalho Ctrl+S (conceitual, pode variar)
    if SEASON3B_IsPress(0x11) and SEASON3B_IsPress(0x53) then -- Ctrl + S
        -- Salvar algo
        print("Salvando...")
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
        -- Útil para movimento contínuo
    end
end
```

## Notas Importantes

1. **Chamada no OnInterfaceRender**: Esta função deve ser chamada dentro de `BridgeFunction_OnInterfaceRender`
2. **Uma vez por frame**: Retorna `true` apenas uma vez por pressionamento
3. **Use constantes**: Defina constantes para códigos VK comuns
4. **Performance**: A função é muito rápida, pode ser chamada a cada frame

## Funções Relacionadas

- [SEASON3B_IsRelease](SEASON3B_IsRelease.md) - Verifica se tecla foi solta
- [SEASON3B_IsRepeat](SEASON3B_IsRepeat.md) - Verifica se tecla está sendo mantida
- [SEASON3B_IsNone](SEASON3B_IsNone.md) - Verifica se tecla não está pressionada
- [SetBlockInput](SetBlockInput.md) - Bloqueia input do jogo
- [Enumerações](../02-Enumeracoes.md) - Códigos VK completos
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

