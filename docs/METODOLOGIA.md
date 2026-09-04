# Metodologia

## 1. Pré-processamento
Os 15 números sorteados em cada concurso (`Bola1`...`Bola15`) são convertidos em uma matriz binária de 25 colunas (uma por dezena possível), indicando presença (1) ou ausência (0) em cada concurso.

## 2. Engenharia de atributos
Para cada concurso são calculados atributos agregados, entre eles:

| Atributo | Descrição |
|---|---|
| `pares` / `impares` | Quantidade de dezenas pares e ímpares sorteadas |
| `baixos` / `altos` | Dezenas de 1–12 vs. 13–25 |
| `primos` | Quantidade de números primos sorteados |
| `fibonacci` | Quantidade de números da sequência de Fibonacci sorteados |
| `moldura` / `centro` | Posição no volante 5×5 (borda vs. centro) |
| `mult_3` / `mult_5` | Quantidade de múltiplos de 3 e de 5 |
| `soma` / `std` | Soma e desvio padrão das dezenas sorteadas |
| gaps | Concursos consecutivos sem que uma dezena seja sorteada |

## 3. Modelagem
Dois classificadores multi-rótulo são treinados via `MultiOutputClassifier`:

- **Random Forest** (`RandomForestClassifier`)
- **Regressão Logística** (`LogisticRegression`)

Os últimos concursos do histórico são reservados como conjunto de teste. O desempenho é avaliado por acurácia, precisão, recall, F1-score e média de acertos por concurso.

## 4. Previsão
O modelo com melhor F1-score é usado para gerar a previsão do próximo concurso. A previsão é comparada às médias históricas de cada atributo e cruzada com a análise de gaps e frequência para destacar números de maior "confiança" e sugerir jogos.

## 5. Limitações
Sorteios de loteria são processos aleatórios; os atributos e modelos aqui descritos capturam padrões estatísticos do histórico, não relações causais que permitam prever o próximo resultado com confiabilidade.
