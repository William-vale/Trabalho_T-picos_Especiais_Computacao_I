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
<br/>
🔗 **Acessar Slide de Apresentação:** [Acessar Slide](https://docs.google.com/presentation/d/1egZrnOOHDVeNVihhj5zVJnhyT5VM7VFH/edit?slide=id.p1#slide=id.p1)

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
