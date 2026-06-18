
# Dashboard Comercial e de Campanha de Vendas - Bebidas Premium
![Dashboard](img/home.png)


Este repositório contém a documentação e a arquitetura da solução analítica completa desenvolvida para a área comercial da **Bebidas Premium**. O projeto engloba desde a engenharia de dados (ingestão, tratamento de inconsistências e cálculo de regras complexas de negócios via Power query), modelagem relacional (*Star Schema*)  até a entrega de um dashboard analítico altamente interativo e de alto impacto visual no **Power BI**.

---

## 📌 Visão Geral das Telas do Dashboard

O layout foi desenvolvido focando na experiência do usuário (UI/UX) através de uma identidade visual unificada em tons de roxo, lavanda e cinza corporativo, reduzindo a fadiga visual do usuário e organizando as visões de forma modular.

O projeto é segmentado em **4 abas analíticas principais**, controladas por um menu superior nativo e filtros globais dinâmicos (`PERÍODO`, `SUPERVISOR`, `VENDEDOR` e botão `Limpar tudo`).

### 1. 👔 Visão Executiva
Focada em apresentar os grandes números e a saúde geral da operação comercial da Bebidas Premium de forma macro.
* **KPIs de Destaque (Cards):** Faturamento Total Acumulado.
  * Quantidade de Vendedores Ativos e Supervisores Ativos na base de dados.
  * Capilaridade da operação: Total de PDVs atendidos e Distribuintes mapeados.
* **Gráficos Estratégicos:** Visão macro da evolução financeira e distribuição das vendas de forma consolidada por canais ou mercados de atuação.

### 2. 📈 Performance Comercial
Abraça o pilar de controle e comparação de resultados em relação ao planejamento estratégico da companhia.
* **Metricas Comparativas (Meta x Realizado):** Apresentação do volume financeiro vendido versus a cota estipulada para o time comercial.
* **Atingimento Percentual ($\%$) e Evolução:** Gráficos de linhas e colunas que detalham o histórico de crescimento mensal e o atingimento das submarcas.
* **Análise de Performance por Canal:** Quebra da performance comercial por Distribuidor, por Vendedor, por Supervisor e por Submarca para identificar desvios e oportunidades de mercado.

### 3. 🏅 Campanha de Vendas
Tela especializada para o acompanhamento do regulamento e engajamento da força de vendas.
* **Mecânica de Rankings (Top 5):** Visão ágil dos 5 melhores colocados no ranking de pontuação (tanto para Supervisores quanto para Vendedores).
* **Painel Multi-Perspectiva:** Gráfico central expansível que altera a exibição entre o ranking de pontos totais por Vendedor ou por Supervisor através de botões de controle (*Bookmarks*).
* **Metas Atingidas por Submarca:** Gráfico focado nas categorias elegíveis para a premiação (**Isotônicos**, **Cerveja Premium** e **Energéticos**), medindo o sucesso absoluto do time.

### 4. 🎯 Cobertura de PDVs (Pontos de Venda)
Focada em mensurar a capilaridade e a eficiência da positivação de mercado.
* **Conceito de PDV Atendido:** Critério técnico estrito onde é classificado como "atendido" qualquer PDV com registro de venda e faturamento maior que zero no período selecionado.
* **Mapeamento de Cobertura:** Distribuição e histórico de positivação agregados por Vendedor, por Supervisor e por Distribuidor.
* **Evolução Mensal de Cobertura:** Análise de tendência para identificar se a base de clientes ativos está expandindo ou retraindo ao longo do ano.

---

## 📐 Engenharia de Dados e Regras de Negócio

### 1. Ingestão e Qualidade dos Dados (ETL)

* **Limpeza Textual:** Remoção de espaços duplos e caracteres especiais. Aplicação de padrão *UPPERCASE* para normalizar strings de vendedores, supervisores e marcas.
* **Validação de Tipagem:** Conversão de strings temporais em formato nativo `DATE` e valores monetários para `DECIMAL/FLOAT`.
* **Segurança e Integridade:** Detecção de PDVs duplicados com grafias divergentes e isolamento de linhas inconsistentes em arquivos de logs.

### 2. Motor de Cálculo de Pontuação da Campanha
A regra de negócios pontua estritamente o atingimento das metas no mês  nas submarcas selecionadas:

| Submarca Participante | Pontuação do Vendedor | Pontuação do Supervisor (Por Vendedor Atingido) |
| :--- | :---: | :---: |
| **Energéticos (A)** | 200 pontos | 40 pontos |
| **Isotônicos (D)** | 100 pontos | 50 pontos |
| **Cerveja Premium (J)** | 150 pontos | 30 pontos |

### 3. Modelagem de Dados Relacional (Data Warehouse)
O banco de dados relacional foi modelado seguindo a metodologia **Star Schema** (Esquema Estrela), otimizando o processamento de contextos de filtros complexos e consultas DAX:
* **Tabelas Fato:**
  * `fato_vendas`: Dados diários de faturamento por SKU e ponto de venda.
  * `fato_metas`: Planejamento de cotas de faturamento por período.
  * `fato_resultado_campanha`: Armazena a inteligência e o cálculo final consolidado de pontos.
* **Tabelas Dimensão:**
  * `dim_vendedores`, `dim_supervisores`, `dim_produtos` e `dim_calendario` (com hierarquia de tempo completa).  

## Link do PBIX publicado:
https://app.powerbi.com/view?r=eyJrIjoiODEwMDAzYWItZjQ2My00NmRmLTgzMjAtMDdmZTMxZTlmZWY5IiwidCI6IjkzNzhhYjJkLWUxNmMtNDZlMS04MzRjLWQ4NGU3MTNhMjA2ZiJ9&pageName=6ce88aaf32c00e3ed6e2




