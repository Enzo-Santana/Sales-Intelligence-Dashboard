# <span style="color:#4B0082;">Análise e Desenvolvimento de Relatório Power BI</span>

---

## <span style="color:#6A5ACD;">Resumo / Destaques Técnicos</span>
<div style="background-color:#F5F5F5; padding:10px; border-radius:5px;">
<strong>Projeto:</strong> Relatório Dinâmico de Vendas em Power BI<br>
<strong>Foco:</strong> Modelagem de Dados, DAX Avançado e Design de Dashboards<br>
<strong>Ferramentas:</strong> Power BI Desktop, DAX, Excel<br>
<strong>Principais Competências:</strong>
<ul>
<li>Estruturação de modelo estrela (Star Schema)</li>
<li>Desenvolvimento de medidas DAX personalizadas</li>
<li>Aplicação de conceitos de Time Intelligence</li>
<li>Design analítico com foco em UX e acessibilidade</li>
<li>Criação de métricas de Curva ABC (Pareto) e KPIs estratégicos</li>
</ul>
</div>

---

## <span style="color:#6A5ACD;">Visão Geral do Projeto</span>
<div style="background-color:#F0F8FF; padding:10px; border-radius:5px;">
Este projeto foi desenvolvido como parte de um teste técnico de Business Intelligence (BI), com foco na criação de um <strong>relatório dinâmico no Power BI</strong>. O objetivo foi transformar dados brutos em <strong>insights acionáveis</strong>, aplicando modelagem eficiente, expressões DAX avançadas e design de dashboards voltado à experiência do usuário.

### Páginas do Relatório
<table style="width:100%; border-collapse:collapse;">
<tr style="background-color:#E6E6FA;">
<th style="border:1px solid #DCDCDC; padding:5px;">Página</th>
<th style="border:1px solid #DCDCDC; padding:5px;">Função Analítica</th>
</tr>
<tr>
<td style="border:1px solid #DCDCDC; padding:5px;">Dashboard / Visão Geral</td>
<td style="border:1px solid #DCDCDC; padding:5px;">KPIs estratégicos e indicadores de vendas e performance</td>
</tr>
<tr>
<td style="border:1px solid #DCDCDC; padding:5px;">Análise Detalhada</td>
<td style="border:1px solid #DCDCDC; padding:5px;">Curva ABC (Pareto) e análise de tendências históricas</td>
</tr>
</table>
</div>

---

## <span style="color:#6A5ACD;">Modelagem de Dados e Arquitetura</span>
<div style="background-color:#FFF5EE; padding:10px; border-radius:5px;">
A estabilidade e performance do relatório dependem de uma <strong>modelagem bem estruturada</strong>. Foi adotado o modelo estrela (Star Schema), prática recomendada em projetos analíticos.

### Estrutura do Modelo

<table style="width:100%; border-collapse:collapse;">
<tr style="background-color:#FFE4E1;">
<th style="border:1px solid #DCDCDC; padding:5px;">Tipo</th>
<th style="border:1px solid #DCDCDC; padding:5px;">Nome</th>
<th style="border:1px solid #DCDCDC; padding:5px;">Descrição</th>
</tr>
<tr>
<td style="border:1px solid #DCDCDC; padding:5px;">Fato</td>
<td style="border:1px solid #DCDCDC; padding:5px;">fVendas</td>
<td style="border:1px solid #DCDCDC; padding:5px;">Contém todas as transações</td>
</tr>
<tr>
<td style="border:1px solid #DCDCDC; padding:5px;">Dimensão</td>
<td style="border:1px solid #DCDCDC; padding:5px;">dCalendario, dProdutos, dGeografia</td>
<td style="border:1px solid #DCDCDC; padding:5px;">Atributos descritivos para análise</td>
</tr>
</table>

### Tabela de Calendário (dCalendario)
<ul>
<li>Fundamental para <strong>Time Intelligence</strong></li>
<li>Relacionamento 1:* com a tabela de fatos</li>
<li>Permite comparações temporais precisas (anuais e acumuladas)</li>
</ul>
</div>

---

## <span style="color:#6A5ACD;">Análises e Implementações DAX</span>
<div style="background-color:#F5FFFA; padding:10px; border-radius:5px;">

### 1. Vendas Brutas LY Exato
- Comparar vendas do ano atual com o anterior, até o mesmo dia/mês da última transação.
- Funções nativas não permitem controle granular, então usamos intervalo manual com `DATESBETWEEN`.

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
