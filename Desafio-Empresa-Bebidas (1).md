# Briefing do Cliente: Apuração de Campanha de Vendas

## Objetivo

A área comercial da **Bebidas Premium** precisa apurar o resultado de uma campanha de vendas a partir das bases de Sell-Out, metas e dicionário de dados disponíveis no pacote do projeto.

O projeto deve contemplar o processo completo de tratamento, consolidação, cálculo da campanha, persistência em banco de dados e construção de dashboard analítico em Power BI.

O objetivo é transformar uma base comercial bruta em uma solução analítica confiável, documentada e pronta para consumo pela área de negócios.

## Arquivos de entrada

O pacote do projeto contém os seguintes arquivos:

* `SELL_OUT.csv`
* `META_VENDEDOR.csv`
* `DICIONARIO_DADOS.xlsx`

## Contexto de negócio

A empresa comercializa diversas linhas de bebidas da marca **Bebidas Premium**.

As submarcas existentes são:

| Código | Submarca        |
| ------ | --------------- |
| A      | Energéticos     |
| B      | Refrigerantes   |
| C      | Água Mineral    |
| D      | Isotônicos      |
| E      | Chás            |
| F      | Sucos           |
| G      | Água de Coco    |
| H      | Tônicos         |
| I      | Kombuchas       |
| J      | Cerveja Premium |

As submarcas participantes da campanha são:

* Energéticos (A)
* Isotônicos (D)
* Cerveja Premium (J)

## Estrutura esperada das bases

### Arquivo `SELL_OUT.csv`

Campos esperados:

* `DATA`
* `DISTRIBUIDOR`
* `MARCA`
* `SUBMARCA`
* `SKU`
* `TIPO_VENDA`
* `PDV_LOJA`
* `VENDEDOR`
* `SUPERVISOR`
* `FATURAMENTO`

Observações:

* A base representa apenas vendas do tipo `Sell Out`.
* Para análises de cobertura comercial, considerar como **PDV atendido** todo PDV que possuir venda registrada com `FATURAMENTO` maior que zero no contexto analisado.

### Arquivo `META_VENDEDOR.csv`

Campos esperados:

* `MES_REFERENCIA`
* `VENDEDOR`
* `SUBMARCA`
* `META_FATURAMENTO`

As metas devem estar disponíveis apenas para as submarcas participantes da campanha:

* Energéticos (A)
* Isotônicos (D)
* Cerveja Premium (J)

### Arquivo `DICIONARIO_DADOS.xlsx`

Arquivo de apoio contendo:

* Nome da coluna
* Tipo de dado
* Descrição
* Exemplo

## Atividades esperadas

### 1. Tratamento dos dados

Criar um processo em Python para:

* Importar os arquivos recebidos.
* Validar tipos de dados.
* Tratar registros inconsistentes.
* Tratar valores nulos.
* Padronizar campos textuais.
* Padronizar datas e campos numéricos.
* Validar relacionamentos entre vendedor, supervisor, submarca e SKU.
* Gerar logs básicos do processamento.

O processo deve estar preparado para lidar com pequenas inconsistências na base, como:

* Campos nulos.
* Espaços extras em textos.
* Datas em formatos diferentes.
* PDVs duplicados com grafias ligeiramente diferentes.

### 2. Consolidação das vendas

Criar uma base consolidada que permita analisar o realizado por:

* Mês de referência.
* Distribuidor.
* Vendedor.
* Supervisor.
* Submarca.
* SKU.
* PDV.

A consolidação deve considerar o faturamento realizado a partir da base `SELL_OUT.csv`.

### 3. Cálculo das metas

Utilizar a tabela `META_VENDEDOR.csv`.

As metas devem ser relacionadas ao realizado através de:

* Mês de referência.
* Vendedor.
* Submarca.

Para cada combinação, calcular:

* Faturamento realizado.
* Meta de faturamento.
* Atingimento percentual.
* Indicador de meta atingida.

### 4. Regras da campanha

A campanha considera apenas as submarcas:

* Energéticos (A)
* Isotônicos (D)
* Cerveja Premium (J)

#### Pontuação do vendedor

Quando o vendedor atingir ou superar a meta da submarca no mês:

| Submarca        | Pontos do vendedor |
| --------------- | ------------------ |
| Energéticos     | 200                |
| Isotônicos      | 100                |
| Cerveja Premium | 150                |

#### Pontuação do supervisor

Sempre que um vendedor subordinado atingir sua meta, o supervisor desse vendedor também pontua:

| Submarca        | Pontos do supervisor |
| --------------- | -------------------- |
| Energéticos     | 40                   |
| Isotônicos      | 50                   |
| Cerveja Premium | 30                   |

### 5. Resultado da campanha

Criar uma tabela final de resultado contendo, no mínimo:

* `MES_REFERENCIA`
* `VENDEDOR`
* `SUPERVISOR`
* `SUBMARCA`
* `FATURAMENTO_REALIZADO`
* `META_FATURAMENTO`
* `ATINGIMENTO_PERCENTUAL`
* `META_ATINGIDA`
* `PONTOS_VENDEDOR`
* `PONTOS_SUPERVISOR`

Também devem ser geradas visões consolidadas para ranking:

* Ranking mensal de vendedores.
* Ranking acumulado de vendedores.
* Ranking mensal de supervisores.
* Ranking acumulado de supervisores.

### 6. Persistência em banco de dados

Criar uma estrutura relacional contendo, no mínimo:

* Fato de vendas.
* Metas.
* Resultado da campanha.
* Dimensão de vendedores.
* Dimensão de supervisores.
* Dimensão de produtos/submarcas.

Implementar carga automatizada utilizando Python.

O banco pode ser:

* PostgreSQL
* SQL Server
* MySQL

A entrega deve incluir os scripts SQL de criação das tabelas e a explicação da estratégia de carga.

### 7. Dashboard Power BI

Desenvolver um dashboard contendo as visões abaixo.

#### Visão executiva

* Faturamento total.
* Quantidade de vendedores ativos.
* Quantidade de supervisores ativos.
* Quantidade de PDVs atendidos.
* Quantidade de distribuidores atendidos.

#### Performance comercial

* Meta x realizado.
* Atingimento percentual.
* Evolução mensal do faturamento.
* Performance por distribuidor.
* Performance por vendedor.
* Performance por supervisor.
* Performance por submarca.

#### Campanha

* Pontuação por vendedor.
* Pontuação por supervisor.
* Ranking de vendedores.
* Ranking de supervisores.
* Metas atingidas por mês.
* Metas atingidas por submarca.

#### Cobertura de PDVs

Para esta análise, utilizar o conceito de **PDV atendido**: um PDV com venda registrada e `FATURAMENTO` maior que zero no contexto analisado.

Criar análises de:

* PDVs atendidos por vendedor.
* PDVs atendidos por supervisor.
* PDVs atendidos por distribuidor.
* Evolução mensal de PDVs atendidos.

## Entregáveis

A entrega deve conter:

* Código Python do processamento.
* Modelo do banco de dados.
* Scripts SQL de criação das tabelas.
* Scripts ou rotina de carga no banco.
* Arquivo Power BI.
* Documento explicando a solução.

## Requisitos técnicos

O projeto deve:

* Utilizar Python para processamento dos dados.
* Utilizar `pandas` para tratamento e consolidação.
* Registrar logs básicos de execução.
* Separar o código em funções ou módulos organizados.
* Permitir reprocessamento da base.
* Evitar cálculos manuais fora do fluxo automatizado.
* Documentar premissas adotadas.

## Critérios de aceite

A solução será considerada adequada quando contemplar:

* Organização do projeto.
* Qualidade do código.
* Clareza do processo de ETL.
* Tratamento adequado das inconsistências.
* Modelagem de dados.
* Aplicação correta das regras de negócio.
* Dashboard - Não será avaliado Visual.
* Capacidade de documentação.

## Observações importantes

* O escopo do projeto é tratar, consolidar e apurar a campanha a partir dos arquivos de entrada.
* Indicadores relacionados a PDVs devem usar o conceito de PDV atendido, derivado das vendas realizadas.
* A campanha pontua apenas as submarcas Energéticos, Isotônicos e Cerveja Premium.
* Podem ser propostas melhorias na modelagem, desde que as regras de negócio obrigatórias sejam mantidas.
