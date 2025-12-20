# IsWriteInterfaceOpen

Verifica se a interface de escrita (chat/input) está aberta.

## Assinatura

```lua
IsWriteInterfaceOpen() -> bool
```

## Parâmetros

Nenhum.

## Retorno

`bool` - `true` se a interface de escrita está aberta, `false` caso contrário.

## Uso

Verifica se o jogador está digitando no chat ou em uma interface de input. Útil para desabilitar certas funcionalidades quando o jogador está digitando.

## Exemplos

### Desabilitar Input Customizado Durante Chat

```lua
function BridgeFunction_OnInterfaceRender()
    -- Não processar input customizado se chat está aberto
    if IsWriteInterfaceOpen() then
        return
    end
    
    -- Processar input customizado apenas quando chat está fechado
    if SEASON3B_IsPress(0x4D) then -- VK_M
        -- Fazer algo
    end
end
```

### Mostrar Indicador

```lua
function BridgeFunction_OnInterfaceRender()
    if IsWriteInterfaceOpen() then
        -- Mostrar indicador de que está digitando
        UIRenderText_SetTextColor(255, 255, 0, 255)
        UIRenderText_RenderText(10, 10, "Digitando...", 150, 20, 1)
    end
end
```

### Pausar UI Durante Input

```lua
function BridgeFunction_OnInterfaceRender()
    -- Pausar UI customizada durante input
    if IsWriteInterfaceOpen() then
        -- Não renderizar UI customizada
        return
    end
    
    -- Renderizar UI normalmente
    -- ...
end
```

## Notas Importantes

1. **Chat/Input**: Verifica se qualquer interface de escrita está aberta
2. **Desabilitar funcionalidades**: Use para desabilitar funcionalidades durante input
3. **Performance**: Função muito rápida, pode ser chamada a cada frame
4. **UX**: Melhora a experiência do usuário evitando conflitos de input

## Funções Relacionadas

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Verifica se tecla foi pressionada
- [SetBlockInput](SetBlockInput.md) - Bloqueia input do jogo
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

