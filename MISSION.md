# Mission: Dominar ML Tabular (TabPFN, MITRA) para Previsão de Leitos Hospitalares sob Mudanças Climáticas no RS

## Why
Conquistar a vaga de bolsa de Iniciação Científica (IC) demonstrando domínio conceitual, matemático e prático sobre Foundation Models para dados tabulares (TabPFN e MITRA) e engenharia de dados temporais em saúde, sendo capaz de justificar escolhas metodológicas, interpretar resultados e construir pipelines preditivos para o SUS em hospitais universitários do RS.

## Success looks like
- Explicar com clareza intuitiva e matemática como o TabPFN realiza aproximação bayesiana da PPD via Transformers sem treino clássico, e por que seu fit é instantâneo mas a predição é custosa.
- Explicar como o MITRA no AutoGluon lida com representações tabulares profundas, fine-tuning e controle de margem de memória (`ag.max_memory_usage_ratio`).
- Identificar e eliminar qualquer forma de *Temporal Data Leakage* no pipeline de dados, implementando divisão temporal (`TimeSeriesSplit`) e engenharia de defasagens (*lags* climáticos do RS: 7d, 14d, 21d).
- Refatorar a base inicial em [`./fontes/`](file:///home/eduardorwll/Sandbox/src/projeto-ic/fontes/) para um framework modular, testado via TDD e reprodutível.
- Responder com segurança e fundamentação científica às perguntas da banca examinadora da bolsa.

## Constraints
- Ambiente de execução com restrições de tempo/memória (especialmente para TabPFN e AutoGluon MITRA).
- Dados do Rio Grande do Sul possuem forte impacto sazonal e quebras estruturais extremas (como a enchente histórica de maio de 2024).
- Aprendizado deve priorizar retenção de longo prazo (*storage strength*) em vez de memorização mecânica de sintaxe (*fluency*).

## Out of scope
- Treinamento de LLMs generativos de linguagem ou modelos de visão computacional.
- Deploy em infraestrutura de nuvem em larga escala de nível corporativo (o foco é prototipagem e validação científica de pesquisa).
- Deep learning para séries temporais contínuas de alta frequência (EEG, ECG).
