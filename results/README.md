# results/

| Pasta | Conteúdo | Versionado? |
|---|---|---|
| `figures/` | gráficos exportados (`.png`) | sim |
| `metrics/` | tabelas comparativas (`.csv` / `.json`) | sim |
| `models/` | modelos serializados (`.pkl` / `.joblib`) | **não** (ver `.gitignore`) |

Modelos podem ser regenerados rodando os notebooks; figuras e métricas ficam versionadas
para que o avaliador veja os resultados sem executar nada.

## Arquivos gerados

As figuras são exportadas pelos notebooks 01, 03 e 04:

- `figures/01_distribuicoes.png` — idade, renda e gênero.
- `figures/02_correlacoes.png` — correlações entre variáveis numéricas.
- `figures/03_valores_extremos.png` — renda, filhos e tamanho da família.
- `figures/04_balanceamento_alvo.png` — quantidade de clientes em cada classe.
- `figures/05_comparacao_modelos.png` — F1 médio dos cinco modelos na validação cruzada.
- `figures/06_matriz_confusao.png` e `figures/07_curva_roc.png` — avaliação no conjunto de teste.
- `figures/08_importancia_variaveis.png` — variáveis mais usadas pelo modelo selecionado.

As tabelas ficam em `metrics/`:

- `validacao_cruzada.csv` — recall, F1 e balanced accuracy de cada modelo.
- `metricas_teste.csv` — métricas do modelo selecionado no conjunto de teste.
- `importancia_variaveis.csv` — importância das variáveis do modelo selecionado.

O modelo `models/best_model.joblib` é salvo pelo notebook 03 e permanece fora do Git,
conforme a regra de `.gitignore`.
