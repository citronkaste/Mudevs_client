# Funções Individuais - Índice

Esta pasta contém a documentação detalhada de cada função da API Lua do Game Client, organizadas por categoria.

Cada função possui sua própria página com exemplos práticos, descrição de parâmetros, valores de retorno e funções relacionadas.

## 📋 Índice por Categoria

### 🖱️ Input & Mouse
- [IsMouseClicked](IsMouseClicked.md) - Verifica se botão esquerdo foi clicado
- [IsMouseHeld](IsMouseHeld.md) - Verifica se botão esquerdo está pressionado
- [CheckMouseIn](CheckMouseIn.md) - Verifica se mouse está em área retangular
- [SetBlockInput](SetBlockInput.md) - Bloqueia/desbloqueia input do jogo
- [SEASON3B_IsPress](SEASON3B_IsPress.md) - Verifica se tecla foi pressionada
- [SEASON3B_IsRelease](SEASON3B_IsRelease.md) - Verifica se tecla foi solta
- [SEASON3B_IsRepeat](SEASON3B_IsRepeat.md) - Verifica se tecla está sendo mantida
- [SEASON3B_IsNone](SEASON3B_IsNone.md) - Verifica se tecla não está pressionada

### 🎨 Rendering & Graphics
- [EnableAlphaBlend](EnableAlphaBlend.md) - Habilita alpha blending padrão
- [EnableAlphaBlendMinus](EnableAlphaBlendMinus.md) - Habilita alpha blending subtrativo
- [DisableAlphaBlend](DisableAlphaBlend.md) - Desabilita alpha blending
- [DisableDepthTest](DisableDepthTest.md) - Desabilita teste de profundidade
- [EnableDepthMask](EnableDepthMask.md) - Habilita escrita no Z-buffer
- [DisableDepthMask](DisableDepthMask.md) - Desabilita escrita no Z-buffer
- [DisableTexture](DisableTexture.md) - Desabilita texturização
- [EnableLightMap](EnableLightMap.md) - Habilita lightmapping
- [BindTexture](BindTexture.md) - Vincula textura para renderização
- [LoadBitmap](LoadBitmap.md) - Carrega textura de arquivo
- [RenderBitmap](RenderBitmap.md) - Renderiza imagem 2D com controle completo
- [RenderImage](RenderImage.md) - Renderiza imagem 2D simplificada
- [Color4f](Color4f.md) - Cria cor baseada em float
- [RGBA](RGBA.md) - Cria cor RGBA padrão

### 📝 Text & UI
- [UIRenderText_SetFont](UIRenderText_SetFont.md) - Define fonte para texto
- [UIRenderText_SetTextColor](UIRenderText_SetTextColor.md) - Define cor do texto
- [UIRenderText_SetBgColor](UIRenderText_SetBgColor.md) - Define cor de fundo do texto
- [UIRenderText_RenderText](UIRenderText_RenderText.md) - Renderiza texto na tela
- [RenderTipText](RenderTipText.md) - Renderiza texto estilo tooltip
- [IsWriteInterfaceOpen](IsWriteInterfaceOpen.md) - Verifica se interface de escrita está aberta

### 👤 Object Management
- [GetCharacter](GetCharacter.md) - Obtém objeto de personagem
- [GetModel](GetModel.md) - Obtém objeto de modelo 3D

### 🎮 Bridge Functions (Hooks)
- [BridgeFunction_OnLoadInterface](BridgeFunction_OnLoadInterface.md) - Quando UI está inicializando
- [BridgeFunction_OnInterfaceRender](BridgeFunction_OnInterfaceRender.md) - Loop crítico de renderização
- [BridgeFunction_OnPacketRecv](BridgeFunction_OnPacketRecv.md) - Quando pacote é recebido

## 📝 Formato da Documentação

Cada arquivo de função segue um formato padronizado:

1. **Título**: Nome da função
2. **Assinatura**: Como chamar a função (sintaxe)
3. **Parâmetros**: Descrição detalhada de cada parâmetro
4. **Retorno**: O que a função retorna
5. **Exemplos**: Exemplos práticos de uso
6. **Notas**: Informações importantes e considerações
7. **Funções Relacionadas**: Links para funções relacionadas

## 🔍 Como Usar Esta Documentação

### Buscar uma Função

1. **Por categoria**: Navegue pelas categorias acima para encontrar funções relacionadas
2. **Por nome**: Os arquivos são nomeados exatamente como as funções (ex: `IsMouseClicked.md` para `IsMouseClicked`)
3. **Busca no editor**: Use a busca do seu editor para encontrar funções específicas

### Estrutura de Navegação

- Cada função tem sua própria página com documentação completa
- Use os links "Funções Relacionadas" no final de cada página para explorar funções similares
- Consulte a documentação principal para visão geral dos sistemas

## 📚 Documentação Relacionada

Para informações mais detalhadas sobre os sistemas, consulte:

- [Documentação Principal](../README.md) - Visão geral e índice completo
- [Bridge Functions](../05-Bridge-Functions.md) - Sistema de hooks e callbacks
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Sistema completo de renderização
- [Sistema de Input](../07-Sistema-Input.md) - Input, mouse e teclado
- [Sistema de UI](../08-Sistema-UI.md) - Interface de usuário e texto

---

**Fonte**: Esta documentação é baseada em `Api.md` - Documentação oficial da API Lua do Game Client.

