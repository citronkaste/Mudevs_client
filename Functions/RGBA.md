# RGBA

Cria um valor de cor RGBA padrão.

## Assinatura

```lua
RGBA(r, g, b, a) -> DWORD
```

## Parâmetros

- `r`, `g`, `b`, `a` (number): Componentes de cor (0 - 255)

## Retorno

`DWORD` - Valor de cor no formato DWORD.

## Uso

Cria um valor de cor usando componentes inteiros (0 a 255). Mais intuitivo que `Color4f` para valores diretos.

## Exemplos

### Criar Cores Comuns

```lua
-- Vermelho opaco
local red = RGBA(255, 0, 0, 255)

-- Verde semi-transparente
local green = RGBA(0, 255, 0, 128)

-- Azul opaco
local blue = RGBA(0, 0, 255, 255)

-- Branco opaco
local white = RGBA(255, 255, 255, 255)

-- Preto opaco
local black = RGBA(0, 0, 0, 255)

-- Amarelo opaco
local yellow = RGBA(255, 255, 0, 255)
```

### Cores com Transparência

```lua
-- Vermelho 50% transparente
local redTransparent = RGBA(255, 0, 0, 128)

-- Verde 25% transparente
local greenTransparent = RGBA(0, 255, 0, 64)

-- Azul 75% transparente
local blueTransparent = RGBA(0, 0, 255, 192)
```

## Diferença entre RGBA e Color4f

- **RGBA**: Usa valores inteiros de 0-255 (mais intuitivo)
- **Color4f**: Usa valores float de 0.0-1.0 (melhor para cálculos)

**Exemplo de conversão:**
```lua
-- RGBA: 255, 0, 0, 255
-- Color4f: 1.0, 0.0, 0.0, 1.0
-- Ambos representam vermelho opaco
```

## Notas Importantes

1. **Intuitivo**: Valores de 0-255 são mais fáceis de entender
2. **Padrão**: Formato padrão para cores em muitos sistemas
3. **DWORD**: Retorna valor DWORD compatível com o sistema
4. **Uso comum**: Mais comum que `Color4f` para valores diretos

## Funções Relacionadas

- [Color4f](Color4f.md) - Cria cor usando valores float
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Define cor do texto
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

