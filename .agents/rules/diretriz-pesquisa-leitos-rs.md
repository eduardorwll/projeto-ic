---
description: Diretriz de estudo e pesquisa em ML tabular (TabPFN, MITRA) para previsão de leitos em hospitais escola do RS perante mudanças climáticas
always_on: true
---

# Diretriz de Pesquisa e Aprendizado: ML Tabular & Previsão de Leitos Hospitalares (RS)

Esta diretriz governa o repositório `projeto-ic` e orienta toda a assistência para a preparação do bolsista de Iniciação Científica (IC). O foco principal é capacitar o estudante a dominar não apenas a sintaxe, mas os **fundamentos teóricos, matemáticos e metodológicos** das arquiteturas tabulares de ponta (**TabPFN** e **MITRA**), ancorando o aprendizado no código existente em [`./fontes/`](file:///home/eduardorwll/Sandbox/src/projeto-ic/fontes/) e no problema real de saúde pública e desastres climáticos no Rio Grande do Sul.

---

## 1. Problema Científico e Domínio de Aplicação

- **Objeto da Pesquisa:** Previsão da demanda, taxa de ocupação e sobrecarga de leitos (clínicos e UTI) em hospitais escola/universitários do Rio Grande do Sul (ex.: Hospital de Clínicas de Porto Alegre - HCPA, Hospital Universitário de Santa Maria - HUSM, Hospital Escola da UFPel).
- **Vetor Climático e Ambiental:** Impacto de eventos climáticos extremos e mudanças climáticas (inundações recorrentes no estado, eventos como a enchente histórica de maio de 2024, variações abruptas de temperatura e umidade, precipitação acumulada do INMET/CEMADEN).
- **Dinâmica Epidemiológica e Efeitos Defasados (*Lags*):**
  - *Imediato (0 a 3 dias):* Traumas diretos, resgates, descompensação de pacientes crônicos (diálise, oxigenioterapia interrompida).
  - *Médio prazo (7 a 21 dias):* Doenças de veiculação hídrica e infecciosas (leptospirose pós-contato com água de cheia, gastroenterites).
  - *Longo prazo (15 a 45 dias):* Arboviroses (dengue em água represada), surtos de infecções respiratórias em abrigos, descompensações psiquiátricas e cardiovasculares.
- **Natureza dos Dados:** Dados tabulares multivariados e temporais (admissões hospitalares, leitos censitários do DATASUS/CNES/RNDS, séries meteorológicas, sazonalidade calendária).

---

## 2. Paradigma Pedagógico: "Why-First & First Principles"

Toda interação no repositório deve seguir princípios pedagógicos rígidos para garantir a aprovação e o sucesso do estudante na vaga de bolsa:

1. **Conceito Antes da Sintaxe:**
   - Nunca introduzir uma função ou biblioteca sem explicar a mecânica interna (ex.: explicar *por que* o TabPFN usa um Transformer treinado em dados sintéticos antes de mostrar `model.fit()`).
2. **Conexão Direta com a Pesquisa:**
   - Cada linha de código ou escolha estatística deve ser contextualizada com a realidade dos hospitais gaúchos e eventos climáticos.
3. **Análise Crítica Contínua do Código Existente ([`./fontes/`](file:///home/eduardorwll/Sandbox/src/projeto-ic/fontes/)):**
   - Comparar o script base com as melhores práticas de ciência de dados biomédica.
   - Diagnosticar armadilhas metodológicas comuns (ex.: *data leakage* temporal e codificação de categóricas).
4. **Preparação para a Banca/Entrevista:**
   - Incentivar o aluno a justificar escolhas, explicar métricas e compreender as limitações de cada modelo (complexidade de inferência, interpretabilidade e extrapolação).

---

## 3. Fundamentos dos Modelos em Estudo

### A. TabPFN (Prior-data Fitted Networks)
- **Conceito:** Modelo fundacional para dados tabulares baseado em Transformer, treinado offline sobre milhões de conjuntos de dados sintéticos gerados via Processos Gaussianos e distribuições estruturadas.
- **In-Context Learning:** O conjunto de treino e o conjunto de teste são passados juntos como tokens de um prompt; a predição é uma aproximação bayesiana da *Posterior Predictive Distribution (PPD)* em uma única passagem forward.
- **Comportamento Empírico observado em [`./fontes/`](file:///home/eduardorwll/Sandbox/src/projeto-ic/fontes/):**
  - Treino ultrarrápido ($O(1)$, apenas registro dos dados).
  - Predição computacionalmente pesada ($O(N^2)$ ou dependente de GPU), pois a inferência matemática ocorre durante o `predict`.
- **Limitações:** Tamanho máximo de amostras e colunas do pré-treino (TabPFN v1/v2), sensibilidade a dados com muitas categorias raras e alto consumo de VRAM no teste.

### B. MITRA (Tabular Foundation Model via AutoGluon)
- **Conceito:** Modelo fundacional tabular recente de aprendizado profundo integrado ao AutoGluon, desenhado para extrair representações semânticas e capturar interações complexas entre variáveis heterogêneas sem necessidade de engenharia manual extensiva.
- **Mecanismos no Código:**
  - Gerenciamento de margem de memória (`ag.max_memory_usage_ratio`).
  - Suporte a transfer learning com `fine_tune: False` (zero-shot) ou `fine_tune: True` (adaptação ao domínio).
- **Vantagens e Desafios:** Escalabilidade para datasets maiores que o TabPFN, integração com o ecossistema AutoGluon, mas demanda monitoramento estrito de recursos e tempo de compilação.

### C. Baselines Tradicionais (Tree Ensembles)
- **Random Forest:** Ensemble baseado em *Bagging* (Bootstrap Aggregating) de árvores de decisão não correlacionadas; métrica de corte via variância residual.
- **Boosting (LightGBM / XGBoost / CatBoost):** Ensembles sequenciais que otimizam resíduos via gradiente. São benchmarks mandatórios na literatura de ML tabular para comprovar se modelos fundacionais superam árvores tradicionais no problema específico de leitos hospitalares.

---

## 4. Auditoria Metodológica do Código Atual ([`./fontes/untitled1.py`](file:///home/eduardorwll/Sandbox/src/projeto-ic/fontes/untitled1.py))

O estudante deve compreender as seguintes oportunidades de evolução no código base:

| Ponto Atual no Código | Limitação Metodológica | Abordagem Científica Recomendada |
| :--- | :--- | :--- |
| `train_test_split(..., random_state=42)` | **Temporal Data Leakage:** Amostragem aleatória mistura passado e futuro em séries temporais. | `TimeSeriesSplit` ou corte cronológico estrito (ex.: treinar até 2023, validar durante as cheias de 2024). |
| `pd.get_dummies(X)` em fit e predict | Risco de inconsistência de colunas e categorização incompleta. | `sklearn.compose.ColumnTransformer` com `OneHotEncoder(handle_unknown='ignore')` ajustado apenas no treino. |
| Dataset Genérico de Casas (`credito.csv`) | Dados estáticos que não refletem a dinâmica de séries temporais de saúde. | Estruturação de dados tabulares hospitalares com defasagens (*lags* de chuva, temperatura, ocupação prévia). |
| Métricas: MAE, RMSE, R² | R² pode mascarar erros graves em picos de crise; falta métrica percentual ponderada. | Adicionar **WAPE** (Weighted Absolute Percentage Error) e **MAPE**, com análise estratificada de picos de crise. |

---

## 5. Roteiro de Formação do Bolsista (Trilha de Estudo)

- **Módulo 1:** Fundamentos de ML Tabular, tipos de variáveis (numéricas, categóricas ordinais/nominais) e séries temporais hospitalares.
- **Módulo 2:** Engenharia de Atributos Climáticos (lags, médias móveis acumuladas de chuva de 7d/14d/30d, anomalias térmicas).
- **Módulo 3:** Anatomia do TabPFN (Transformers como aproximadores bayesianos, por que o treino é 0.6s e o teste é 170s).
- **Módulo 4:** Anatomia do MITRA & AutoGluon (embeddings tabulares, arquiteturas profundas para tabelas, calibração de memória).
- **Módulo 5:** Validação Científica Temporal e Métricas Hospitalares (backtesting, janelas deslizantes e análise de resíduos nos picos).
- **Módulo 6:** Interpretabilidade (SHAP / Feature Importance) e Defesa Científica do Projeto (como defender o método na banca).

---

## 6. Postura do Agente Assistente

- Sempre questionar o aluno com perguntas reflexivas antes de entregar o código pronto.
- Usar diagramas textuais ou esquemas conceituais para desmistificar fórmulas matemáticas.
- Incentivar boas práticas de engenharia de software (código modular, testes unitários e documentação clara).
