# IsMouseClicked

Verifica se o botão esquerdo do mouse foi clicado no frame atual.

## Assinatura

```lua
IsMouseClicked() -> bool
```

## Parâmetros

Nenhum.

## Retorno

`bool` - `true` se o botão esquerdo do mouse foi clicado no frame atual, `false` caso contrário.

## Características

- Retorna `true` apenas uma vez por clique
- Útil para detectar cliques únicos (não mantidos)
- Deve ser chamado dentro de `BridgeFunction_OnInterfaceRender` para funcionar corretamente

## Exemplos

### Uso Básico

```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        -- Botão foi clicado neste frame
        UIRenderText_RenderText(100, 100, "Mouse clicado!", 200, 20, 1)
    end
end
```

### Clique em Área Específica

```lua
function BridgeFunction_OnInterfaceRender()
    -- Verificar clique em botão (100, 100, 200x50)
    if IsMouseClicked() and CheckMouseIn(100, 100, 200, 50) then
        -- Botão foi clicado
        UIRenderText_RenderText(100, 200, "Botão Clicado!", 200, 20, 1)
    end
end
```

### Sistema de Botões

```lua
local buttons = {
    {x = 100, y = 100, w = 200, h = 50, text = "Botão 1"},
    {x = 100, y = 160, w = 200, h = 50, text = "Botão 2"}
}

function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        for i, button in ipairs(buttons) do
            if CheckMouseIn(button.x, button.y, button.w, button.h) then
                -- Botão clicado
                print("Botão clicado: " .. button.text)
            end
        end
    end
end
```

## Diferença entre IsMouseClicked e IsMouseHeld

- **IsMouseClicked**: Retorna `true` apenas uma vez quando o botão é pressionado
- **IsMouseHeld**: Retorna `true` continuamente enquanto o botão está pressionado

**Exemplo:**
```lua
function BridgeFunction_OnInterfaceRender()
    if IsMouseClicked() then
        -- Executa apenas uma vez por clique
        print("Clique detectado")
    end
    
    if IsMouseHeld() then
        -- Executa continuamente enquanto pressionado
        -- Útil para drag & drop, seleção contínua, etc.
    end
end
```

## Notas Importantes

1. **Chamada no OnInterfaceRender**: Esta função deve ser chamada dentro de `BridgeFunction_OnInterfaceRender` para funcionar corretamente
2. **Uma vez por frame**: Retorna `true` apenas uma vez por clique, mesmo se chamado múltiplas vezes no mesmo frame
3. **Combine com CheckMouseIn**: Use `CheckMouseIn` para verificar se o clique foi em uma área específica
4. **Performance**: A função é muito rápida, pode ser chamada a cada frame sem problemas

## Funções Relacionadas

- [IsMouseHeld](IsMouseHeld.md) - Verifica se botão está sendo mantido pressionado
- [CheckMouseIn](CheckMouseIn.md) - Verifica se mouse está em área retangular
- [MouseLButton](../10-Variaveis-Globais.md#mouselbutton) - Variável global do estado do botão esquerdo
- [Sistema de Input](../07-Sistema-Input.md) - Documentação completa do sistema de input

