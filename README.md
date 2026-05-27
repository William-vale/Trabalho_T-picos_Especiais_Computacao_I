# 🔍 Análise Exploratória e Regressão — Homicídios Globais

> Projeto de análise de dados com Python utilizando a base oficial da **ONU (UNODC)** sobre homicídios intencionais no mundo.

---

## 📋 Sumário

- [Sobre o Projeto](#sobre-o-projeto)
- [Base de Dados](#base-de-dados)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Instalação e Execução](#instalação-e-execução)
- [Limpeza e Tratamento dos Dados](#limpeza-e-tratamento-dos-dados)
- [Análise Exploratória](#análise-exploratória)
  - [Pergunta 1 — Top 10 Países com Maiores Taxas de Homicídio](#pergunta-1--top-10-países-com-maiores-taxas-de-homicídio-2018-2022)
  - [Pergunta 2 — Homicídios de Mulheres em 2022](#pergunta-2--homicídios-de-mulheres-em-2022)
  - [Pergunta 3 — Regiões com Mais Homicídios](#pergunta-3--regiões-com-mais-homicídios)
  - [Pergunta 4 — Países com Menor Número de Homicídios por Sub-região](#pergunta-4--países-com-menor-número-de-homicídios-por-sub-região)
  - [Pergunta 5 — Países com Menor Mortalidade Feminina](#pergunta-5--países-com-menor-mortalidade-feminina)
- [Regressão](#regressão)
- [Decisões Metodológicas](#decisões-metodológicas)
- [Autores](#autores)

---

## Sobre o Projeto

Este projeto foi desenvolvido como trabalho acadêmico da disciplina de **Tópicos em Ciência de Dados**, com o objetivo de aplicar técnicas de **Análise Exploratória de Dados (EDA)** e **Regressão** sobre dados reais de criminalidade global.

A análise busca responder perguntas concretas sobre a distribuição de homicídios intencionais no mundo, identificar padrões regionais, diferenças de gênero e construir um modelo preditivo capaz de explicar a variação nas taxas de homicídio entre países.

Todo o código foi desenvolvido em **Python**, utilizando o ambiente **Google Colab**.

🔗 **Notebook no Google Colab:** [Acessar notebook](https://colab.research.google.com/drive/1uo1YFYDQhMhz49TFIhQDVmmgOhvNqqZQ?usp=sharing#scrollTo=RtpEfPn7I6NB)

---

## Base de Dados

| Atributo | Descrição |
|---|---|
| **Nome** | UNODC Crime and Criminal Justice Statistics |
| **Organização** | United Nations Office on Drugs and Crime |
| **Tema** | Homicídios Intencionais Globais |
| **Cobertura** | 190+ países |
| **Período** | Série histórica de décadas |
| **Formato** | CSV |
| **Acesso** | Público |

🔗 **Fonte oficial:** [UNODC Statistics](https://raw.githubusercontent.com/Atila-dev/teste-topicos/refs/heads/main/data_cts_intentional_homicide.csv)

### Principais colunas

| Coluna | Descrição |
|---|---|
| `Country` | Nome do país |
| `Iso3_code` | Código ISO3 do país / código regional |
| `Region` | Grande região geográfica (América, África, Ásia...) |
| `Subregion` | Sub-região geográfica |
| `Year` | Ano do registro |
| `Indicator` | Tipo de indicador (Victims of intentional homicide...) |
| `Dimension` | Dimensão da análise (Total, por mecanismo...) |
| `Category` | Categoria dentro da dimensão |
| `Sex` | Sexo da vítima (Total, Male, Female) |
| `Age` | Faixa etária (Total, 18-29, 30-44, 60+...) |
| `Unit of measurement` | Unidade: `Counts` ou `Rate per 100,000 population` |
| `VALUE` | Valor numérico do indicador |

---

## Tecnologias Utilizadas

- **Python 3** — linguagem principal
- **pandas** — manipulação e análise de dados
- **numpy** — operações numéricas
- **Google Colab** — ambiente de execução em nuvem

---

## Estrutura do Projeto

```
📦 projeto-homicidios-unodc/
├── 📄 perguntas1a5.py              # Código das perguntas 1 a 5 (EDA)
├── 📄 README.md                    # Este arquivo
├── 📊 dataset_homicidios_paises_tratado.csv     # Dataset de países (gerado)
└── 📊 dataset_homicidios_regioes_onu_tratado.csv # Dataset ONU (gerado)
```

---

## Instalação e Execução

### Pré-requisitos

```bash
pip install pandas numpy
```

### Executar localmente

```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
python perguntas1a5.py
```

### Executar no Google Colab

Acesse o link do notebook e execute as células na ordem. Os datasets tratados serão gerados automaticamente na sessão.

---

## Limpeza e Tratamento dos Dados

Antes de iniciar qualquer análise, o dataset original passou por um pipeline de limpeza e preparação.

### Etapas realizadas

**1. Cópia de segurança do dataset original**

```python
df_tratado = df_unodc.copy()
```

Trabalhamos sempre em uma cópia para preservar o dataset bruto e garantir reprodutibilidade das análises.

**2. Padronização da coluna `Age`**

```python
df_tratado['Age'] = df_tratado['Age'].astype(str).str.replace(' ', '')
df_tratado['Age'] = df_tratado['Age'].str.replace('60andolder', '60+')
```

Remoção de espaços extras e substituição do rótulo `60 and older` por `60+` para uniformizar os valores categóricos da faixa etária.

**3. Correção dos valores numéricos em `VALUE`**

```python
df_tratado['VALUE'] = pd.to_numeric(
    df_tratado['VALUE'].astype(str).str.replace(',', '.'), errors='coerce'
)
```

A coluna `VALUE` continha vírgulas como separador decimal (ex: `1,5`). Foi necessário converter para ponto antes de transformar em tipo numérico.

**4. Separação em dois datasets**

O dataset foi dividido em dois conforme a natureza dos registros:

```python
# Dados por país (para análise própria)
df_paises = df_tratado[
    (~df_tratado['Indicator'].str.contains('Regional Estimate', na=False)) &
    (~df_tratado['Iso3_code'].str.startswith(('M49', 'BIG5', 'WORLD'), na=False))
].copy()

# Estimativas regionais da ONU (para validação)
df_onu = df_tratado[
    (df_tratado['Indicator'].str.contains('Regional Estimate', na=False)) |
    (df_tratado['Iso3_code'].str.startswith(('M49', 'BIG5', 'WORLD'), na=False))
].copy()
```

| Dataset | Conteúdo | Uso |
|---|---|---|
| `df_paises` | Registros de países individuais | Análises próprias |
| `df_onu` | Estimativas regionais da ONU | Validação e comparação |

### Visão geral dos dados após tratamento

<!-- 📸 PRINT: Saída do df_paises.shape e df_onu.shape -->
```
# Exemplo de saída esperada:
# df_paises.shape → (XXXX, 13)
# df_onu.shape    → (XXXX, 13)
```

> 🖼️ <img width="300" height="282" alt="image" src="https://github.com/user-attachments/assets/3038baa6-d858-432b-acd1-31dd33a548cb" />

<!-- 📸 PRINT: Saída do df_paises.describe() -->
> 🖼️ **[Inserir print: df_paises.describe()]**

<!-- 📸 PRINT: Contagem de valores nulos e duplicados -->
> 🖼️ **[Inserir print: valores nulos e linhas duplicadas]**

---

## Análise Exploratória

### Pergunta 1 — Top 10 Países com Maiores Taxas de Homicídio (2018–2022)

**Objetivo:** Identificar os países com os índices mais altos de homicídio nos últimos 5 anos disponíveis.

#### Decisões metodológicas

**Por que taxa e não contagem absoluta?**
Usar o número bruto de vítimas (`Counts`) introduziria um viés demográfico severo: países com maior população apareceriam no topo simplesmente por terem mais habitantes. A **taxa por 100.000 habitantes** nivela a comparação e reflete o risco real da população.

**Por que média dos 5 anos?**
Um único ano anormal (evento extremo, guerra, crise) poderia distorcer o ranking. A média do período representa melhor o padrão estrutural de violência do país.

#### Filtros aplicados

```python
anos_alvo = [2018, 2019, 2020, 2021, 2022]

df_taxa = df_paises[
    (df_paises['Year'].isin(anos_alvo)) &
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Rate per 100,000 population') &
    (df_paises['Sex'] == 'Total') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]
```

> Os filtros `Sex = Total`, `Age = Total`, `Dimension = Total` e `Category = Total` são essenciais para evitar **dupla contagem** ao trabalhar com o dado agregado.

#### Resultado

<!-- 📸 PRINT: Tabela top_10_paises com países e taxa média -->
> 🖼️ **[Inserir print: tabela Top 10 países — Taxa Média por 100 mil hab.]**

---

### Pergunta 2 — Homicídios de Mulheres em 2022

**Objetivo:** Identificar os países com maiores índices de homicídio feminino em 2022 e entender se o problema é de criminalidade geral ou de vitimização desproporcional de mulheres.

Esta pergunta foi dividida em **duas análises complementares**.

#### Análise 2a — Taxa de homicídio feminino

```python
df_mulheres_2022 = df_paises[
    (df_paises['Year'] == 2022) &
    (df_paises['Sex'] == 'Female') &
    (df_paises['Unit of measurement'] == 'Rate per 100,000 population') &
    ...
]
```

<!-- 📸 PRINT: Tabela top_10_mulheres_2022 -->
> 🖼️ **[Inserir print: Top 10 países — Taxa de Homicídios de Mulheres (2022)]**

#### Análise 2b — Proporção feminina no total de vítimas

Ir além da taxa e calcular **qual porcentagem das vítimas totais são mulheres** permite distinguir dois cenários:

- País com criminalidade geral alta → mulheres aparecem no ranking por isso
- País onde mulheres são alvos desproporcionais → problema específico de gênero

> **Atenção metodológica:** para calcular proporções, é obrigatório usar `Counts` (valores absolutos). Taxas populacionais **não podem** ser somadas ou divididas diretamente com precisão demográfica.

```python
df_proporcao['Proporção Feminina (%)'] = (
    df_proporcao['Vítimas Mulheres'] / df_proporcao['Total de Vítimas']
) * 100
```

<!-- 📸 PRINT: Tabela df_proporcao com porcentagem de vítimas femininas -->
> 🖼️ **[Inserir print: tabela Proporção Feminina (%) nos 10 países]**

---

### Pergunta 3 — Regiões com Mais Homicídios

**Objetivo:** Identificar quais grandes regiões geográficas concentram o maior volume absoluto de homicídios na série histórica.

#### Por que `Counts` nesta pergunta?

A pergunta busca saber **onde ocorrem mais homicídios fisicamente** — isso requer contagem direta de vítimas. A taxa por 100.000 hab. indicaria o risco proporcional, não o volume total.

```python
ranking_regioes = df_regioes.groupby('Region')['VALUE'].sum().reset_index()
ranking_regioes = ranking_regioes.sort_values(by='VALUE', ascending=False)
```

<!-- 📸 PRINT: Tabela ranking_regioes com total de homicídios por região -->
> 🖼️ **[Inserir print: tabela — Total de Homicídios por Região]**

---

### Pergunta 4 — Países com Menor Número de Homicídios por Sub-região

**Objetivo:** Para cada sub-região do mundo, identificar o país com menor índice de homicídios.

Esta pergunta expôs um importante **problema estatístico** que levou a duas abordagens.

#### Abordagem 1 — Soma total histórica (problemática)

```python
total_pais_subregiao = df_subregiao.groupby(['Subregion', 'Country'])['VALUE'].sum()
indices_menores = total_pais_subregiao.groupby('Subregion')['VALUE'].idxmin()
```

**Problema:** um país que forneceu dados por apenas 1 ano terá soma menor do que um microestado seguro que reportou dados por 20 anos consecutivos. O ranking fica distorcido pela cobertura histórica desigual.

<!-- 📸 PRINT: Tabela paises_menores_homicidios (soma bruta) -->
> 🖼️ **[Inserir print: tabela — Método 1 (Soma Bruta)]**

#### Abordagem 2 — Média anual (metodologicamente correta)

```python
media_anual_pais = df_subregiao.groupby(['Subregion', 'Country'])['VALUE'].mean()
indices_menores_medias = media_anual_pais.groupby('Subregion')['VALUE'].idxmin()
```

**Vantagem:** a média anual nivela a comparação entre países com históricos de duração diferentes. Países que reportaram poucos anos não levam vantagem injusta.

**Funções-chave utilizadas:**
- `.idxmin()` — retorna o índice da linha com o menor valor dentro de cada grupo (mais eficiente do que ordenar e pegar o primeiro)
- `.loc[]` — recupera as linhas completas a partir dos índices encontrados

<!-- 📸 PRINT: Tabela menores_medias_subregiao (média anual) -->
> 🖼️ **[Inserir print: tabela — Método 2 (Média Anual por Sub-região)]**

---

### Pergunta 5 — Países com Menor Mortalidade Feminina

**Objetivo:** Identificar os países mais seguros para mulheres em termos de risco de homicídio.

Esta pergunta também passou por duas abordagens para evidenciar uma armadilha estatística comum.

#### Abordagem 1 — Contagem absoluta (enviesada)

```python
total_mulheres_pais = df_menor_mulheres.groupby('Country')['VALUE'].sum()
top_10_menores_mulheres = total_mulheres_pais.sort_values(ascending=True)
```

**Problema:** microestados (Mônaco, San Marino, Liechtenstein...) sempre dominam o ranking simplesmente por terem populações muito pequenas — não porque são genuinamente mais seguros. Países que falharam em reportar dados à ONU na maioria dos anos também aparecem com somas artificialmente baixas.

<!-- 📸 PRINT: Tabela top_10_menores_mulheres (contagem absoluta) -->
> 🖼️ **[Inserir print: tabela — Método 1 (Contagem Absoluta)]**

#### Abordagem 2 — Taxa média histórica (correta)

```python
media_taxa_mulheres = df_taxa_mulheres.groupby('Country')['VALUE'].mean()
top_10_menores_taxas_mulheres = media_taxa_mulheres.sort_values(ascending=True)
```

**Vantagem:** a taxa proporcional elimina o viés demográfico (tamanho da população), e a média histórica nivela a cobertura desigual de dados entre países.

Com essa abordagem, o ranking reflete países onde o **risco real** de uma mulher ser vítima de homicídio é genuinamente baixo.

<!-- 📸 PRINT: Tabela top_10_menores_taxas_mulheres (taxa média) -->
> 🖼️ **[Inserir print: tabela — Método 2 (Taxa Média por 100 mil hab.)]**

---

## Regressão

> 🚧 **Seção em desenvolvimento** — os resultados da regressão serão adicionados nesta seção.

**Objetivo:** Construir um modelo de regressão capaz de explicar e prever a variação nas taxas de homicídio entre os países, com base em variáveis como região geográfica, sub-região e ano.

### O que é Regressão Linear?

A regressão linear busca a relação matemática entre uma variável dependente (o que queremos prever) e uma ou mais variáveis independentes (os fatores explicativos):

```
y = β₀ + β₁x₁ + β₂x₂ + ... + ε
```

| Símbolo | Significado |
|---|---|
| `y` | Variável dependente (taxa de homicídio) |
| `β₀` | Intercepto (valor base) |
| `β₁, β₂...` | Coeficientes (peso de cada variável) |
| `x₁, x₂...` | Variáveis explicativas (região, ano...) |
| `ε` | Erro / resíduo do modelo |

### Como avaliar o modelo?

| Métrica | O que mede | Interpretação |
|---|---|---|
| **R²** | Proporção da variância explicada | Quanto mais próximo de 1, melhor |
| **RMSE** | Erro médio das previsões | Quanto menor, mais preciso |
| **p-valor** | Significância estatística de cada variável | p < 0,05 indica variável relevante |

<!-- 📸 PRINT: Resultado do modelo de regressão (summary, coeficientes, R²) -->
> 🖼️ **[Inserir print: sumário do modelo de regressão]**

<!-- 📸 PRINT: Gráfico de valores reais vs valores previstos -->
> 🖼️ **[Inserir print: gráfico Valores Reais × Previstos]**

<!-- 📸 PRINT: Gráfico de resíduos -->
> 🖼️ **[Inserir print: gráfico de resíduos do modelo]**

---

## Decisões Metodológicas

Um dos pontos centrais deste trabalho foi tomar decisões metodológicas conscientes a cada análise. O quadro abaixo resume as principais escolhas e suas justificativas.

| Decisão | Escolha adotada | Por quê |
|---|---|---|
| **Counts vs Taxa** | Taxa por 100 mil hab. para comparações entre países | Elimina viés demográfico |
| **Counts para proporção** | Counts ao calcular proporção feminina | Taxas não podem ser somadas diretamente |
| **Soma vs Média** | Média anual ao comparar países com históricos diferentes | Nivelar cobertura histórica desigual |
| **df_paises vs df_onu** | `df_paises` para análises próprias | Evitar misturar dados de países com estimativas regionais |
| **Cópia dos dados** | Sempre trabalhar em cópia com `.copy()` | Preservar dataset original e garantir reprodutibilidade |
| **Período 2018–2022** | Últimos 5 anos com cobertura global razoável | Anos mais recentes têm dados incompletos |
| **Filtros Total** | Age, Sex, Dimension, Category sempre fixados em `Total` | Evitar dupla contagem de subcategorias |
| **idxmin() vs sort** | `.idxmin()` para encontrar mínimos por grupo | Mais eficiente e direto do que ordenar e selecionar |

---

## Autores

Desenvolvido como trabalho acadêmico.

| Nome | GitHub |
|---|---|
| _(seu nome)_ | [@seu-usuario](https://github.com/seu-usuario) |
| _(nome colega)_ | [@colega](https://github.com/colega) |

---

<div align="center">

**UNODC Intentional Homicide Dataset · Python · pandas · numpy**

</div>
