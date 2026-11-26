# Roteiro de apresentação — 5 minutos (Esteira de ML: filmes coloridos × preto-e-branco)

**Limite máximo: 5:00.** Fale até **4:30** e deixe **0:30** de margem. Use alarmes no celular em 4:00 e 4:30.

Regra: **7 slides, no máximo 2 frases por slide.** Não leia código — mostre só a saída já executada.

---

## Roteiro cronometrado

### 0:00–0:30 | Abertura
**Mostrar:** título do notebook.
**Fala:** “Bom dia. Apresento uma esteira de aprendizado de máquina com filmes do Kaggle: preparação dos dados, treino, avaliação e predição com o modelo implantado. O objetivo é classificar filmes como coloridos ou preto-e-branco.”

### 0:30–1:20 | Base e estatísticas descritivas
**Mostrar:** `value_counts` de `color_type` e um trecho do `describe`.
**Fala:** “A base tem **26.545 filmes e 30 colunas**. Na descrição geral: **18.997 coloridos, 4.295 preto-e-branco, 656 mixed e 2.597 sem rótulo**, além de muitos valores ausentes e extremos. Isso mostrou a necessidade de limpar os dados.”

### 1:20–2:20 | Transformações nas linhas e nas colunas
**Mostrar:** print `26.545 → 22.272` e a criação do `target`.
**Fala:** “Nas **linhas**, removi duplicatas, rótulos ambíguos e valores extremos: cai para **22.272 filmes**, 16,1% a menos. Nas **colunas**, criei o alvo binário, contadores de gêneros, diretores e idiomas, o log de orçamento e bilheteria, e retirei identificadores e a própria `color_type` para não vazar a resposta. Ficaram **20 preditores**.”

### 2:20–3:00 | Divisão e modelo
**Mostrar:** print dos splits e o `Pipeline`.
**Fala:** “Dividi em **60% treino, 20% validação e 20% teste**, de forma estratificada. Treinei um **RandomForest de 200 árvores** dentro de um pipeline com imputação, padronização e one-hot, usando `class_weight='balanced'` porque preto-e-branco é minoritária.”

### 3:00–4:10 | Avaliação: acurácia e matriz de confusão
**Mostrar:** matriz de confusão e a linha da acurácia.
**Fala:** “No teste, a **acurácia foi 92,39%** e a balanceada, **93,07%**. Na matriz: dos **744** filmes realmente preto-e-branco, **700 acertos e 44 erros**; dos **3.711** coloridos, **3.416 acertos e 295 erros**. Está quase 9 pontos acima do baseline de 83,3%, embora a classe preto-e-branco seja mais difícil.”

### 4:10–4:40 | Modelo implantado e predição
**Mostrar:** as duas predições.
**Fala:** “Salvei o modelo com `joblib`, recarreguei do disco e testei filmes novos: um moderno previsto como **colorido com 94,1%** e um de 1943 como **preto-e-branco com 91,5%**.”

### 4:40–5:00 | Encerramento
**Mostrar:** slide final com o resumo dos requisitos.
**Fala:** “Resumo: estatística, transformações em linhas e colunas, três conjuntos, treino, matriz de confusão e predição com o modelo implantado. Tudo no notebook executado. Obrigado.”

---

## Se atrasar (nesta ordem)

1. Aos **3:30**: corte a frase do baseline e do F1; vá direto da matriz para a predição.
2. Aos **4:00**: faça só a primeira predição e encerre.
3. Aos **4:30**: pare imediatamente, mesmo que falte o encerramento.

---

## Versão de 60 segundos (plano B)

“Base do Kaggle com 26.545 filmes. Descrevi os dados, limpei 16% das linhas e criei 20 preditores. Separei 60/20/20, treinei um RandomForest e avaliei no teste: **92,39% de acurácia**, com matriz de 700/44 e 3.416/295. Salvei o modelo com `joblib` e previ filmes novos: 94,1% colorido e 91,5% preto-e-branco.”

---

## Números indispensáveis

| Item | Valor |
|---|---|
| Base | 26.545 filmes × 30 colunas |
| Classes originais | 18.997 color / 4.295 P&B / 656 mixed / 2.597 vazios |
| Após limpeza | 22.272 filmes (18.555 color / 3.717 P&B) |
| Conjuntos | 13.363 treino / 4.454 validação / 4.455 teste |
| Modelo | RandomForest, 200 árvores, `balanced`, seed 42 |
| Acurácia (teste) | **92,39%** (balanceada 93,07%) |
| Matriz | 700/44 em P&B; 3.416/295 em colorido |
| Predições | 94,1% colorido; 91,5% P&B |

**Dica final:** ensaie uma vez cronometrando. Se passar de 4:30 no ensaio, use a versão de 60 segundos como fala principal e estique apenas os números da matriz.
