# LFquantum

Análise estatística e modelagem preditiva aplicada aos resultados históricos da **Lotofácil**, usando engenharia de atributos (features) e aprendizado de máquina (Random Forest e Regressão Logística).

## 📋 Sobre o projeto

O `LFquantum` é um notebook Python que recebe o histórico de concursos da Lotofácil (colunas `Bola1` a `Bola15`) e realiza:

- **Pré-processamento** dos dados em uma matriz binária (1–25) indicando quais dezenas saíram em cada concurso;
- **Engenharia de atributos**, incluindo:
  - Paridade (pares/ímpares), faixa (baixos/altos), números primos e de Fibonacci;
  - Posição no volante 5×5 (moldura, centro, diagonais);
  - Múltiplos de 3 e de 5, soma e desvio padrão das dezenas sorteadas;
  - Gaps (concursos sem sair) e frequência histórica de cada dezena;
- **Treinamento e avaliação de modelos** (`RandomForestClassifier` e `LogisticRegression`, via `MultiOutputClassifier`), com métricas de acurácia, precisão, recall e F1-score;
- **Análise de importância de atributos** a partir do Random Forest;
- **Geração de previsão** para o próximo concurso, com comparação frente às médias históricas, distribuição no volante e sugestões de jogos (principal e conservador).

## ⚠️ Aviso importante

Sorteios de loteria são eventos aleatórios e independentes: nenhum modelo estatístico ou de aprendizado de máquina pode prever com confiabilidade seu resultado. Este projeto tem finalidade **educacional e exploratória** — um estudo de padrões estatísticos, engenharia de atributos e comparação de modelos de classificação — e não deve ser interpretado como garantia de acerto nem como recomendação de aposta.

## 🛠️ Tecnologias

- Python 3
- pandas, numpy
- scikit-learn (RandomForestClassifier, LogisticRegression, MultiOutputClassifier)
- matplotlib, seaborn
- scipy

## 📦 Estrutura do repositório

```
LFquantum/
├── notebooks/
│   └── LFquantum.ipynb      # Notebook principal (análise, modelagem e previsão)
├── data/                    # Histórico de concursos (CSV) — não versionado
├── docs/                    # Documentação complementar
├── requirements.txt         # Dependências do projeto
├── LICENSE
└── README.md
```

## 🚀 Como usar

1. Clone o repositório:
   ```bash
   git clone https://github.com/<seu-usuario>/LFquantum.git
   cd LFquantum
   ```
2. Crie um ambiente virtual e instale as dependências:
   ```bash
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. Coloque o histórico de concursos da Lotofácil (separador `;`, colunas `Bola1`...`Bola15`) em `data/Lotof.csv`.
4. Abra o notebook em `notebooks/LFquantum.ipynb` no Jupyter, VS Code ou Google Colab e execute as células em ordem.
   - Se rodar fora do Google Colab, substitua o trecho de upload (`google.colab.files.upload()`) pela leitura direta do arquivo em `data/Lotof.csv`.

📌 Status

Experimental / Research

O projeto encontra-se em desenvolvimento e pode sofrer alterações na metodologia, features, modelos e critérios de avaliação.

⚠️ Limitações

O LFquantum deve ser interpretado como um experimento de Machine Learning aplicado a dados de loteria, e não como um sistema determinístico de previsão.

Existem limitações importantes:

Sorteios são eventos essencialmente aleatórios;
Frequência histórica não implica maior probabilidade futura;
"Números atrasados" não possuem necessariamente maior chance de serem sorteados;
Correlação histórica não significa causalidade;
Modelos de Machine Learning podem encontrar padrões espúrios;
As métricas utilizadas precisam ser interpretadas com cautela;
A metodologia não elimina a aleatoriedade do processo.

Portanto:

O objetivo do projeto é explorar padrões estatísticos e testar modelos preditivos sobre dados históricos, não garantir resultados de loteria.

🔮 Possíveis evoluções

O LFquantum pode ser expandido em diversas direções:

Validação walk-forward;
Cross-validation temporal;
XGBoost / LightGBM;
Redes neurais;
LSTM / Transformers para séries temporais;
Modelos probabilísticos;
Calibração de probabilidades;
SHAP para interpretabilidade;
Otimização de hiperparâmetros;
Ensemble de múltiplos modelos;
Backtesting automatizado;
Simulações Monte Carlo;
Otimização de combinações;
Análise de dependência entre dezenas;
Dashboard interativo;
API para geração automática de previsões;
Atualização automática dos resultados históricos.

Pipeline do projeto
                 ┌─────────────────┐
                 │   Lotof.csv     │
                 └────────┬────────┘
                          │
                          ▼
                ┌───────────────────┐
                │ Pré-processamento │
                └─────────┬─────────┘
                          │
                          ▼
                ┌───────────────────┐
                │ Matriz binária    │
                │     25 × N        │
                └─────────┬─────────┘
                          │
                          ▼
                ┌───────────────────┐
                │ Feature Engineering│
                └─────────┬─────────┘
                          │
                          ▼
                ┌───────────────────┐
                │ StandardScaler    │
                └─────────┬─────────┘
                          │
                ┌─────────┴─────────┐
                ▼                   ▼
        ┌───────────────┐   ┌───────────────┐
        │ Random Forest │   │   Logistic     │
        │               │   │  Regression    │
        └───────┬───────┘   └───────┬───────┘
                │                   │
                └─────────┬─────────┘
                          ▼
                  Comparação de modelos
                          │
                          ▼
                   Melhor modelo
                          │
                          ▼
                    Ranking 1–25
                          │
                          ▼
                    Top 18 dezenas
                          │
                          ▼
                Análise estatística
                          │
                          ▼
                 Sugestões de jogos

## 📊 Saída

O notebook imprime estatísticas descritivas, o comparativo entre os modelos treinados, a importância de cada atributo, e a previsão final para o próximo concurso — incluindo um jogo principal (18 dezenas) e uma versão conservadora (15 dezenas) baseada em critérios de confiança.

## 📄 Licença

Distribuído sob a licença MIT. Veja [LICENSE](LICENSE) para mais detalhes.
