# SetBlockInput

Bloqueia ou desbloqueia o input do jogo.

## Assinatura

```lua
SetBlockInput(block) -> void
```

## Parâmetros

- `block` (bool): `true` para bloquear input do jogo, `false` para desbloquear

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Útil quando você tem uma UI modal que deve capturar todo o input, impedindo que o jogador interaja com o jogo enquanto a UI está aberta.

## Exemplos

### Modal com Bloqueio de Input

```lua
local modalOpen = false

function BridgeFunction_OnInterfaceRender()
    if modalOpen then
        -- Bloquear input do jogo
        SetBlockInput(true)
        
        -- Renderizar modal
        UIRenderText_SetBgColor(0, 0, 0, 200)
        UIRenderText_RenderText(100, 100, "", 400, 300, 10)
        
        -- Título
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(120, 120, "Modal Aberto", 360, 25, 11)
        
        -- Fechar modal com ESC
        if SEASON3B_IsPress(0x1B) then -- VK_ESCAPE
            modalOpen = false
            SetBlockInput(false)
        end
    end
end
```

### Menu de Opções

```lua
local menuVisible = false

function BridgeFunction_OnInterfaceRender()
    -- Toggle menu com tecla M
    if not menuVisible and SEASON3B_IsPress(0x4D) then -- VK_M
        menuVisible = true
        SetBlockInput(true)
    end
    
    if menuVisible then
        -- Renderizar menu
        -- ...
        
        -- Fechar menu
        if SEASON3B_IsPress(0x1B) then -- VK_ESCAPE
            menuVisible = false
            SetBlockInput(false)
        end
    end
end
```

### Dialog Box

```lua
local dialogOpen = false
local dialogText = ""

function BridgeFunction_OnInterfaceRender()
    if dialogOpen then
        -- Bloquear input
        SetBlockInput(true)
        
        -- Renderizar dialog
        UIRenderText_SetBgColor(50, 50, 50, 220)
        UIRenderText_RenderText(200, 200, "", 400, 200, 10)
        
        -- Texto do dialog
        UIRenderText_SetTextColor(255, 255, 255, 255)
        UIRenderText_RenderText(220, 220, dialogText, 360, 100, 11)
        
        -- Botão OK
        if IsMouseClicked() and CheckMouseIn(350, 350, 100, 30) then
            dialogOpen = false
            SetBlockInput(false)
        end
        
        -- Renderizar botão OK
        UIRenderText_RenderText(350, 350, "OK", 100, 30, 11)
    end
end
```

## Notas Importantes

1. **Sempre desbloqueie**: Sempre chame `SetBlockInput(false)` quando fechar a UI modal
2. **Use com modais**: Ideal para menus, dialogs e UIs que devem capturar todo o input
3. **Não bloqueie permanentemente**: Evite bloquear o input sem uma forma de desbloquear
4. **Combine com ESC**: Use ESC como tecla padrão para fechar modais e desbloquear input

## Funções Relacionadas

- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Verifica se tecla foi pressionada
- [IsMouseClicked](IsMouseClicked.md) - Verifica se mouse foi clicado
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

