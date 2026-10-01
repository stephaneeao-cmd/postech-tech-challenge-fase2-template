# results/

| Pasta | Conteúdo | Versionado? |
|---|---|---|
| `figures/` | gráficos exportados (`.png`) | sim |
| `metrics/` | tabelas comparativas (`.csv` / `.json`) | sim |
| `models/` | modelos serializados (`.pkl` / `.joblib`) | **não** (ver `.gitignore`) |

Modelos podem ser regenerados rodando os notebooks; figuras e métricas ficam versionadas
para que o avaliador veja os resultados sem executar nada.

## Como reproduzir

Execute os notebooks na ordem `01_eda.ipynb` → `02_preprocessamento.ipynb` →
`03_modelagem.ipynb` → `04_avaliacao.ipynb`. O notebook 02 gera o dataset tratado;
o 03 compara os modelos e salva `models/best_model.joblib`; o 04 carrega esse modelo
para gerar as métricas e gráficos do teste. O arquivo `.joblib` é ignorado pelo Git,
então é necessário executar o notebook 03 antes do 04 em um ambiente novo.

O alvo marca `TARGET = 1` quando há pelo menos um atraso de 60 dias ou mais no
histórico observado. `TARGET = 0` significa que não foi observado atraso dessa
gravidade; não significa necessariamente que o cliente nunca atrasou pagamentos.

O dicionário das duas bases e a correspondência entre nomes originais e nomes em
português estão no notebook 01. No dataset tratado, idade e tempo de trabalho estão
em anos e aparecem como `IDADE_ANOS` e `TEMPO_TRABALHO_ANOS`; os CSVs brutos mantêm
os nomes originais. No EDA, o gráfico de distribuição converte a idade para anos
somente para facilitar a leitura; a matriz de correlação usa idade e tempo de
trabalho nos valores originais em dias.

## Arquivos gerados

As figuras são exportadas pelos notebooks 01, 03 e 04:

- `figures/01_distribuicoes.png` — idade, renda e gênero.
- `figures/02_correlacoes.png` — correlações entre variáveis numéricas.
- `figures/03_valores_extremos.png` — renda, filhos e tamanho da família.
- `figures/04_balanceamento_alvo.png` — quantidade de clientes em cada classe.
- `figures/05_comparacao_modelos.png` — F1 médio dos cinco modelos na validação cruzada por perfil.
- `figures/06_matriz_confusao.png` e `figures/07_curva_roc.png` — avaliação no conjunto de teste.
- `figures/08_importancia_variaveis.png` — variáveis mais usadas pelo modelo selecionado.

As tabelas ficam em `metrics/`:

- `validacao_cruzada.csv` — recall, F1 e balanced accuracy em divisões aleatórias e por perfil. A divisão por perfil mantém características idênticas juntas; ela é mais rigorosa e pode resultar em métricas menores, pois testa combinações que o modelo não viu no treino.
- `analise_perfis_repetidos.csv` — contagem de perfis repetidos e perfis com valores diferentes de `TARGET`.
- `metricas_teste.csv` — métricas do modelo selecionado no conjunto de teste.
- `importancia_variaveis.csv` — importância das variáveis do modelo selecionado.

O modelo `models/best_model.joblib` é salvo pelo notebook 03 e permanece fora do Git,
conforme a regra de `.gitignore`.
