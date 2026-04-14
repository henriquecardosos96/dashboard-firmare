# 📊 Firmare Dashboard — Gestão Empresarial

> Dashboard semanal interativo para clientes da **Firmare Gestão Empresarial**, conectado ao Google Sheets como fonte de dados. Permite acompanhamento em tempo real de métricas financeiras, comerciais, de marketing e tráfego pago.

---

## 🏢 Contexto

A Firmare Gestão Empresarial entrega relatórios semanais aos seus clientes com análises de desempenho em quatro eixos: Financeiro, Comercial, Marketing e Tráfego Pago. Atualmente, esses relatórios são produzidos manualmente em slides (PDF). Este projeto substitui e supera esse processo com um dashboard HTML interativo, atualizado automaticamente a partir de uma planilha Google Sheets.

**Cliente piloto:** Dra. Joice Fraga — Saúde Plena (Candeias e Salvador/BA)

---

## 🎯 Objetivos

- Eliminar o trabalho manual de geração de relatórios em slides
- Centralizar os dados em uma planilha estruturada por aba temática
- Entregar ao cliente uma URL única que sempre mostra a semana mais recente
- Escalar o modelo para todos os clientes da Firmare com mínima configuração

---

## 🗂️ Estrutura do Repositório

```
firmare-dashboard/
├── index.html              # Dashboard principal (entrada da aplicação)
├── assets/
│   ├── style.css           # Estilos globais e design system Firmare
│   └── logo-firmare.svg    # Logo da Firmare
├── js/
│   ├── config.js           # IDs do Sheets, nomes das abas, metas
│   ├── sheets.js           # Módulo de conexão e parsing do Google Sheets
│   ├── charts.js           # Funções de visualização (gráficos, KPIs)
│   └── dashboard.js        # Orquestrador principal
└── README.md
```

---

## 📐 Arquitetura de Dados

### Fonte de dados
O dashboard consome o Google Sheets via URL pública no formato CSV:

```
https://docs.google.com/spreadsheets/d/{SHEET_ID}/gviz/tq?tqx=out:csv&sheet={ABA}
```

### Estrutura de abas do Google Sheets

| Aba | Conteúdo | Atualização |
|---|---|---|
| `financeiro` | Receita bruta, despesas, ticket médio, faturamento acumulado, meta, top 5 procedimentos | Semanal |
| `comercial` | Leads totais, convertidos, recaptação, fora do perfil, agendamentos, origem (Instagram/Site) | Semanal |
| `marketing` | Novos seguidores, criativos publicados, formato, link do melhor criativo, engajamento | Semanal |
| `trafego` | Campanhas ativas, investimento, CPL, CTR, ROAS, visitas ao perfil | Semanal |
| `config` | Clientes cadastrados, metas por cliente, paleta de cores, período ativo | Fixo |

Todas as abas compartilham as colunas de identificação:

```
cliente | data_inicio_semana | data_fim_semana | mes_referencia
```

---

## 📊 Módulos do Dashboard

### 💰 Financeiro
- KPIs: Receita Bruta, Despesas, Resultado Líquido, Ticket Médio
- Gráfico de barras: Receita por semana (histórico do mês)
- Gráfico de rosca: Receita por categoria de procedimento
- Barra de progresso: % da meta mensal atingida
- Tabela: Top 5 procedimentos por valor

### 🎯 Comercial
- KPIs: Total de Leads, Conversões, Agendamentos, Taxa de Conversão
- Funil visual: Visitas → Leads → Qualificados → Agendamentos → Vendas
- Gráfico de barras: Origem dos leads (Instagram vs Site)
- Destaque: Leads frios/fora de perfil + motivo

### 📣 Marketing & Posicionamento
- KPIs: Novos Seguidores, Criativos Publicados, Engajamento do Melhor Criativo
- Card destacado: Link + métricas do criativo campeão da semana (curtidas, comentários, compartilhamentos, salvamentos)
- Histórico: Crescimento de seguidores semana a semana

### 🚀 Tráfego Pago
- KPIs: Investimento Total, CPL, CTR, ROAS
- Comparativo por campanha: Mensagens vs Visitas ao Perfil
- Análise de eficiência: Custo por resultado

---

## 🔍 Diagnóstico da Base Atual

Durante a exploração inicial da planilha (`Base_de_Dados_Firmare.csv`), identificamos:

- **4 registros** preenchidos (Jan–Fev 2026), 2 clientes: Dra. Joice Fraga e Dra. Renata Bastos
- **Apenas 12 dos 50 campos** com dados consistentes
- Bloco financeiro, comercial e tráfego pago **completamente vazios** na planilha
- Dados ricos existem nos PDFs mas **não estão sendo inseridos** na planilha
- 15 colunas sem nome (`Coluna 35` a `Coluna 49`) — sem uso definido

**Conclusão:** a reestruturação em abas temáticas é o primeiro passo antes de qualquer desenvolvimento.

---

## 🚀 Como Rodar Localmente

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/firmare-dashboard.git
cd firmare-dashboard

# Abra diretamente no navegador (sem servidor necessário)
open index.html

# Ou use um servidor local simples
npx serve .
```

> ⚠️ Para que os dados carreguem, a planilha Google Sheets precisa estar **publicada na web** (Arquivo → Compartilhar → Publicar na web → CSV).

---

## ⚙️ Configuração

Edite o arquivo `js/config.js` para apontar para o Sheets correto:

```javascript
const CONFIG = {
  SHEET_ID: "1fSgWk1_NkDzm8ynnboz3SGZKjJSBtfDWaXm8AulYDak",
  ABAS: {
    financeiro: "financeiro",
    comercial:  "comercial",
    marketing:  "marketing",
    trafego:    "trafego",
    config:     "config"
  },
  CLIENTE_PADRAO: "Dra. Joice Fraga"
};
```

---

## 🎨 Design

O dashboard segue a identidade visual da Firmare:

| Token | Valor |
|---|---|
| Cor primária | `#6B3A1F` (marrom) |
| Cor de destaque | `#C9A24B` (dourado) |
| Fundo | `#F5F0E8` (creme) |
| Tipografia display | Playfair Display |
| Tipografia corpo | DM Sans |

---

## 📅 Roadmap

- [x] Exploração da base de dados e diagnóstico
- [x] Definição da arquitetura de abas do Sheets
- [x] README e documentação inicial
- [ ] Reestruturação do Google Sheets em abas temáticas
- [ ] Conexão HTML → Sheets via CSV público
- [ ] Módulo Financeiro (HTML + JS)
- [ ] Módulo Comercial + Funil
- [ ] Módulo Marketing
- [ ] Módulo Tráfego Pago
- [ ] Filtro por cliente (multi-cliente)
- [ ] Filtro por período (semana / mês)
- [ ] Análise estratégica gerada por IA (Claude API)
- [ ] Deploy via GitHub Pages

---

## 🤝 Desenvolvido por

**Firmare Gestão Empresarial** · [firmaregestao.com](https://firmaregestao.com) · @firmare.gestao
