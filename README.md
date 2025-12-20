# Documentação da API Lua - Mu Online Client

Documentação completa e organizada da API Lua do Game Client, incluindo todas as funções, classes, propriedades e hooks disponíveis para desenvolvimento de scripts client-side.

## 📋 Índice

### 📚 Documentação Principal

Documentação temática organizada por sistemas:

1. **[Introdução e Princípios](01-Introducao.md)** - Visão geral do sistema e princípios de design
2. **[Enumerações e Constantes](02-Enumeracoes.md)** - Constantes globais do sistema
3. **[Funções Globais de Utilidade](03-Funcoes-Globais.md)** - Funções auxiliares básicas
4. **[Objetos do Jogo](04-Objetos-Game.md)** - Objetos principais (Character, Model, Item, etc.)
5. **[Bridge Functions (Hooks)](05-Bridge-Functions.md)** - Funções de callback do sistema
6. **[Sistema de Renderização](06-Sistema-Renderizacao.md)** - Sistema completo de renderização e gráficos
7. **[Sistema de Input](07-Sistema-Input.md)** - Input, mouse e teclado
8. **[Sistema de UI](08-Sistema-UI.md)** - Interface de usuário e texto
9. **[Sistema de Pacotes](09-Sistema-Pacotes.md)** - Manipulação de pacotes de rede
10. **[Variáveis Globais](10-Variaveis-Globais.md)** - Variáveis globais disponíveis

### 📁 Funções Individuais

Todas as funções estão documentadas individualmente na pasta [`Functions/`](Functions/README.md), organizadas por categoria:

- **🖱️ Input & Mouse** - Funções de entrada e mouse (8 funções)
- **🎨 Rendering & Graphics** - Renderização e gráficos (13 funções)
- **📝 Text & UI** - Texto e interface de usuário (6 funções)
- **👤 Object Management** - Gerenciamento de objetos (2 funções)
- **🎮 Bridge Functions** - Hooks e callbacks do sistema (3 funções)

## 📊 Estrutura da Documentação

### Arquivos Principais

A documentação está organizada em 10 arquivos principais que cobrem os sistemas essenciais:

- **01-10**: Documentação temática por sistema
- **Functions/**: Documentação individual de cada função (32 funções)
- **Api.md**: Documentação oficial completa da API

### Organização das Funções

Todas as funções estão documentadas individualmente na pasta `Functions/` com:

- Assinatura completa da função
- Descrição detalhada de parâmetros
- Valores de retorno
- Exemplos práticos de uso
- Notas importantes
- Links para funções relacionadas

### Categorias Principais

- **🖱️ Input & Mouse** (8) - Entrada, mouse e teclado
- **🎨 Rendering & Graphics** (13) - Renderização e gráficos
- **📝 Text & UI** (6) - Texto e interface
- **👤 Object Management** (2) - Gerenciamento de objetos
- **🎮 Bridge Functions** (3) - Hooks e callbacks

## 📖 Como Usar Esta Documentação

### Para Iniciantes

1. **Comece aqui**: Leia [01-Introducao.md](01-Introducao.md) para entender os princípios básicos
2. **Entenda os objetos**: Consulte [04-Objetos-Game.md](04-Objetos-Game.md) para conhecer os objetos principais
3. **Aprenda os hooks**: Veja [05-Bridge-Functions.md](05-Bridge-Functions.md) para entender o sistema de callbacks

### Para Desenvolvimento

1. **Funções específicas**: Use a [pasta Functions/](Functions/README.md) para documentação detalhada de cada função
2. **Sistemas completos**: Consulte os arquivos numerados (01-10) para visão geral de cada sistema
3. **Referência completa**: Use `Api.md` como referência técnica completa

### Navegação Rápida

- **Por categoria**: Navegue pelas categorias no [índice de funções](Functions/README.md)
- **Por nome**: Os arquivos são nomeados exatamente como as funções
- **Por sistema**: Use os arquivos principais (01-10) para visão geral

## 🔗 Links Rápidos

- **[Todas as Funções](Functions/README.md)** - Índice completo de todas as funções
- **[Bridge Functions](05-Bridge-Functions.md)** - Sistema de hooks e callbacks
- **[Sistema de Renderização](06-Sistema-Renderizacao.md)** - Sistema completo de renderização
- **[Sistema de UI](08-Sistema-UI.md)** - Interface de usuário e texto
- **[Sistema de Pacotes](09-Sistema-Pacotes.md)** - Manipulação de pacotes

## 📝 Notas Importantes

- Todas as funções estão documentadas em português
- Exemplos de código estão incluídos em cada função
- A documentação segue o padrão Markdown para fácil leitura
- Baseada em `Api.md` - Documentação oficial da API

---

**Fonte**: Documentação baseada em `Api.md` - Documentação oficial da API Lua do Game Client.

