# Projeto IC: Previsão de Leitos Hospitalares (RS) & Modelos Tabulares (TabPFN, MITRA, Google TabFM)

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Research: IC](https://img.shields.io/badge/Pesquisa-Inicia%C3%A7%C3%A3o%20Cient%C3%ADfica-green.svg)]()
[![Focus: Saúde Pública RS](https://img.shields.io/badge/Dom%C3%ADnio-Sa%C3%BAde%20P%C3%BAblica%20%26%20Clima-red.svg)]()

Repositório de Iniciação Científica (IC) focado na **modelagem preditiva da demanda e taxa de ocupação de leitos hospitalares** (clínicos e de UTI) em hospitais universitários e de ensino do **Rio Grande do Sul** (ex.: Hospital de Clínicas de Porto Alegre - HCPA, Hospital Universitário de Santa Maria - HUSM, Hospital Escola UFPel) frente a **eventos climáticos extremos e mudanças climáticas**.

---

## 🔬 Contexto e Missão da Pesquisa

O Rio Grande do Sul enfrenta desastres hidrometeorológicos recorrentes e severos (como as inundações históricas de maio de 2024 e variações térmicas extremas). O impacto desses eventos na demanda de leitos do SUS se manifesta em múltiplas defasagens temporais (*lags*):

- **Imediato (0 a 3 dias):** Traumas, hipotermia, afogamentos e descompensação aguda de doentes crônicos por interrupção de tratamento (hemodiálise, perda de insulina/refrigeração).
- **Intermediário (7 a 21 dias):** Doenças de veiculação hídrica pós-contato com água de cheia (pico clássico de **leptospirose** no RS) e gastroenterites agudas.
- **Longo Prazo (15 a 45 dias):** Arboviroses (dengue em água parada), surtos de infecções respiratórias em abrigos, descompensações cardiovasculares e psiquiátricas.

O objetivo do projeto é comparar o desempenho de **Foundation Models para dados tabulares** contra modelos tradicionais de ensemble para antecipar sobrecargas com 7 a 21 dias de antecedência.

---

## 🤖 Modelos em Estudo

1. **TabPFN (Prior Labs / Hollmann et al., Nature & ICLR):**
   - Foundation Model tabular baseado em Transformer.
   - Aproximação da *Posterior Predictive Distribution (PPD)* bayesiana em modo *In-Context Learning (ICL)*.
   - Treino instantâneo ($O(1)$) com inferência forward contendo estimativa nativa de quantis de incerteza ($Q_{0.10}, Q_{0.50}, Q_{0.90}$).

2. **MITRA (Tabular Foundation Model via AutoGluon):**
   - Modelo tabular profundo com representações latentes densas (*deep embeddings*) para colunas e linhas.
   - Suporte a execução *Zero-Shot* (`fine_tune: False`) e adaptação supervisionada (*Fine-Tuning*), com gestão de limites de memória (`ag.max_memory_usage_ratio`).

3. **Google TabFM (Google Research, 2026):**
   - Foundation model tabular de 400 milhões de parâmetros treinado em Modelos Causais Estruturais (SCMs).
   - Inferência zero-shot in-context via PyTorch/JAX e extensão *TabFM-Auto* com agentes LLM (Gemini) para autoevolução de pipelines.

4. **Baselines Tradicionais:**
   - `RandomForestRegressor` (Bagging), `LightGBM` e `CatBoost` (Gradient Boosting).

---

## 📁 Estrutura do Repositório

```text
projeto-ic/
├── README.md                      # Apresentação do projeto e documentação
├── MISSION.md                     # Missão da pesquisa, escopo e critérios de sucesso
├── RESOURCES.md                   # Curadoria de bibliografia primária (papers e livros)
├── NOTES.md                       # Caderno de anotações e preferências
├── GEMINI.md / AGENTS.md          # Contratos e diretrizes operacionais dos agentes
├── .gitignore                     # Filtros de arquivos temporários, caches e dados
├── .agents/
│   ├── rules/
│   │   └── diretriz-pesquisa-leitos-rs.md  # Diretriz formal de integridade e TDD
│   └── skills/                    # Catálogo de skills integrado ao Sandbox
├── fontes/                        # Scripts e notebooks iniciais de experimentação
│   ├── untitled1.py               # Benchmark inicial de wrappers (RF, TabPFN, MITRA)
│   └── Untitled1.ipynb            # Notebook Google Colab com logs de execução
├── lessons/                       # Trilha pedagógica interativa em HTML (estilo Tufte)
│   ├── 0001-conteudo-programatico-ml-tabular-leitos-rs.html
│   ├── 0002-ciclo-1-dados-temporais-lags-e-leakage.html
│   ├── 0003-ciclo-2-anatomia-e-teoria-do-tabpfn.html
│   ├── 0004-ciclo-3-anatomia-do-mitra-e-autogluon.html
│   ├── 0005-ciclo-4-validacao-cientifica-tdd-e-defesa-banca.html
│   └── 0006-ciclo-especial-tabfm-google-research.html
├── reference/                     # Cheat sheets de referência técnica rápida
│   ├── tabpfn-cheat-sheet.html
│   ├── mitra-autogluon-cheat-sheet.html
│   ├── temporal-validation-cheat-sheet.html
│   └── tabfm-google-cheat-sheet.html
└── assets/
    └── style.css                  # Estilização visual unificada (Tufte/Acadêmico)
```

---

## 📖 Trilha de Aprendizado e Lições Interativas

O repositório inclui uma suíte completa de lições conceituais construídas sob o framework pedagógico `/teach`, abordando tanto a teoria matemática quanto o código:

- **[Lição 0001: Conteúdo Programático & Mapeamento de Bibliotecas](lessons/0001-conteudo-programatico-ml-tabular-leitos-rs.html)**
- **[Lição 0002: Ciclo 1 — Séries Temporais, Lags Climáticos & Zero Data Leakage](lessons/0002-ciclo-1-dados-temporais-lags-e-leakage.html)**
- **[Lição 0003: Ciclo 2 — Anatomia e Teoria do TabPFN (Prior Labs)](lessons/0003-ciclo-2-anatomia-e-teoria-do-tabpfn.html)**
- **[Lição 0004: Ciclo 3 — MITRA & Modelos Fundacionais no AutoGluon](lessons/0004-ciclo-3-anatomia-do-mitra-e-autogluon.html)**
- **[Lição 0005: Ciclo 4 — Validação Científica, TDD & Guia de Defesa na Banca](lessons/0005-ciclo-4-validacao-cientifica-tdd-e-defesa-banca.html)**
- **[Lição 0006: Módulo Especial — Google TabFM (400M Parâmetros & SCMs)](lessons/0006-ciclo-especial-tabfm-google-research.html)**

---

## ⚡ Como Visualizar as Lições Localmente

Para abrir qualquer lição no navegador:

```bash
# Abrir o sumário programático
xdg-open lessons/0001-conteudo-programatico-ml-tabular-leitos-rs.html

# Ou visualizar os cheat sheets
xdg-open reference/tabpfn-cheat-sheet.html
```

---

## ⚙️ Requisitos e Instalação

```bash
# Clonar o repositório
git clone https://github.com/eduardorwll/projeto-ic.git
cd projeto-ic

# Criar ambiente virtual
python -m venv .venv
source .venv/bin/activate

# Instalar dependências essenciais
pip install pandas scikit-learn tabpfn autogluon.tabular pytest
```

---

## ⚖️ Licença

Este projeto é desenvolvido para fins acadêmicos e de pesquisa científica sob a licença [MIT](LICENSE).
