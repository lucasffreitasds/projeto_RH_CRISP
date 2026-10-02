# Previsão de Risco de Desligamento — RH com CRISP-DM

**Status: em desenvolvimento — etapa inicial de análise dos dados.**

Estou desenvolvendo este projeto para investigar fatores associados à rotatividade de funcionários e, posteriormente, construir modelos que estimem o risco de desligamento.

Organizei o trabalho seguindo o **CRISP-DM**, começando pelo entendimento do negócio e dos dados. A proposta é conectar a análise técnica ao planejamento de ações de retenção pelo setor de Recursos Humanos.

A pergunta principal é: **como identificar funcionários com maior risco de saída e avaliar o impacto de uma possível ação de retenção?**

[Ver notebook](projeto_RH_CRISP.ipynb) · [Meu portfólio](https://lucasffreitasds.github.io/portfolio_projetos/)

## Dados

Utilizo o arquivo `HR-Employee-Attrition-balanced.csv`, com **1.761 registros e 35 colunas**. A base inclui informações sobre remuneração, cargo, satisfação, tempo de empresa, trajetória profissional e condições de trabalho.

A variável resposta é `Attrition`:

- **Yes:** registro de funcionário que saiu.
- **No:** registro de funcionário que permaneceu.

Na base, **528 registros apresentam desligamento**, correspondendo a **29,98% da amostra**. Essa proporção descreve o dataset utilizado; ainda preciso verificar sua origem e representatividade para interpretar os resultados em uma operação real.

## Desenvolvimento até agora

Nesta primeira etapa, trabalhei em:

1. **Separação dos dados:** divisão estratificada em 75% para treino e 25% para teste, com 1.320 e 441 registros, respectivamente.
2. **Entendimento do negócio:** construção de um cenário de referência para estimar custos de substituição e explorar o potencial de ações de retenção.
3. **Qualidade dos dados:** inspeção de dimensões, tipos e valores ausentes.
4. **Estatística descritiva:** cálculo de média, mediana, dispersão, assimetria e curtose dos atributos numéricos do treino.
5. **Formulação de hipóteses:** organização de 15 perguntas sobre perfil, cargo, gestão, satisfação e qualidade de vida.
6. **Engenharia de variáveis:** criação de indicadores de estabilidade profissional, renda relativa, satisfação, deslocamento e relacionamento com a gestão.
7. **Análise exploratória inicial:** construção de histogramas e boxplots para comparar distribuições entre os grupos com e sem desligamento.

Entre as variáveis criadas estão a renda em relação ao nível do cargo, a proporção da carreira passada na empresa, o tempo sem promoção em relação ao tempo no cargo e a combinação de horas extras com baixo envolvimento.

A preparação final dos dados, o treinamento dos modelos e a avaliação preditiva ainda serão desenvolvidos.

## Análise de negócio

Comecei pela estimativa de custo de substituição, utilizando o salário anual e multiplicadores definidos conforme o nível do cargo.

Também construí cenários conservador, moderado e otimista, variando três premissas:

- **Recall:** parcela dos desligamentos que um futuro modelo conseguiria identificar.
- **Precision:** proporção de alertas que corresponderia a desligamentos.
- **Taxa de retenção:** parcela dos casos identificados em que uma intervenção do RH conseguiria evitar a saída.

A intenção é entender como o desempenho do modelo, a efetividade da intervenção e os custos envolvidos se relacionam.

**Esses cenários são simulações.** Os valores de precision, recall e retenção foram definidos como premissas, e os resultados financeiros ainda precisam de revisão e validação.

## Ferramentas utilizadas

Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Pillow e Jupyter Notebook.

## Como executar

Utilizei **Python 3.13**. Com Python e Git instalados, clone o repositório:

```bash
git clone https://github.com/lucasffreitasds/projeto_RH_CRISP.git
cd projeto_RH_CRISP
```

Se usar Pyenv, ajuste `.python-version` para uma versão ou ambiente instalado na sua máquina. O arquivo atual referencia meu ambiente local, `milk_env`.

Crie e ative um ambiente virtual:

**Linux / macOS:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Windows — Prompt de Comando:**

```bat
py -3.13 -m venv .venv
.venv\Scripts\activate.bat
```

Instale as dependências e abra o JupyterLab:

```bash
python -m pip install -r requirements.txt
python -m pip install jupyterlab
python -m jupyterlab
```

Abra `projeto_RH_CRISP.ipynb`. Na seção de carregamento dos dados, substitua o caminho absoluto pela leitura relativa:

```python
df_raw = pd.read_csv("dataset/HR-Employee-Attrition-balanced.csv")
```

Execute o notebook a partir da raiz do repositório, usando o kernel do ambiente criado e seguindo a ordem das células.

## Limitações e próximos passos

Como o projeto ainda está no início, os principais pontos que preciso desenvolver ou revisar são:

- **Verificar a origem e a qualidade da base:** entender como essa versão foi construída e conferir identificadores repetidos, escalas de satisfação e possíveis inconsistências.

- **Revisar a divisão de treino e teste:** existem valores de `EmployeeNumber` presentes nos dois conjuntos. Preciso verificar o que essas repetições representam e evitar que registros do mesmo funcionário contaminem a avaliação.

- **Ajustar as variáveis de renda relativa:** atualmente, médias, medianas e desvios são calculados separadamente em cada conjunto. Vou utilizar as referências aprendidas no treino para transformar os demais dados.

- **Concluir a análise exploratória:** avaliar as hipóteses, investigar relações entre as variáveis e restringir as análises que orientam a modelagem ao conjunto de treino. Alguns gráficos atuais utilizam a base completa.

- **Revisar as variáveis criadas:** avaliar indicadores redundantes, divisões com denominadores próximos de zero e a contribuição de cada atributo para o problema.

- **Avançar para a modelagem:** preparar os dados em uma `Pipeline`, estabelecer um modelo de referência e comparar algoritmos com validação cruzada.

- **Revisar as simulações financeiras:** padronizar a moeda, alinhar a fórmula de ROI entre os cenários e validar custos e período de referência antes de interpretar os valores como estimativas anuais.

## Autor

**Lucas Ferreira de Freitas** — Cientista de Dados e Engenheiro Agrônomo.

[GitHub](https://github.com/lucasffreitasds) · [Portfólio](https://lucasffreitasds.github.io/portfolio_projetos/)

**Base utilizada:** [HR-Employee-Attrition-balanced.csv](dataset/HR-Employee-Attrition-balanced.csv).
