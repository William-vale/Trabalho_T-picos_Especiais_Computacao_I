# 🔍 Análise Exploratória e Regressão — Homicídios Globais

> Projeto de análise de dados com Python utilizando a base oficial da **ONU (UNODC)** sobre homicídios intencionais no mundo.

---

## 📋 Sumário

- [Sobre o Projeto](#sobre-o-projeto)
- [Links dos Projetos](#links-dos-projetos)
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
  - [Pergunta 6 — Sub-regiões com Maior Número de Homicídios](#pergunta-6--sub-regiões-com-maior-número-de-homicídios)
  - [Pergunta 7 — País com Maior Número de Homicídios por Continente em 2020](#pergunta-7--país-com-maior-número-de-homicídios-por-continente-em-2020)
  - [Pergunta 8 — País Mais Violento para Mulheres em 2021](#pergunta-8--país-mais-violento-para-mulheres-em-2021)
  - [Pergunta 9 — País com Maior Média Anual de Vítimas de Homicídio](#pergunta-9--país-com-maior-média-anual-de-vítimas-de-homicídio)
  - [Pergunta 10 — Média Anual de Homicídios no Brasil nos Últimos 10 Anos](#pergunta-10--média-anual-de-homicídios-no-brasil-nos-últimos-10-anos)
- [Regressão](#regressão)
- [Decisões Metodológicas](#decisões-metodológicas)
- [Autores](#autores)

---

## Sobre o Projeto

Este projeto foi desenvolvido como trabalho acadêmico da disciplina de **Tópicos em Ciência de Dados**, com o objetivo de aplicar técnicas de **Análise Exploratória de Dados (EDA)** e **Regressão** sobre dados reais de criminalidade global.

A análise busca responder perguntas concretas sobre a distribuição de homicídios intencionais no mundo, identificar padrões regionais, diferenças de gênero e construir um modelo preditivo capaz de explicar a variação nas taxas de homicídio entre países.

Todo o código foi desenvolvido em **Python**, utilizando o ambiente **Google Colab**.

## Links dos Projetos

🔗 **Notebook no Google Colab Com perguntas respondidas:** [Acessar notebook](https://colab.research.google.com/drive/1uo1YFYDQhMhz49TFIhQDVmmgOhvNqqZQ?usp=sharing#scrollTo=RtpEfPn7I6NB)
<br/>
🔗 **Notebook no Google Colab com a parte de regressão:** [Acessar notebook](https://colab.research.google.com/drive/1r2uWPups1EFy5Hs6DBTDmpBqFxe1NIXL?usp=sharing#scrollTo=ZKPm6XCMqGB0)
<br/>
🔗 **Acessar Slide de Apresentação:** [Acessar Slide](https://drive.google.com/file/d/1h2XIRlcCsrsXbv217TdQRPm_ZLNG6ZqS/view?usp=drivesdk)

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
├── 📄 topicos_regr.py              # Código sobre a regressão
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

<img width="300" height="282" alt="image" src="https://github.com/user-attachments/assets/3038baa6-d858-432b-acd1-31dd33a548cb" />
<br/>
<!-- 📸 PRINT: Saída do df_paises.describe() -->
<img width="282" height="289" alt="image" src="https://github.com/user-attachments/assets/142bffa7-a62f-4467-860f-0292d78e9ea4" />
<br/>
<!-- 📸 PRINT: Contagem de valores nulos e duplicados -->
<img width="519" height="171" alt="image" src="https://github.com/user-attachments/assets/a68157c1-6ef1-4baa-b9b8-e495c94bb723" />

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

<br/>
<!-- 📸 PRINT: Tabela top_10_paises com países e taxa média -->
<img width="385" height="261" alt="image" src="https://github.com/user-attachments/assets/31e6c4f1-5ba1-489f-a0c3-8ec2415bce2a" />
<br/>

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

<br/>
<!-- 📸 PRINT: Tabela top_10_mulheres_2022 -->
<img width="577" height="302" alt="image" src="https://github.com/user-attachments/assets/84af754f-17fc-4883-b43c-ee02b09dfa85" />
<br/>

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

<br/>
<!-- 📸 PRINT: Tabela df_proporcao com porcentagem de vítimas femininas -->
<img width="652" height="308" alt="image" src="https://github.com/user-attachments/assets/5e61609e-7f38-4348-8ced-cdaa16e5abbd" />
<br/>

---

### Pergunta 3 — Regiões com Mais Homicídios

**Objetivo:** Identificar quais grandes regiões geográficas concentram o maior volume absoluto de homicídios na série histórica.

#### Por que `Counts` nesta pergunta?

A pergunta busca saber **onde ocorrem mais homicídios fisicamente** — isso requer contagem direta de vítimas. A taxa por 100.000 hab. indicaria o risco proporcional, não o volume total.

```python
ranking_regioes = df_regioes.groupby('Region')['VALUE'].sum().reset_index()
ranking_regioes = ranking_regioes.sort_values(by='VALUE', ascending=False)
```

<br/>
<!-- 📸 PRINT: Tabela ranking_regioes com total de homicídios por região -->
<img width="249" height="169" alt="image" src="https://github.com/user-attachments/assets/cb9cebd8-719e-4900-93b5-df30d8045b6a" />
<br/>

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

<br/>
<!-- 📸 PRINT: Tabela paises_menores_homicidios (soma bruta) -->
<img width="543" height="423" alt="image" src="https://github.com/user-attachments/assets/66beb70a-bd17-43f3-a9ff-713eefd490db" />
<br/>

#### Abordagem 2 — Média anual (metodologicamente correta)

```python
media_anual_pais = df_subregiao.groupby(['Subregion', 'Country'])['VALUE'].mean()
indices_menores_medias = media_anual_pais.groupby('Subregion')['VALUE'].idxmin()
```

**Vantagem:** a média anual nivela a comparação entre países com históricos de duração diferentes. Países que reportaram poucos anos não levam vantagem injusta.

**Funções-chave utilizadas:**
- `.idxmin()` — retorna o índice da linha com o menor valor dentro de cada grupo (mais eficiente do que ordenar e pegar o primeiro)
- `.loc[]` — recupera as linhas completas a partir dos índices encontrados

<br/>
<!-- 📸 PRINT: Tabela menores_medias_subregiao (média anual) -->
<img width="582" height="423" alt="image" src="https://github.com/user-attachments/assets/0e0c7e69-e01a-457c-bac5-b41872881ed1" />
<br/>

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

<br/>
<!-- 📸 PRINT: Tabela top_10_menores_mulheres (contagem absoluta) -->
<img width="368" height="287" alt="image" src="https://github.com/user-attachments/assets/d441d5a5-1820-4a0a-89d8-2146a7d7a78b" />
<br/>

#### Abordagem 2 — Taxa média histórica (correta)

```python
media_taxa_mulheres = df_taxa_mulheres.groupby('Country')['VALUE'].mean()
top_10_menores_taxas_mulheres = media_taxa_mulheres.sort_values(ascending=True)
```

**Vantagem:** a taxa proporcional elimina o viés demográfico (tamanho da população), e a média histórica nivela a cobertura desigual de dados entre países.

Com essa abordagem, o ranking reflete países onde o **risco real** de uma mulher ser vítima de homicídio é genuinamente baixo.

<br/>
<!-- 📸 PRINT: Tabela top_10_menores_taxas_mulheres (taxa média) -->
<img width="498" height="296" alt="image" src="https://github.com/user-attachments/assets/87666f1f-95c1-4305-89dc-0d7b8956342d" />
<br/>

---

### Pergunta 6 — Sub-regiões com Maior Número de Homicídios

**Objetivo:** Identificar quais sub-regiões geográficas concentram o maior volume de homicídios, utilizando tanto o número absoluto quanto a taxa proporcional para uma análise completa.

Esta pergunta usa **duas métricas complementares**, pois cada uma responde uma dimensão diferente do problema.

#### Análise 6a — Volume absoluto de homicídios (`Counts`)

```python
df_count = df_paises[
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Counts') &
    (df_paises['Sex'] == 'Total') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]

ranking_count = (
    df_count.groupby('Subregion')['VALUE']
    .sum()
    .sort_values(ascending=False)
)
```

**Por que `Counts` aqui?** O volume absoluto indica onde fisicamente ocorre o maior número de homicídios — útil para alocação de recursos e políticas públicas de segurança em escala.

> Os filtros `Sex = Total`, `Age = Total`, `Dimension = Total` e `Category = Total` garantem que cada homicídio seja contabilizado **apenas uma vez**, evitando a duplicação de subcategorias.

<br/>
<!-- 📸 PRINT: ranking_count.head(10) — Top 10 sub-regiões por volume -->
<img width="279" height="339" alt="image" src="https://github.com/user-attachments/assets/8f0be0a4-a49e-4603-9ddf-df1bf2a4efc6" />
<br/>

#### Análise 6b — Taxa média por 100 mil habitantes

```python
df_rate = df_paises[
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Rate per 100,000 population') &
    (df_paises['Sex'] == 'Total') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]

ranking_rate = (
    df_rate.groupby('Subregion')['VALUE']
    .mean()
    .sort_values(ascending=False)
)
```

**Por que também calcular a taxa?** Sub-regiões muito populosas aparecem no topo do ranking absoluto independentemente da sua violência real. A taxa proporcional permite comparações mais justas, revelando quais sub-regiões têm maior risco per capita — o que pode ser diferente do ranking por volume.

<br/>
<!-- 📸 PRINT: ranking_rate.head(10) — Top 10 sub-regiões por taxa média -->
<img width="277" height="329" alt="image" src="https://github.com/user-attachments/assets/af20aa40-8754-4344-97eb-de41620c348a" />
<br/>

---

### Pergunta 7 — País com Maior Número de Homicídios por Continente em 2020

**Objetivo:** Para cada continente, identificar qual país registrou o maior número absoluto de homicídios no ano de 2020.

#### Decisões metodológicas

**Por que `Counts` e não taxa?** A pergunta busca o país com o **maior volume** de homicídios dentro de cada continente — isso requer contagem absoluta de vítimas. Usar taxa mudaria a pergunta para "maior risco proporcional", que é uma análise diferente.

**Por que 2020?** É um ano recente com boa cobertura de dados para a maioria dos países. Permite um retrato atual da distribuição de violência por continente.

**Por que `.idxmax()` por grupo?** Após agrupar por continente e país, o `.idxmax()` retorna diretamente o índice do maior valor em cada continente — mais eficiente do que ordenar toda a tabela e filtrar o topo de cada grupo.

```python
df_2020 = df_paises[
    (df_paises['Year'] == 2020) &
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Counts') &
    (df_paises['Sex'] == 'Total') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]

homicidios = (
    df_2020.groupby(['Region', 'Country'])['VALUE']
    .sum()
    .reset_index()
)

idx = homicidios.groupby('Region')['VALUE'].idxmax()

resultado = homicidios.loc[idx].sort_values('VALUE', ascending=False)
```

**Funções-chave utilizadas:**
- `.groupby(['Region', 'Country'])` — agrupa por continente e país simultaneamente
- `.idxmax()` — retorna o índice do maior valor dentro de cada continente
- `.loc[idx]` — recupera as linhas completas (com país e continente) a partir dos índices

<br/>
<!-- 📸 PRINT: Tabela resultado — país líder em homicídios por continente em 2020 -->
<img width="249" height="142" alt="image" src="https://github.com/user-attachments/assets/c8994269-d63b-4cfe-bb99-a0b053a53cca" />
<br/>

---

### Pergunta 8 — País Mais Violento para Mulheres em 2021

**Objetivo:** Identificar o país com maior incidência de homicídios femininos em 2021, demonstrando por que a taxa proporcional é a métrica correta — e não o volume absoluto.

Esta pergunta foi deliberadamente construída com **duas abordagens** para expor um viés estatístico comum.

#### Análise 8a — Por volume absoluto (`Counts`) — enviesada

```python
df_mulheres_count = df_paises[
    (df_paises['Year'] == 2021) &
    (df_paises['Sex'] == 'Female') &
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Counts') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]

ranking_mulheres_count = (
    df_mulheres_count.groupby('Country')['VALUE']
    .mean()
    .sort_values(ascending=False)
)
```

**Problema:** países com grande população feminina — como Brasil, Índia, México — aparecem no topo simplesmente pelo tamanho da população, não pela proporção de risco. O ranking por volume **favorece e enviesa países muito populosos**.

<br/>
<!-- 📸 PRINT: ranking_mulheres_count.head(10) — por volume -->
<img width="296" height="323" alt="image" src="https://github.com/user-attachments/assets/d93612d5-7e2d-442a-a2b8-894124877047" />
<br/>

#### Análise 8b — Por taxa proporcional — correta

```python
df_mulheres_rate = df_paises[
    (df_paises['Year'] == 2021) &
    (df_paises['Sex'] == 'Female') &
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Rate per 100,000 population') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]

ranking_mulheres_rate = (
    df_mulheres_rate.groupby('Country')['VALUE']
    .mean()
    .sort_values(ascending=False)
)
```

**Vantagem:** a taxa por 100 mil habitantes elimina o efeito do tamanho da população e revela onde o **risco proporcional** de uma mulher ser assassinada é genuinamente maior — independentemente de o país ter 1 milhão ou 200 milhões de habitantes.

> O filtro `Sex == 'Female'` combinado com `Age = Total`, `Dimension = Total` e `Category = Total` garante que apenas o total de mulheres vítimas seja contabilizado, sem duplicações por subcategorias.

<br/>
<!-- 📸 PRINT: ranking_mulheres_rate.head(10) — por taxa -->
<img width="295" height="323" alt="image" src="https://github.com/user-attachments/assets/64060ced-a400-4200-983c-cc270ec28737" />
<br/>

---

### Pergunta 9 — País com Maior Média Anual de Vítimas de Homicídio

**Objetivo:** Identificar os países que apresentam, em média por ano, os maiores volumes de homicídios intencionais ao longo de toda a série histórica disponível.

#### Decisão metodológica: média em vez de soma total

```python
df_vitimas = df_paises[
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Counts') &
    (df_paises['Sex'] == 'Total') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]

ranking_media = (
    df_vitimas.groupby('Country')['VALUE']
    .mean()
    .sort_values(ascending=False)
)
```

**Por que média e não soma?** Usar a soma total histórica favorece países com **mais anos reportados** na base de dados — um país que reportou 30 anos acumularia mais homicídios do que um que reportou apenas 10, mesmo que seja menos violento. A média por ano nivela a comparação e reflete o **padrão estrutural** de violência de cada país, independentemente da duração da série histórica disponível.

**Por que `Counts` nesta análise?** O objetivo é identificar onde ocorre o maior **volume** de homicídios — não o maior risco proporcional. Países com populações muito grandes como Brasil, México e Índia tendem a aparecer no topo, o que é esperado e informativo para esta pergunta específica.

<br/>
<!-- 📸 PRINT: ranking_media.head(10) — países com maior média anual de homicídios -->
<img width="234" height="308" alt="image" src="https://github.com/user-attachments/assets/29b1426f-1af0-4288-afa6-2a5fff32e9f0" />
<br/>

---

### Pergunta 10 — Média Anual de Homicídios no Brasil nos Últimos 10 Anos

**Objetivo:** Calcular a média anual de homicídios no Brasil entre 2012 e 2021, usando tanto o número absoluto quanto a taxa por 100 mil habitantes como métricas complementares.

#### Decisões metodológicas

**Por que agrupar por ano antes de calcular a média?** O dataset tem múltiplas linhas por ano para o Brasil (por dimensão, categoria, faixa etária etc.). Se calculássemos a média diretamente sobre todas as linhas, estaríamos incluindo subcategorias e duplicando contagens. O agrupamento por ano garante primeiro o total real de cada ano, e a média final é calculada sobre esses totais anuais — resultando na **média de homicídios por ano**.

**Por que o período vai de 2012 a 2021 e não até 2023?** Embora o filtro permita anos até 2023, a base de dados contém registros para o Brasil apenas até 2021. O período efetivo analisado é de **10 anos: 2012 a 2021**.

#### Análise 10a — Média por contagem absoluta

```python
df_brasil = df_paises[
    (df_paises['Country'] == 'Brazil') &
    (df_paises['Year'].between(2012, 2021)) &
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Counts') &
    (df_paises['Sex'] == 'Total') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]

# Passo 1: total real por ano
media_por_ano = df_brasil.groupby('Year')['VALUE'].sum()

# Passo 2: média dos totais anuais
media_homicidios = media_por_ano.mean()

print(f'Média anual de homicídios no Brasil (2012-2021): {media_homicidios:.2f}')
```

<br/>
<!-- 📸 PRINT: media_por_ano — série histórica por ano + média final -->
<img width="370" height="338" alt="image" src="https://github.com/user-attachments/assets/e55c67ee-a65c-4f21-a0c6-960e99eb8a24" />
<br/>

#### Análise 10b — Taxa média por 100 mil habitantes

```python
df_brasil_taxa = df_paises[
    (df_paises['Country'] == 'Brazil') &
    (df_paises['Year'].between(2012, 2021)) &
    (df_paises['Indicator'] == 'Victims of intentional homicide') &
    (df_paises['Unit of measurement'] == 'Rate per 100,000 population') &
    (df_paises['Sex'] == 'Total') &
    (df_paises['Age'] == 'Total') &
    (df_paises['Dimension'] == 'Total') &
    (df_paises['Category'] == 'Total')
]

print(f"Taxa média no período: {df_brasil_taxa['VALUE'].mean():.2f}")
```

**Por que calcular também a taxa?** O número absoluto de homicídios é influenciado pelo crescimento da população ao longo dos anos. A taxa por 100 mil habitantes oferece uma **leitura mais estável da tendência real de violência** no período, independentemente das variações populacionais.

<br/>
<!-- 📸 PRINT: saída da taxa média por 100 mil hab. no período -->
<img width="370" height="338" alt="image" src="https://github.com/user-attachments/assets/6e340216-9aee-4787-9036-b3c5b1b2f4fd" />
<br/>

---

## Regressão

**Objetivo:** Treinar um modelo de Regressão Linear Simples para capturar a tendência histórica de homicídios no Brasil e gerar previsões para os anos 2023 a 2026.

### O que é Regressão Linear?

A regressão linear busca a relação matemática entre uma variável que queremos prever e outras variáveis explicativas:

```
y = β₀ + β₁x + ε
```

| Símbolo | Significado | Neste projeto |
|---|---|---|
| `y` | Variável dependente (o que prevemos) | Número de homicídios |
| `β₀` | Intercepto — valor base quando x = 0 | Calculado pelo modelo |
| `β₁` | Coeficiente — peso da variável preditora | Variação por ano |
| `x` | Variável preditora | Ano (Year) |
| `ε` | Erro / resíduo do modelo | Diferença real × previsto |

### Configuração da análise

| Parâmetro | Valor |
|---|---|
| **País analisado** | Brasil (`Brazil`) |
| **Período de treino** | 2013 a 2022 (10 anos) |
| **Variável preditora (X)** | `Year` — ano do registro |
| **Variável alvo (y)** | `VALUE` — número de homicídios |
| **Filtro de sexo** | `Total` (homens + mulheres) |
| **Biblioteca** | `sklearn.linear_model.LinearRegression` |
| **Métrica de avaliação** | MSE — Mean Squared Error |

<br/>
<!-- 📸 PRINT: print("Dados carregados com sucesso! Linhas e colunas:", df.shape) -->
<img width="476" height="143" alt="image" src="https://github.com/user-attachments/assets/0b771c5e-bb0f-49f4-819f-4fef2be3832c" />
<br/>

---

### Etapa 1 — Filtragem dos Dados

```python
df_filtrado = df[
    (df['Country'] == 'Brazil') &
    (df['Sex'] == 'Total') &
    (df['Year'] >= 2013) &
    (df['Year'] <= 2022)
].copy()
```

Isolamos apenas os registros do Brasil, com sexo agregado (`Total`) e dentro do período de análise. O `.copy()` garante que alterações futuras não afetem o DataFrame original.

---

### Etapa 2 — Agrupamento por Ano com `.max()`

```python
df_agrupado = df_filtrado.groupby('Year')['VALUE'].max().reset_index()
```

**Por que `.max()` e não `.sum()` ou `.mean()`?**

O dataset tem múltiplas linhas por ano para o mesmo país — cada linha representa uma combinação de dimensão, categoria e mecanismo. Somar essas linhas duplicaria os valores. O `.max()` captura o maior valor reportado para aquele ano, que corresponde ao total agregado (linha com `Dimension = Total`, `Category = Total`).

<br/>
<!-- 📸 PRINT: df_agrupado após o groupby — tabela com Year e VALUE por ano -->
<img width="445" height="264" alt="image" src="https://github.com/user-attachments/assets/ae2f487e-1736-4ed1-8666-d655bc0a3eb9" />
<br/>


---

### Etapa 3 — Tratamento de Zeros

```python
df_agrupado['VALUE'] = df_agrupado['VALUE'].replace(0, np.nan)
df_agrupado['VALUE'] = df_agrupado['VALUE'].interpolate()
```

**Por que substituir zeros?**

Um valor `0` em dados de homicídios não significa que não houve mortes — indica dado ausente, falha no reporte ou erro na coleta. Incluir zeros no treino puxaria a linha de regressão artificialmente para baixo, distorcendo as previsões.

**Por que interpolação e não remoção?**

Com apenas 10 pontos de dados (2013–2022), remover uma linha causaria perda significativa de informação e quebraria a continuidade da série temporal. A interpolação linear estima o valor faltante com base nos anos vizinhos, preservando todos os pontos.

---

### Etapa 4 — Treinamento do Modelo

```python
X = df_agrupado[['Year']]   # Variável preditora (precisa ser 2D)
y = df_agrupado['VALUE']    # Variável alvo

modelo_final = LinearRegression()
modelo_final.fit(X, y)
```

O modelo ajusta os parâmetros `β₀` (intercepto) e `β₁` (coeficiente do ano) minimizando o erro quadrático total entre os valores reais e os previstos — técnica conhecida como **Mínimos Quadrados Ordinários (OLS)**.

---

### Etapa 5 — Avaliação com MSE

```python
previsoes_treino = modelo_final.predict(X)
mse_final = mean_squared_error(y, previsoes_treino)

print(f"Erro Quadrático Médio (MSE) no Treino: {mse_final:.0f}")
```

| Métrica | O que mede | Interpretação |
|---|---|---|
| **MSE** | Média dos erros ao quadrado | Quanto menor, melhor o ajuste |
| **√MSE (RMSE)** | Erro médio na mesma unidade de y | Interpretável em nº de homicídios |

---

### Etapa 6 — Previsões para Anos Futuros

```python
anos_futuros = [2023, 2024, 2025, 2026]
dados_futuros = pd.DataFrame({'Year': anos_futuros})

previsoes_futuras = modelo_final.predict(dados_futuros)

for ano, taxa in zip(anos_futuros, previsoes_futuras):
    print(f"   Ano {ano}: {taxa:.0f}")
```

O modelo aplica a equação aprendida (`β₀ + β₁ × Ano`) sobre cada ano futuro. Como a regressão é linear, a variação entre anos consecutivos é constante — a reta continua com a mesma inclinação aprendida no treino.

<br/>
<!-- 📸 PRINT: Previsões para 2023, 2024, 2025 e 2026 -->
<img width="377" height="227" alt="image" src="https://github.com/user-attachments/assets/5a1f34dd-7ae4-41ca-ab55-3f1bd49a0d5b" />
<br/>

---

### Limitação importante

A regressão linear assume que a tendência histórica continuará. Eventos externos — mudanças de política pública, crises econômicas, conflitos — podem quebrar essa tendência. As previsões devem ser interpretadas como **extrapolação da tendência observada**, não como certeza.

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
| **idxmax() por grupo** | `.idxmax()` para encontrar máximos por continente (P7) | Retorna diretamente o índice do maior valor por grupo |
| **Duas métricas (P6 e P8)** | Volume absoluto + taxa proporcional em paralelo | Cada métrica responde uma dimensão diferente do problema |
| **Média vs soma histórica (P9)** | Média anual por país | Soma favorece países com mais anos reportados na base |
| **Agrupamento anual antes da média (P10)** | `groupby('Year').sum()` antes de `.mean()` | Garante o total real por ano antes de calcular a média |
| **País da regressão** | Brasil | Série histórica consistente + país de alto volume |
| **Agrupamento .max()** | `.max()` ao consolidar múltiplas linhas por ano | `.sum()` duplicaria valores de subcategorias |
| **Zeros → NaN → interpolate()** | Substituir zeros por NaN e interpolar | Zero não significa ausência de crime, e interpolação preserva os 10 pontos |
| **Variável preditora** | `Year` (ano) | Captura tendência temporal de forma simples e interpretável |

---

## Autores

Desenvolvido como trabalho acadêmico.

| Nome | GitHub |
|---|---|
| _(William do Vale)_ | [@William-vale](https://github.com/William-vale) |
| _(Antonio Lucas)_ | [@AntLucass](https://github.com/AntLucass) |
| _(Atila-dev)_ | [@Atila-dev](https://github.com/Atila-dev) |
| _(Augusto Derik)_ | [@AugustoDerik](https://github.com/AugustoDerik) |
| _(Geilma Melo)_ | [@GeilmaMelo](https://github.com/GeilmaMelo) |
| _(Leandro Melo)_ | [@LeandroMel0](https://github.com/LeandroMel0) |
| _(Viennel)_ | [@Viennel](https://github.com/Viennel) |

---

<div align="center">

**UNODC Intentional Homicide Dataset · Python · pandas · numpy**

</div>
