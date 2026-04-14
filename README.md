> LINK: https://henriquecardosos96.github.io/dashboard-firmare/

# 📊 Firmare Dashboard — Gestão Empresarial

> Dashboard semanal interativo para clientes da **Firmare Gestão Empresarial**, conectado ao Google Sheets como fonte de dados. Permite acompanhamento em tempo real de métricas financeiras, comerciais, de marketing e tráfego pago — com insights gerados automaticamente por IA.

---

## 🏢 Contexto

A Firmare Gestão Empresarial entrega relatórios semanais aos seus clientes com análises de desempenho em quatro eixos: Financeiro, Comercial, Marketing e Tráfego Pago. Este projeto substitui e supera o processo manual de slides com um dashboard HTML interativo, atualizado automaticamente a partir de uma planilha Google Sheets.

**Cliente piloto:** Dra. Joice Fraga — Saúde Plena (Candeias e Salvador/BA)

---

## ✨ Funcionalidades

- 🔐 **Tela de login** com senha de acesso
- 👥 **Filtro por cliente** com opção "Todos"
- 📅 **Filtro por período** (data de / até)
- 🔄 **Navegação semanal** (← semana anterior / próxima →)
- 📈 **Comparativos automáticos** em todos os KPIs (▲▼ vs semana anterior)
- 🤖 **Insights gerados por IA** (Claude API) com base nos dados da semana
- 📊 **Gráficos de linha/área** com histórico semanal
- 🔗 **Dados ao vivo** via Google Sheets público (CSV)

---

## 🗂️ Estrutura do Repositório

```
firmare-dashboard/
├── index.html        # Dashboard completo (single-file application)
└── README.md         # Este arquivo
```

> O dashboard é uma aplicação **single-file**: todo o HTML, CSS e JavaScript estão em `index.html`, sem dependências de build. Basta abrir no navegador ou hospedar em qualquer servidor estático.

---

## 📐 Arquitetura de Dados

### Fonte de dados

O dashboard consome o Google Sheets via URL pública no formato CSV:

```
https://docs.google.com/spreadsheets/d/{SHEET_ID}/gviz/tq?tqx=out:csv
```

> A planilha deve estar publicada em: **Arquivo → Compartilhar → Publicar na web → CSV**

### Colunas esperadas na planilha

| Coluna | Módulo | Tipo |
|---|---|---|
| `Cliente` | Geral | Texto |
| `Início da Semana (Data da segunda-feira)` | Geral | Data (DD/MM/AAAA) |
| `Fim da Semana (Data do domingo)` | Geral | Data |
| `Receita Bruta da Semana` | Financeiro | Número |
| `Despesas Totais da Semana` | Financeiro | Número |
| `Ticket Médio da Semana` | Financeiro | Número |
| `Faturamento Acumulado (Mês)` | Financeiro | Número |
| `Meta de Faturamento Mensal` | Financeiro | Número |
| `Top 5 Vendas` | Financeiro | Texto livre (um por linha) |
| `Total de Leads Recebidos (Semana)` | Comercial | Número |
| `Leads de Tráfego Convertidos (Venda Direta)` | Comercial | Número |
| `Leads de Recaptação Convertidos (Base antiga)` | Comercial | Número |
| `Leads Fora de Perfil (Desqualificados)` | Comercial | Número |
| `Agendamentos/Visitas Realizadas` | Comercial | Número |
| `Nº de Vendas Realizadas` | Comercial | Número |
| `Análise Estratégica de Leads` | Comercial | Texto |
| `Novos Seguidores (Instagram)` | Marketing | Número |
| `Quantidade de Criativos Publicados (Total da semana)` | Marketing | Número |
| `Formato Predominante (Vídeos, Cards ou Carrosséis)` | Marketing | Texto |
| `Link do Melhor Criativo (Performance)` | Marketing | URL |
| `Visualizações (Melhor Criativo` | Marketing | Número |
| `Curtidas (Melhor Criativo)` | Marketing | Número |
| `Comentários (Melhor Criativo)` | Marketing | Número |
| `Compartilhamentos (Melhor Criativo)` | Marketing | Número |
| `Análise Estratégica de Conteúdo` | Marketing | Texto |
| `Quantidade de Campanhas Ativas` | Tráfego | Número |
| `Valor Total Investido (Semana)` | Tráfego | Número |
| `CPL Médio (Custo por Lead)` | Tráfego | Número |
| `CTR Médio (Taxa de Clique)` | Tráfego | Texto/% |
| `ROAS (Retorno sobre Investimento)` | Tráfego | Número |
| `Análise Estratégica de Tráfego` | Tráfego | Texto |
| `Valor Investido Mensagem` *(opcional)* | Tráfego | Número |
| `Leads Campanha Mensagem` *(opcional)* | Tráfego | Número |
| `CPL Campanha Mensagem` *(opcional)* | Tráfego | Número |
| `Valor Investido Visita Perfil` *(opcional)* | Tráfego | Número |
| `Visitas Perfil` *(opcional)* | Tráfego | Número |
| `Custo por Visita` *(opcional)* | Tráfego | Número |

---

## 📊 Módulos do Dashboard

### 💰 Financeiro
KPIs com comparativo semanal: Receita Bruta, Despesas, Resultado Líquido, Ticket Médio, ROI (%). Barra de progresso da meta mensal. Top 5 procedimentos (texto livre). Gráfico de linha histórico.

### 🎯 Comercial
KPIs com comparativo: Leads, Agendamentos, Vendas, Taxa de Conversão. Funil visual proporcional com taxa de conversão entre cada etapa. Gráfico histórico de leads.

### 📣 Marketing & Posicionamento
KPIs com comparativo: Novos Seguidores, Criativos, Engajamento, Visualizações. Card do criativo campeão com link clicável. Gráfico de linha histórico de seguidores.

### 🚀 Tráfego Pago
KPIs: Investimento, CPL, CTR, ROAS. Cards por campanha (Mensagens e Visitas ao Perfil). Gráfico histórico de investimento.

### 🤖 Insights IA
Ao acessar a aba, os dados da semana são enviados à Claude API, que retorna 8 insights estratégicos classificados por tipo:
- 🔴 **Vermelho** — alertas e problemas a resolver
- 🟢 **Verde** — pontos positivos e oportunidades
- 🟡 **Amarelo** — atenção e pontos neutros

---

## ⚙️ Configuração

Edite as constantes no topo do bloco `<script>` em `index.html`:

```javascript
const SENHA        = 'gestaoFirmare2026$';          // senha de acesso
const SHEET_ID     = '1fSgWk1_NkDzm...';            // ID da planilha Google Sheets
const CLAUDE_MODEL = 'claude-sonnet-4-20250514';     // modelo da Claude API
```

---

## 🚀 Deploy

### GitHub Pages (recomendado)

```bash
# 1. Clone ou crie o repositório
git clone https://github.com/seu-usuario/firmare-dashboard.git
cd firmare-dashboard

# 2. Ative o GitHub Pages nas configurações do repositório
# Settings → Pages → Source: main branch / root

# 3. Acesse via
# https://seu-usuario.github.io/firmare-dashboard/
```

> ⚠️ **CORS — Insights IA:** A Claude API requer que a origem da requisição seja permitida. Em GitHub Pages isso funciona normalmente via `fetch` do lado do cliente. Caso use outro domínio, verifique as políticas de CORS.

### Localmente

```bash
# Sem dependências — abra direto no navegador
open index.html

# Ou com servidor local simples
npx serve .
python3 -m http.server 8080
```

---

## 🎨 Design

| Token | Valor | Uso |
|---|---|---|
| `--marrom` | `#5C3317` | Sidebar, cards destaque, textos |
| `--dourado` | `#B8922A` | Acentos, bordas ativas, links |
| `--dourado-claro` | `#D4AC5A` | Textos sobre fundo marrom |
| `--creme` | `#F4EFE6` | Background principal |
| `--bege` | `#E6DDD0` | Bordas, divisores |
| `--branco` | `#FDFBF8` | Cards |
| Tipografia display | Cormorant Garamond | KPIs, títulos |
| Tipografia corpo | Jost | Labels, textos, navegação |

---

## 📅 Roadmap

- [x] Tela de login com senha
- [x] Conexão ao Google Sheets via CSV público
- [x] Filtro por cliente (com opção "Todos")
- [x] Filtro por período (data de / até)
- [x] Navegação semanal com setas
- [x] Comparativos automáticos em todos os KPIs
- [x] Módulo Financeiro com ROI
- [x] Módulo Comercial com funil proporcional + taxas
- [x] Módulo Marketing com gráfico de linha
- [x] Módulo Tráfego Pago com gráfico histórico
- [x] Aba Insights IA (Claude API)
- [x] Logo da Firmare no header e login
- [x] Deploy via GitHub Pages
- [ ] Suporte a múltiplas abas no Sheets (por módulo)
- [ ] Exportar relatório em PDF
- [ ] Notificações por email ao atingir metas

---

## 🤝 Desenvolvido por

**Firmare Gestão Empresarial** · [firmaregestao.com](https://firmaregestao.com) · @firmare.gestao
