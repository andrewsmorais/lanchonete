# Plano de Implementação: Painel Administrativo ChefStart & Robô WhatsApp Gemini para Thom's Lanches

Modernização completa do painel administrativo do Thom's Lanches incorporando todas as funcionalidades e inteligência de dados demonstradas no produto de mercado **ChefStart**, acrescido de um **Robô Conversacional de WhatsApp alimentado pela API Gemini** e arquitetura de integração com a Meta Cloud API, mantendo a vitrine inicial do cardápio 100% preservada.

---

## Revisão do Usuário & Decisões Confirmadas

> [!IMPORTANT]
> **Decisões alinhadas na Fase 1:**
> 1. **Robô WhatsApp + Gemini**: Incluir simulador interativo de conversa em tempo real dentro do painel para testar pedidos em linguagem natural e gerar pedidos automáticos no KDS, acompanhado da documentação e painel de configuração da Meta Cloud API.
> 2. **Identidade Visual**: Preservar e aprofundar o acabamento escuro premium do Thom's Lanches (`#0a0a0c` a `#121216` com vidro escuro, ouro e âmbar metálico), organizando os novos dashboards, gráficos comparativos e tabelas do ChefStart com alta legibilidade.
> 3. **Módulo Garçom Mobile**: Fornecer a interface dedicada do garçom para tablets e celulares, permitindo escolher a mesa, filtrar itens por categoria com fotos apetitosas e lançar os pedidos direto para a cozinha/KDS.
> 4. **Cardápio Inicial do Cliente**: Permanece completamente intacto, conforme instrução explícita do usuário.

---

## 1. Visão Geral & Módulos do Sistema

O sistema passará a oferecer ao dono do restaurante e à sua equipe um ecossistema operacional de ponta a ponta:

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                            THOM'S LANCHES ECOSYSTEM                          │
├──────────────────────────────────────┬───────────────────────────────────────┤
│ 🛒 CARDÁPIO ONLINE (INTACTO)         │ 👑 PAINEL ADMINISTRATIVO (ATUALIZADO) │
│ - Vitrine de lanches e combos        │ - 1. Dashboard Executivo & KPIs       │
│ - Carrinho de compras do cliente     │ - 2. Salão: Controle de Mesas & Tempo │
│ - Botão direto de WhatsApp           │ - 3. Garçom: Cardápio Mobile com Fotos│
│                                      │ - 4. Logística: Quadro Kanban Entregas│
│                                      │ - 5. Cozinha KDS & Status             │
│                                      │ - 6. Robô IA WhatsApp (Gemini + Meta) │
│                                      │ - 7. Gestão de Fichas Técnicas/Preços │
└──────────────────────────────────────┴───────────────────────────────────────┘
```

### Principais Pilares Solicitados:
1. **Dashboard Executivo (Resumo Geral ChefStart)**:
   - Cards de destaque: **Ticket Médio** (`R$ 46,25`), **Faturamento Semanal/Mensal** (`R$ 8.940,00`), **Clientes Atendidos** (`890`) e **Variação %** comparativa.
   - **Gráfico Comparativo Semanal**: Barras comparativas de Segunda a Domingo entre a *Semana Passada* (cinza escuro) e *Esta Semana* (âmbar/dourado vibrante).
   - **Gráfico de Origem dos Pedidos**: Distribuição percentual em anel (*Donut Chart*) entre **Mesa**, **Balcão**, **Entrega (Delivery)** e **Individual/WhatsApp**.
   - **Alerta de Estoque Crítico**: Tabela com controle de insumos e produtos com baixa contagem (ex: Pão de Hambúrguer, Queijo Mussarela, Coca-Cola Lata) e badge de prioridade (Alta, Média).
   - **Pratos Mais Vendidos**: Tabela com contagem exata e faturamento de cada item.

2. **Controle de Salão & Mesas (Grid Visual 1 a 10)**:
   - Cards visuais para cada mesa com número, capacidade de lugares (ex: 4 lugares, 2 lugares), status (Livre, Ocupada, Reservada).
   - Nome do cliente e garçom associado.
   - Itens já pedidos na mesa com resumo dos pratos e valor acumulado (`R$ 89,80`).
   - **Cronômetro de ocupação em tempo real** (ex: `00:42`, `01:15`) com alerta de permanência.
   - Ações rápidas: Abrir Comanda, Adicionar Pedido, Transferir/Unir Mesas e Fechar Conta com emissão de extrato.

3. **Módulo Cardápio do Garçom (PDV Salão Mobile)**:
   - Tela adaptada para smartphone e tablet com cabeçalho de seleção da mesa/comanda.
   - Carrossel de categorias com fotos apetitosas (Hambúrgueres, Linha Frango, Beirutes, Bebidas e Porções).
   - Busca instantânea por nome ou código do item (ex: Cód. 1, Cód. 3).
   - Painel de lançamento com colunas "A preparar" e "Entregues".
   - Botão de confirmação "Salvar Pedido" que despacha os itens imediatamente para a tela da Cozinha (KDS).

4. **Quadro de Entregas (Kanban Logístico)**:
   - Colunas organizadas do ChefStart: **Abertas**, **Em Preparo**, **Prontas**, **Enviando** e **Entregue**.
   - Filtros de período (Ano, Mês, Dia) e campo de busca por cliente/pedido.
   - Detalhamento de endereço, entregador associado (ex: Marlon Souza, Jefferson), valor a receber e botão "Marcar Pronto / Despachar".

5. **Robô WhatsApp com IA Gemini & Meta Cloud API**:
   - **Simulador Interativo de WhatsApp no Painel**: Interface idêntica ao chat do WhatsApp Web/Mobile onde o dono do restaurante pode simular clientes conversando em linguagem natural, pedindo sugestões de lanches, tirando dúvidas sobre ingredientes e fechando pedidos ("Quero 2 X-Bacon e uma Coca zero").
   - O modelo Gemini processa a intenção, consulta o cardápio do Thom's Lanches, formata o resumo do pedido e gera a comanda diretamente na fila de pedidos reais da cozinha!
   - **Guia e Central de Conexão com a Meta Cloud API**: Documentação prática passo a passo (Token de Acesso Permanente, ID do Número de Telefone, Webhook URL e Verify Token) com endpoints prontos em Node.js/Express.

---

## 2. Experiência do Usuário & Design Visual

### Direção de Arte: Obsidian, Âmbar Metálico e Vidro Escuro
- **Fundo**: Base profunda (`#0a0a0c` a `#121216`) com gradiente sutil e acabamento fosco/texturizado.
- **Cards e Superfícies**: Glassmorphism escuro (`bg-zinc-900/80 backdrop-blur-md border border-amber-500/20 shadow-xl shadow-black/60 rounded-2xl`).
- **Acentos**: Dourado e Âmbar (`#f59e0b`, `#fbbf24`, `#d97706`), verde esmeralda para métricas positivas e vermelho carmim para alertas críticos.
- **Tipografia**: `Plus Jakarta Sans` para estrutura e números tabulares (`font-mono tabular-nums`), e `Bebas Neue` para títulos de impacto.
- **Zero-Slop**: Gráficos SVG nativos precisos, micro-interações de hover suaves (`hover:-translate-y-1`), badges sem cápsulas artificiais e botões com feedback tátil.

---

## 3. Arquitetura Técnica & Fluxo de Dados

```
┌────────────────────────────────────────────────────────────────────────┐
│                          FLUXO DO ROBÔ WHATSAPP                        │
└──────────────────────────────────┬─────────────────────────────────────┘
                                   │
         ┌─────────────────────────┴─────────────────────────┐
         ▼                                                   ▼
┌───────────────────┐                               ┌───────────────────┐
│  SIMULADOR NO     │                               │  META CLOUD API   │
│  PAINEL ADMIN     │                               │ (WhatsApp Oficial)│
└────────┬──────────┘                               └─────────┬─────────┘
         │                                                    │
         ▼                                                    ▼
┌───────────────────────────────────────────────────────────────────────┐
│ BACKEND / PROXY GEMINI API (ai.models.generateContent)                │
│ - Modelo: gemini-3.8-flash                                            │
│ - System Instruction: Atendente virtual do Thom's Lanches             │
│ - Function Calling / Structured Output: Extrai itens, obs e endereço  │
└──────────────────────────────────┬────────────────────────────────────┘
                                   │
                                   ▼
┌───────────────────────────────────────────────────────────────────────┐
│ ESTADO OPERACIONAL CENTRALIZADO (KDS / MESAS / ENTREGAS / DASHBOARD)  │
│ - Novo pedido criado em "Abertas / Em Preparo"                        │
│ - Notificação sonora e visual no Painel e Cozinha                     │
└───────────────────────────────────────────────────────────────────────┘
```

### Estrutura de Abas do Painel Administrativo:
- **Dashboard / Resumo Executivo**: KPIs de faturamento, gráfico comparativo de semanas, gráfico Donut de origem dos pedidos, estoque crítico e top 5 produtos.
- **Controle de Mesas (Salão)**: Grid das Mesas 1 a 10 com status livre/ocupada, timer de ocupação, comanda e extrato.
- **Módulo Garçom (PDV Salão)**: Interface do garçom com fotos reais, busca por código, seleção de mesa e envio direto à cozinha.
- **Quadro de Entregas (Kanban)**: Gestão de delivery por etapas (Abertas -> Em Preparo -> Prontas -> Enviando -> Entregue).
- **Cozinha (KDS)**: Tela da chapa com cronômetros e itens agrupados.
- **Robô WhatsApp IA (Gemini)**: Simulador interativo do robô + Guia de integração Meta API.
- **Gestão de Lanches**: Controle de preços, pausa de itens e ficha de custos.

---

## 4. Plano de Execução Passo a Passo

1. **Atualizar Estrutura de Navegação do Painel Administrativo**:
   - Adicionar as novas abas na Sidebar e na barra de atalhos: *Controle de Mesas*, *Módulo Garçom*, *Kanban Entregas* e *Robô WhatsApp IA*.
2. **Construir o Dashboard Executivo Idêntico ao ChefStart**:
   - Inserir gráfico SVG de barras comparativas (Semana Passada vs Esta Semana).
   - Inserir gráfico Donut de Origem dos Pedidos (Mesa, Balcão, Entrega, Individual).
   - Inserir tabela de Produtos em Estoque Crítico (Insumos, Estoque Atual e Prioridade).
   - Inserir tabela de Pratos Mais Vendidos com dados enriquecidos.
3. **Implementar a Visão de Salão & Mesas (Mesas 1 a 10)**:
   - Criar o grid interativo de mesas com capacidade de pessoas, temporizador de tempo ativo (`00:42`), status visual, cliente associado e modal de abertura/fechamento de comanda.
4. **Implementar a Tela de Atendimento do Garçom**:
   - Criar a interface mobile-friendly do garçom com seleção de mesa, grade de lanches com fotos, busca por código e lançamento direto para a Cozinha KDS.
5. **Implementar o Quadro de Entregas (Kanban Logístico)**:
   - Desenvolver o quadro kanban de 5 colunas com arraste/mudança de status, filtros por data e atribuição de motoboy/taxa.
6. **Implementar o Robô WhatsApp com IA Gemini**:
   - Integrar chamada à API Gemini (`gemini-3.8-flash`) com prompt de atendente treinado no cardápio do Thom's Lanches.
   - Criar o simulador interativo de chat no painel permitindo conversar com o robô e testar pedidos que se transformam em comandas reais.
   - Incluir a aba de configuração da Meta Cloud API com webhook pronto.
7. **Verificação & Testes**:
   - Validar build sem erros via `compile_applet` e `lint_applet`.
   - Garantir que a parte inicial do cardápio do cliente permaneceu totalmente intocada.
