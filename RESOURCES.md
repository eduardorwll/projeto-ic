# Tabular ML, Climate & Hospital Bed Forecasting Resources

## Knowledge

### Tabular Foundation Models & In-Context Learning
- [Paper: _TabPFN: A Transformer That Solves Small Tabular Classification Problems in a Second_ (Hollmann et al., Nature / ICLR)](https://arxiv.org/abs/2207.01848)
  Artigo fundador do TabPFN. Use para: entender a aproximação bayesiana da Posterior Predictive Distribution (PPD), geração de dados sintéticos via Processos Gaussianos e complexidade in-context.
- [Paper: _TabPFN v2_ (Prior Labs)](https://arxiv.org/abs/2410.18041)
  Evolução para datasets maiores, regressão e aceleração de inferência. Use para: limites práticos, tokens e regressão.
- [Paper: _TabFM: A Zero-Shot Foundation Model for Tabular Data_ (Google Research, 2026)](https://arxiv.org/abs/2609.37959)
  Foundation Model tabular de 400M parâmetros do Google treinado em Modelos Causais Estruturais (SCMs). Use para: entender In-Context Learning com causalidade sintética, variantes TabFM+ e integração PyTorch/JAX/BigQuery.
- [Paper: _TabFM-Auto: Self-Evolving Pipelines for Tabular Foundation Models_ (Google Research, 2026)](https://arxiv.org/abs/2609.37989)
  Pipeline autoevolutivo unindo o TabFM com agentes LLM (Gemini). Use para: orquestração de pré-processamento de tabelas e seleção de contexto via LLMs.
- [Documentação Oficial do AutoGluon Tabular & MITRA](https://auto.gluon.ai/stable/tutorials/tabular/tabular-foundation-models.html)
  Guia do ecossistema AutoGluon para modelos fundacionais tabulares. Use para: parametrização do MITRA, `ag.max_memory_usage_ratio`, fine-tuning e ensembles.

### Temporal Modeling, Data Leakage & Health Informatics
- [Livro: _Forecasting: Principles and Practice_ (Hyndman & Athanasopoulos)](https://otexts.com/fpp3/)
  Texto padrão-ouro em previsão temporal. Use para: TimeSeriesSplit, janelas deslizantes (rolling origin), defasagens (lags), métricas WAPE e MAE.
- [Paper: _Leakage and the Reproducibility Crisis in Machine Learning-Based Science_ (Kapoor & Narayanan, Patterns)](https://doi.org/10.1016/j.patter.2023.100804)
  Referência essencial em integridade científica. Use para: diagnosticar e evitar data leakage temporal e de pré-processamento.
- [Boletins Epidemiológicos & Desastres Climáticos RS (CEVS/SES-RS / CEMADEN / INMET)](https://saude.rs.gov.br/)
  Dados e relatórios de monitoramento de enchentes, leptospirose e doenças respiratórias no RS. Use para: calibrar defasagens temporais (lags de 7 a 21 dias).

## Wisdom (Communities)

- [OpenML Tabular Benchmark & Repositories](https://www.openml.org/)
  Comunidade de benchmarks abertos para dados tabulares. Use para: avaliar baselines padronizados.
- [AutoGluon Discussion & GitHub](https://github.com/autogluon/autogluon)
  Fórum oficial de desenvolvedores do AutoGluon. Use para: troubleshooting de alocação de GPU/RAM e parâmetros de modelos tabulares profundos.
