# Color4f

Cria um valor de cor baseado em componentes float.

## Assinatura

```lua
Color4f(r, g, b, a) -> DWORD
```

## Parâmetros

- `r`, `g`, `b`, `a` (float): Componentes de cor (0.0 - 1.0)

## Retorno

`DWORD` - Valor de cor no formato DWORD.

## Uso

Cria um valor de cor usando componentes float (0.0 a 1.0). Útil para cálculos de cor e interpolação.

## Exemplos

### Criar Cores

```lua
-- Vermelho opaco
local red = Color4f(1.0, 0.0, 0.0, 1.0)

-- Verde semi-transparente
local green = Color4f(0.0, 1.0, 0.0, 0.5)

-- Azul opaco
local blue = Color4f(0.0, 0.0, 1.0, 1.0)

-- Branco opaco
local white = Color4f(1.0, 1.0, 1.0, 1.0)
```

### Interpolação de Cores

```lua
function InterpolateColor(color1, color2, t)
    -- Interpolação linear entre duas cores
    local r = color1.r + (color2.r - color1.r) * t
    local g = color1.g + (color2.g - color1.g) * t
    local b = color1.b + (color2.b - color1.b) * t
    local a = color1.a + (color2.a - color1.a) * t
    return Color4f(r, g, b, a)
end
```

## Notas Importantes

1. **Float-based**: Usa valores de 0.0 a 1.0 em vez de 0-255
2. **Cálculos**: Ideal para cálculos matemáticos e interpolação
3. **DWORD**: Retorna valor DWORD compatível com o sistema
4. **Precisão**: Mais preciso para cálculos que `RGBA`

## Funções Relacionadas

- [RGBA](RGBA.md) - Cria cor usando valores 0-255
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Define cor do texto
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

