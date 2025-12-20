# Enumerações e Constantes

Este documento lista todas as constantes e enumerações disponíveis na API Lua do Client.

## Códigos de Teclado (VK Codes)

Códigos virtuais de teclas do Windows usados com `SEASON3B_IsPress`, `SEASON3B_IsRelease`, etc.

| Constante | Valor | Descrição |
| :-------- | :---- | :-------- |
| `VK_LBUTTON` | 0x01 | Botão esquerdo do mouse |
| `VK_RBUTTON` | 0x02 | Botão direito do mouse |
| `VK_CANCEL` | 0x03 | Cancel |
| `VK_MBUTTON` | 0x04 | Botão do meio do mouse |
| `VK_BACK` | 0x08 | Backspace |
| `VK_TAB` | 0x09 | Tab |
| `VK_RETURN` | 0x0D | Enter |
| `VK_SHIFT` | 0x10 | Shift |
| `VK_CONTROL` | 0x11 | Ctrl |
| `VK_MENU` | 0x12 | Alt |
| `VK_PAUSE` | 0x13 | Pause |
| `VK_CAPITAL` | 0x14 | Caps Lock |
| `VK_ESCAPE` | 0x1B | Esc |
| `VK_SPACE` | 0x20 | Espaço |
| `VK_PRIOR` | 0x21 | Page Up |
| `VK_NEXT` | 0x22 | Page Down |
| `VK_END` | 0x23 | End |
| `VK_HOME` | 0x24 | Home |
| `VK_LEFT` | 0x25 | Seta Esquerda |
| `VK_UP` | 0x26 | Seta Cima |
| `VK_RIGHT` | 0x27 | Seta Direita |
| `VK_DOWN` | 0x28 | Seta Baixo |
| `VK_0` até `VK_9` | 0x30-0x39 | Números 0-9 |
| `VK_A` até `VK_Z` | 0x41-0x5A | Letras A-Z |
| `VK_F1` até `VK_F12` | 0x70-0x7B | Teclas de função F1-F12 |

## Tipos de Entidade (Kind)

Usado na propriedade `Kind` de `GameCharacter`.

| Valor | Descrição |
| :---- | :-------- |
| 0 | Player (Jogador) |
| 1 | Monster (Monstro) |
| 2 | NPC |

## Códigos de Classe

Códigos de classe de personagem usados em `GameCharacter.Class`.

| Valor | Classe |
| :---- | :----- |
| 0 | Dark Wizard (DW) |
| 1 | Dark Knight (DK) |
| 2 | Fairy Elf (FE) |
| 3 | Magic Gladiator (MG) |
| 4 | Dark Lord (DL) |
| 5 | Summoner (SU) |
| 6 | Rage Fighter (RF) |
| 7 | Grow Lancer (GL) |
| 8 | Rune Wizard (RW) |
| 9 | Slayer (SL) |
| 10 | Gun Crusher (GC) |
| 11 | Light Wizard (LW) |
| 12 | Lemuria Mage (LM) |
| 13 | Illusion Knight (IK) |
| 14 | Mystic Knight (MK) |
| 15 | Dark Knight (DK) |
| 16 | Magic Knight (MK) |
| 17 | Dark Wizard (DW) |
| 18 | Soul Master (SM) |
| 19 | Grand Master (GM) |
| 20 | High Elf (HE) |
| 21 | Muse Elf (ME) |
| 22 | Blade Knight (BK) |
| 23 | Blade Master (BM) |
| 24 | Dark Wizard (DW) |
| 25 | Soul Master (SM) |
| 26 | Grand Master (GM) |
| 27 | Dark Knight (DK) |
| 28 | Blade Knight (BK) |
| 29 | Blade Master (BM) |
| 30 | Fairy Elf (FE) |
| 31 | Muse Elf (ME) |
| 32 | High Elf (HE) |
| 33 | Magic Gladiator (MG) |
| 34 | Dark Lord (DL) |
| 35 | Summoner (SU) |
| 36 | Rage Fighter (RF) |
| 37 | Grow Lancer (GL) |
| 38 | Rune Wizard (RW) |
| 39 | Slayer (SL) |
| 40 | Gun Crusher (GC) |
| 41 | Light Wizard (LW) |
| 42 | Lemuria Mage (LM) |
| 43 | Illusion Knight (IK) |
| 44 | Mystic Knight (MK) |

## Códigos de Controle (CtlCode)

Usado em `GameCharacter.CtlCode` para identificar status administrativo.

| Valor | Descrição |
| :---- | :-------- |
| 0 | Jogador Normal |
| 8 | Game Master (GM) |
| 32 | Administrador |

## Níveis PK

Usado em `GameCharacter.PK` para identificar status de PK.

| Valor | Descrição |
| :---- | :-------- |
| 3 | Common (Normal) |
| 6 | Phonomania (PK) |

## Notas Importantes

1. **VK Codes**: Use os valores hexadecimais diretamente ou defina constantes em seu script
2. **Kind**: Sempre verifique o tipo de entidade antes de acessar propriedades específicas
3. **Class**: Os valores podem variar dependendo da versão do cliente
4. **CtlCode**: Use para identificar GMs e administradores

## Exemplos de Uso

```lua
-- Verificar se a tecla M foi pressionada
if SEASON3B_IsPress(0x4D) then -- VK_M
    -- Fazer algo
end

-- Verificar tipo de entidade
local character = GetCharacter(index)
if character and character.Kind == 0 then
    -- É um jogador
end

-- Verificar se é GM
if Hero and Hero.CtlCode == 8 then
    -- É um Game Master
end
```

## Funções Relacionadas

- [SEASON3B_IsPress](../Functions/SEASON3B_IsPress.md) - Verifica se tecla foi pressionada
- [GetCharacter](../Functions/GetCharacter.md) - Obtém objeto de personagem
- [Variáveis Globais](10-Variaveis-Globais.md) - Documentação de variáveis globais

