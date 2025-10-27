# Análise e Desenvolvimento de Relatório Power BI

## Resumo / Destaques Técnicos
- **Projeto:** Relatório Dinâmico de Vendas em Power BI  
- **Foco:** Modelagem de Dados, DAX Avançado e Design de Dashboards  
- **Ferramentas:** Power BI Desktop, DAX, Excel  
- **Principais Competências:**
  - Estruturação de modelo estrela (Star Schema)
  - Desenvolvimento de medidas DAX personalizadas
  - Aplicação de conceitos de Time Intelligence
  - Design analítico com foco em UX e acessibilidade
  - Criação de métricas de Curva ABC (Pareto) e KPIs estratégicos

---

## Visão Geral do Projeto
Este projeto foi desenvolvido como parte de um teste técnico de Business Intelligence (BI), com foco na criação de um relatório dinâmico no Power BI. O objetivo principal foi transformar dados brutos em **insights acionáveis**, aplicando modelagem eficiente, expressões DAX avançadas e design de dashboards voltado à experiência do usuário.

O relatório final possui duas páginas principais, cada uma com função analítica distinta:

1. **Dashboard / Visão Geral:** KPIs estratégicos e principais indicadores de vendas e performance.  
2. **Análise Detalhada:** Curva ABC (Pareto) e análise de tendências históricas.

---

## Modelagem de Dados e Arquitetura
A estabilidade e performance do relatório dependem de uma **modelagem bem estruturada**. Neste projeto, foi adotado o modelo estrela (Star Schema), prática recomendada em projetos analíticos.

### Estrutura do Modelo
- **Tabela de Fatos:** `fVendas` – contém todas as transações.  
- **Tabelas de Dimensão:** `dCalendario`, `dProdutos`, `dGeografia` – fornecem atributos descritivos.  

Essa arquitetura garante consultas otimizadas e processamento DAX eficiente, mantendo integridade referencial e contexto correto entre medidas.

### Tabela de Calendário (`dCalendario`)
- Fundamental para cálculos de **Time Intelligence**.  
- Criada de forma independente e relacionada à tabela de fatos (1:*), possibilitando comparações temporais precisas, como análises anuais e acumuladas.

---

## Análises e Implementações DAX

### Medida: Vendas Brutas LY Exato
- **Objetivo:** Comparar vendas do ano atual com o ano anterior, limitando o cálculo até o mesmo dia e mês da última transação do ano atual.  
- **Desafio:** Funções nativas (`SAMEPERIODLASTYEAR`, `DATEADD`) não permitem controle granular do período de corte.  
- **Solução:** Construção manual do intervalo de datas e aplicação do filtro com `DATESBETWEEN`.  

```DAX
VAR vFinalDates = DATESBETWEEN('dCalendario'[Data], vStartOfYearLY, vFinalEndDate)
VAR vResult = CALCULATE([Vendas brutas], KEEPFILTERS(vFinalDates))
RETURN IF(NOT ISBLANK([Vendas brutas]), vResult)
```

Essa abordagem garante comparações realistas entre anos, mesmo com bases de dados de diferentes períodos.

2. Medida: % Vendas Acumulada - ABC

Objetivo: calcular a contribuição percentual acumulada das categorias, base para a Curva ABC (Pareto).

Ferramentas utilizadas:
CALCULATE, SUMMARIZE, FILTER, ALLSELECTED, RANKX.

Descrição:
A medida acumula o percentual de vendas de cada categoria após ordenação decrescente.
O uso de ALLSELECTED permite que o cálculo respeite filtros dinâmicos aplicados pelo usuário, como segmentações e seleções em visuais.

Design e Experiência do Usuário (UX)

O design do relatório foi construído com foco na clareza, acessibilidade e consistência visual, utilizando princípios de data storytelling e design funcional.

Paleta de Cores

Foi adotado um esquema institucional com tons de roxo/lilás e azul marinho, garantindo:

Contraste adequado e legibilidade (conforme padrões WCAG);

Diferenciação visual entre séries de dados (ex.: ano atual e ano anterior).

Gráfico de Tendência

Comparação entre Vendas LY e Vendas Atuais por meio de um gráfico de linha otimizado:

Rótulos de dados posicionados manualmente para evitar sobreposição;

Identificação clara de cada série temporal.

Visual da Curva ABC

Utilização de gráfico combinado (colunas e linha) para representar a regra 80/20:

Eixo primário: valores absolutos de vendas;

Eixo secundário: percentual acumulado;

Layout intuitivo que evidencia a contribuição das categorias mais relevantes.

Formatação de Unidades

Para consistência visual, foi aplicada uma formatação personalizada nas medidas:

R$ #,##0,,.0 M


Essa escolha substitui o padrão “Mi” por “M”, tornando a apresentação mais direta e legível.

Conclusão

Este projeto demonstra a capacidade de construir soluções completas em Power BI, desde a modelagem até a entrega visual, equilibrando técnica, design e clareza analítica.
A combinação de DAX avançado, modelagem estruturada e design orientado a insights garante um resultado robusto e profissional, adequado a contextos corporativos e de tomada de decisão.

Como Visualizar o Projeto

Você pode abrir o arquivo .pbix deste repositório diretamente no Power BI Desktop (versão mais recente).
O relatório é totalmente funcional e não depende de conexão externa com banco de dados.

Autor

Enzo Santana
Estudante de Ciência da Computação • UNASP-SP
Foco em Business Intelligence, Análise de Dados e Modelagem DAX

LinkedIn
 • [GitHub](https://github.com/Enzo-Santana)
 • [E-mail](enzogcsantana21@gmail.com)
 • [LinkedIn](https://www.linkedin.com/in/enzo-g-c-santana/)
