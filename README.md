# Esteira de Machine Learning — Classificação de Filmes (Colorido × Preto-e-Branco)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/antonioojunior26/esteira-ml-filmes/blob/main/Esteira_ML_Filmes.ipynb)

## Objetivo

Implementar uma esteira completa de aprendizado de máquina: estatística descritiva, preparação dos dados, divisão em treino/validação/teste, treinamento de um classificador, avaliação com matriz de confusão e predição com o modelo implantado.

O problema é **classificação binária**: prever se um filme é **colorido** (`color`) ou **preto-e-branco** (`black-and-white`) a partir de metadados.

## Base de dados

- **Fonte:** [Movie Metadata: Genre, Crew, Color & Tech Specs](https://www.kaggle.com/datasets/danielaijdkx/movie-metadata-genre-crew-color-tech-specs/data) — Kaggle, Daniel Silalahi.
- **Licença:** CC0 1.0 (domínio público). Dados originados do Wikidata.
- **Tamanho:** 26.545 filmes × 30 colunas na tabela principal (`movies.csv`).
- O dataset também contém `movie_genres.csv`, `movie_crew.csv`, `movie_cast.csv` e `movie_awards.csv`; o notebook usa a tabela principal.

## Estrutura do repositório

```text
esteira-ml-filmes/
├── Esteira_ML_Filmes.ipynb        # notebook já executado, com saídas salvas
├── Roteiro_Apresentacao_5min.md   # roteiro cronometrado para apresentação
├── requirements.txt               # dependências Python
└── .gitignore                     # evita subir dados e artefatos gerados
```

Artefatos **gerados na execução** e não versionados: `dados/` (CSVs baixados) e `modelo_final.joblib` (modelo serializado).

## Como executar

### Local

```powershell
pip install -r requirements.txt
jupyter notebook Esteira_ML_Filmes.ipynb
```

No Jupyter/VS Code: `Kernel → Restart & Run All`. O notebook procura `dados/movies.csv`; se não existir, faz o download automático da API pública do Kaggle com `curl` e extrai o arquivo.

### Google Colab

Clique no badge **Open In Colab** no topo (ou abra o `.ipynb` pelo Colab) e execute `Ambiente de execução → Executar tudo`. Se o download automático for bloqueado, o notebook oferece upload manual de `movies.csv`.

## Pipeline resumido

1. **Estatísticas descritivas** da base original (`shape`, `dtypes`, `describe`, valores ausentes, distribuição das classes).
2. **Transformação nas linhas:** remoção de duplicatas, rótulos `mixed`/vazios e valores extremos (26.545 → 22.272 filmes).
3. **Transformação nas colunas:** alvo binário, contadores derivados de listas (`n_genres`, `n_directors`, etc.), `main_genre`, `log1p` dos valores monetários e exclusão de identificadores e de `color_type` (vazamento de rótulo).
4. **Divisão estratificada:** 60% treino / 20% validação / 20% teste.
5. **Treinamento:** `ColumnTransformer` (imputação, padronização, one-hot) + `RandomForestClassifier` (200 árvores, `class_weight='balanced'`, `random_state=42`).
6. **Avaliação:** acurácia, acurácia balanceada, relatório de classificação e matriz de confusão no conjunto de teste.
7. **Implantação:** serialização com `joblib`, recarga do artefato e predição de filmes novos.

## Resultados

| Métrica (conjunto de teste) | Valor |
|---|---:|
| Acurácia | **92,39%** |
| Acurácia balanceada | 93,07% |
| F1 — preto-e-branco | 0,805 |
| F1 — colorido | 0,953 |
| Baseline (sempre prever “colorido”) | 83,3% |

Matriz de confusão (linhas = classe real, colunas = prevista):

| | previsto: preto-e-branco | previsto: colorido |
|---|---:|---:|
| real: preto-e-branco | 700 | 44 |
| real: colorido | 295 | 3.416 |

**Predições do modelo implantado:** filme moderno → colorido (94,1% de confiança); filme de 1943 → preto-e-branco (91,5%).

> Observação: o ano de lançamento é um preditor forte (filmes antigos tendem a ser preto-e-branco), portanto parte do desempenho reflete esse padrão histórico.

## Licença e créditos

Dataset: CC0 1.0, cortesia de Daniel Silalahi / Wikidata. Código e notebook: uso acadêmico livre.
