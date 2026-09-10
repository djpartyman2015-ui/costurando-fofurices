# Ateliê Costurando Fofurices — Sistema de Gestão

Documentação de tudo que foi construído e configurado até agora.

---

## 1. Visão geral

Sistema de gestão completo para o ateliê de enxoval de bebê **Costurando Fofurices**, feito como um **único arquivo HTML/JS**, hospedado gratuitamente no **GitHub Pages**, com banco de dados em tempo real no **Firebase Firestore**.

- **Link do sistema:** https://djpartyman2015-ui.github.io/costurando-fofurices/
- **Repositório GitHub:** `djpartyman2015-ui/costurando-fofurices`
- **Projeto Firebase:** `costurando-fofurices`
- **Login:** Google (só quem entra com uma conta Google autorizada acessa os dados)

---

## 2. Funcionalidades do sistema

### Dashboard
- KPIs do mês: Receita, Custo total, Lucro, Margem média, Ticket médio por produto
- Navegação por mês (setas ◀ ▶) com comparativo percentual vs mês anterior
- "Carretel da margem" na barra lateral (indicador visual sempre visível)
- Insights automáticos: canal que mais vendeu, produto com margem baixa, ticket médio, frete total dos pedidos, frete absorvido, taxa de cartão paga, gasto com suprimentos, valor a receber
- **Entregas da semana**: lista agrupada por pedido (não por produto), com aviso de atrasados, checkbox de seleção pra imprimir só os marcados, impressão com logo + carimbo de data/hora, e clique na linha abre os detalhes do pedido
- Gráfico de Receita/Custo/Lucro dos últimos 6 meses
- Gráfico de Despesas por categoria dos últimos 6 meses (empilhado: produtos, frete, taxa de cartão, suprimentos, funcionário, mídia, material, outro)
- Gráfico de Vendas por Estado (UF) e Produtos mais vendidos (histórico completo)
- Gráfico de Recebido x Pendente (histórico completo)
- Tabela "Detalhamento de custos do mês" (cada categoria separada)
- Tabela de produtos mais lucrativos
- Dicas fixas de referência de mercado (markup, margem saudável)

### Catálogo
- Cadastro de produtos: nome, categoria, preço de venda, custo de material, custo de mão de obra, foto
- Categorias: Saquinhos para Maternidade, Enxoval, Mantinhas, Necessaires, Porta Documentos, Porta Laços, Ninho, Combos, Outro
- Barra de busca por nome
- Ordenação alfabética
- Badge de margem (verde/amarelo/vermelho) em cada produto
- Editar / Excluir
- **Importação em massa**: cola uma lista de produtos (formato `Nome | Categoria`) e cadastra todos de uma vez — já vem pré-carregada com os 67 produtos originais do catálogo

### Suprimentos (registro de compras)
- Não é mais item por item — é um registro simples de cada compra: Loja, Data, Cartão usado, Valor, Frete
- Entra automaticamente no cálculo de custo/margem do mês da compra
- Editar / Excluir

### Custos
- Categorias: Material, Funcionário, Mídia, Frete, Outro
- Campo condicional "Nome do funcionário" quando categoria = Funcionário
- Campo condicional "Duração do anúncio (dias)" quando categoria = Mídia (substitui o campo Recorrente)
- Campo "Recorrente (mensal)" para as demais categorias
- Editar / Excluir

### Canais
- Gráficos de Receita por canal e Quantidade por canal
- Gráfico de Custo x Receita x Lucro por canal (histórico completo) — mostra qual canal é mais lucrativo, não só o que mais vende
- Tabela de detalhamento por canal

### Vendas
- **Pedido com múltiplos itens** (carrinho): dá pra vender vários produtos pra mesma cliente num único pedido
- Dados do cliente: nome, WhatsApp (com botão de conversa direta), Instagram, Estado (UF), nome do bebê, detalhes livres do pedido
- Canal, data da venda, data combinada de entrega
- Status de entrega (Pendente/Entregue) separado do Status de pagamento (calculado automaticamente)
- Frete: tipo (Sedex, PAC, Jadlog, Retirada local, Motoboy, Outro), valor, se é pago pelo cliente ou absorvido
- Desconto aplicável no pedido
- Pagamento dividido entre Cartão e Pix, com cálculo automático da **taxa de 3,03%** sobre pagamentos no cartão
- Resumo ao vivo no formulário: total, pago, taxa, quanto falta
- Clique na linha da tabela abre modal com todos os detalhes do pedido
- Editar / Excluir / Marcar como entregue
- **Imprimir um pedido individual**: botão "🖨️ Imprimir pedido" dentro do modal de detalhes — imprime só aquele pedido (itens em linhas, valores, canal, datas, frete, pagamento completo), com o mesmo cabeçalho com logo/data/hora

### Identidade Visual
- Nome da marca, logo, cor primária e secundária editáveis — aplicados em tempo real em todo o sistema
- Logo padrão já configurado com a arte real do ateliê

---

## 3. Infraestrutura técnica

### Firebase (projeto `costurando-fofurices`)
- **Firestore**: banco de dados principal (coleções: `produtos`, `materiais`, `custos`, `vendas`, `config`)
- **Authentication**: login Google ativado (login anônimo foi desativado por segurança)
- **Plano**: Blaze (pagamento por uso, necessário para backups automáticos)
- **Backup configurado e confirmado funcionando:**
  - Recuperação pontual: ativada, 7 dias
  - Backups programados: diários, retenção de 30 dias
- Domínio autorizado para login: `djpartyman2015-ui.github.io`

### GitHub
- Repositório dedicado: `costurando-fofurices` (separado dos outros projetos pessoais em `Links-Ativos`)
- Arquivos no repositório:
  - `index.html` — sistema completo (HTML + CSS + JS + Firebase + Chart.js embutido)
  - `manifest.json` — configuração de PWA
  - `icon-192.png` e `icon-512.png` — ícones do app
- GitHub Pages ativado, publicando a partir da branch `main`

### PWA (app no celular)
- Sistema instalável na tela inicial do iPhone (via Safari → Compartilhar → Adicionar à Tela de Início) e Android
- Abre em tela cheia, sem barra do navegador, com ícone e nome próprios

### Chart.js
- Embutido diretamente no `index.html` (não depende de CDN externo) — corrige um problema em que os gráficos ficavam em branco por bloqueio de rede corporativa

### Claude Code
- Conectado ao repositório localmente (`C:\Claude\Projetos\costurando-fofurices`), permitindo aplicar e subir atualizações direto do computador, sem precisar fazer upload manual pelo site do GitHub

---

## 4. Outros projetos Firebase do Andrey (mapeados durante a configuração de backup)

| Projeto | Banco usado | Backup |
|---|---|---|
| `costurando-fofurices` | Firestore | ✅ Diário (30 dias) + Recuperação pontual (7 dias) |
| `medicos-andrey` | Realtime Database | ✅ Diário, confirmado rodando |
| `filmoteca-10976` | Firestore | ✅ Semanal (30 dias) + Recuperação pontual (7 dias) — já estava configurado |
| `skincare-andrey` | — | ⏳ Pendente — esbarrou na cota máxima de projetos por conta de faturamento; pedido de aumento de cota enviado ao Google (resposta em ~2 dias úteis) |

---

## 5. Correções importantes feitas ao longo do projeto

- **Bug de fuso horário**: datas no formato `AAAA-MM-DD` estavam sendo reinterpretadas como UTC ao calcular o mês, fazendo custos do dia 1º do mês contarem no mês anterior. Corrigido.
- **Contagem dupla de frete**: custos lançados com categoria "Frete" estavam sendo somados duas vezes no total do mês. Corrigido.
- **Gráficos em branco**: causados por bloqueio de CDN externo (Chart.js) em rede corporativa. Resolvido embutindo a biblioteca no próprio arquivo.
- **Botão Cancelar**: reforçado para sempre fechar o formulário (antes usava toggle, agora força o fechamento).
- **Login "missing initial state" (bug conhecido do Firebase)**: acontecia às vezes no login por popup. Adicionada tentativa automática (retry) antes de mostrar erro pra usuária.
- **Login em loop no celular**: tentativa de usar login por redirecionamento (em vez de popup) no PWA/celular causou looping em vez de resolver — a página de autenticação do Firebase travava em branco. Revertido para popup sempre, com retry mais espaçado (até 2 tentativas automáticas).
- **Persistência de sessão**: forçada explicitamente via `setPersistence` (indexedDB) para reduzir pedidos de login repetidos — mas login toda hora no iPhone é uma limitação conhecida do próprio Safari/iOS em apps instalados (ITP), não totalmente controlável pelo sistema.
- **Impressão com páginas em branco sobrando**: causada por esconder o resto da tela só com `visibility:hidden` (que preserva o espaço/altura do layout). Corrigido criando um container único de impressão (`#printOutput`) fora de todo o layout principal, com `display:none` de verdade no resto do app durante a impressão.
- **Impressão gastando tinta com fundo colorido**: adicionado CSS específico de impressão forçando fundo branco e badges sem preenchimento colorido.

## 6. Fluxo de trabalho para novas mudanças

1. Pedir a mudança aqui no chat com a Claude
2. Receber o `index.html` atualizado (e demais arquivos, se houver)
3. Subir no repositório `costurando-fofurices` no GitHub (substituindo o anterior) — manualmente ou via Claude Code local
4. Dar Ctrl+Shift+R na aba do site pra forçar atualização sem cache
5. Testar a mudança

---

*Documento gerado em 10 de agosto de 2026, atualizado pela última vez em 10 de setembro de 2026, resumindo o desenvolvimento do sistema até esta data.*
