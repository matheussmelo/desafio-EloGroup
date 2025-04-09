# Desafio Técnico - EloGroup

## Visão Geral

Este repositório documenta o pipeline completo de análise desenvolvido para o desafio técnico proposto pela EloGroup, com foco na **identificação de regiões com alto potencial para expansão de laboratórios de medicina diagnóstica** nos Estados Unidos, com base em dados demográficos, econômicos e operacionais.

---

## Contexto

A medicina diagnóstica exerce um papel central na jornada de cuidado em saúde, representando um mercado de aproximadamente 106 bilhões de dólares nos EUA, com mais de 40 mil laboratórios e mais de 680 mil profissionais empregados (fonte: ACLA).

O desafio consiste em oferecer insumos analíticos para apoiar o plano de expansão de uma rede norte-americana de laboratórios diagnósticos, partindo da premissa de que, embora seja difícil induzir demanda nesse setor, é estratégico fidelizar pacientes e estar presente em locais com alto potencial de uso recorrente dos serviços.

---

## Estrutura de Dados

Os dados utilizados estão localizados na pasta `data/` (não incluída no repositório devido ao volume e confidencialidade). Abaixo, a descrição dos arquivos:

- `transactional_data.csv`: registros transacionais dos exames realizados.
- `exams_data.csv`: informações detalhadas sobre os exames.
- `df_geocode.csv`: localização dos laboratórios (endereços, coordenadas e ZCTAs).
- `EconomicData_ZCTAs.csv`: dados econômicos por ZCTA.
- `DemographicData_ZCTAs.csv`: dados demográficos por ZCTA.

---

## Ambiente de Execução

Para executar os notebooks:

1. Clonar o repositório:
   ```
   git clone <url-do-repositorio>
   ```

2. Ativar o ambiente virtual:
   ```
   .venv/Scripts/activate
   ```

3. Instalar as dependências:
   ```
   pip install -r requirements.txt
   ```

---

## Notebooks

### 1. Análise Inicial (`1. eda-inicial-pre.ipynb`)

Objetivo: explorar a estrutura dos datasets, tratar inconsistências, lidar com valores ausentes e estruturar os dados para análise posterior. Também foram levantadas hipóteses para orientar as próximas etapas da investigação.

### 2. Análise Final (`2. principal-analysis.ipynb`)

Foco: investigar padrões das regiões com laboratórios instalados, avaliando fatores como população, renda e faixa etária por ZCTA. A análise resultou na recomendação de áreas com maior potencial de expansão.

---

## Estratégia de Análise

Foram formuladas quatro hipóteses para guiar a análise:

- ZCTAs com maior população concentram maior demanda e receita.
- Faixas etárias mais idosas (60+) demandam mais exames, gerando mais receita.
- Renda domiciliar mais alta facilita acesso e realização de exames de maior valor.
- Maior número de laboratórios por ZCTA poderia indicar regiões com maior faturamento.

Com base nisso, os dados foram analisados para avaliar correlações e validar as hipóteses.

---

## Principais Resultados

### Correlações Observadas

- Receita total e volume de exames possuem forte correlação.
- Ambas variáveis estão altamente correlacionadas com a população da ZCTA.

### Perfil Econômico

- Faixas de renda entre \$35.000 e \$149.999 foram as mais associadas à alta receita e volume de exames.
- As ZCTAs com maior receita apresentaram maior concentração nessas faixas de renda.

### Perfil Demográfico

- Faixas etárias entre 25 e 54 anos foram predominantes entre as ZCTAs com melhor desempenho.
- A população idosa (60+) não se destacou entre as ZCTAs mais lucrativas, contrariando uma das hipóteses iniciais.

### Distribuição de Laboratórios

- ZCTAs com três laboratórios apresentaram maior mediana de receita, mas com amostra estatística reduzida (apenas duas ZCTAs).
- Nas 10 ZCTAs com maior receita, todas tinham apenas um laboratório, sugerindo que múltiplas unidades não são, necessariamente, um fator de alto desempenho.

---

## Metodologia de Ranqueamento

Para recomendar os melhores locais de expansão, utilizou-se o `QuantileTransformer` do Scikit-learn para transformar três variáveis em percentis (0 a 1):

- População total (`TotalPopulation`)
- Percentual da população entre 25 e 54 anos (`%_Melhores_faixas_idade`)
- Percentual da população nas faixas de renda entre \$35.000 e \$149.999 (`%_Melhores_faixas_renda`)

A média desses três percentis gerou um **score composto por ZCTA**, utilizado para definir o ranqueamento final.

## Recomendação Final

Com base no score médio dos percentis, as três ZCTAs mais indicadas para a expansão dos laboratórios são:

- **28273**
- **75067**
- **37128**

Essas regiões combinam alta população, bom perfil etário e presença significativa de faixas de renda favoráveis ao consumo de serviços diagnósticos.

---

Para qualquer questão, pode enviar um e-mail para: matheusmelo1702@gmail.com.