---
título: aaa "lição do tutorial do Azure Analysis Services 5: criar colunas calculadas | Descrição de Microsoft Docs": descreve como toocreate calculados colunas no projeto do tutorial hello Azure Analysis Services. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 01/06/2017 Author: owend
---
# <a name="lesson-5-create-calculated-columns"></a>Lição 5: criar colunas calculadas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você criará novos dados em seu modelo adicionando colunas calculadas. Você pode criar colunas calculadas (como colunas personalizadas) ao usar obter dados, usando Olá Editor de consultas ou posterior no como designer do modelo de saudação fazer aqui. mais, consulte toolearn [colunas calculadas](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Você criará cinco novas colunas calculadas em três tabelas diferentes. etapas de saudação são ligeiramente diferentes para cada tarefa mostra que há várias maneiras toocreate colunas, renomeá-las e colocá-los em vários locais em uma tabela.  

Nesta lição, você também usará primeiro as DAX (Expressões de Análise de Dados). DAX é uma linguagem especial para criar expressões de fórmula altamente personalizáveis para modelos tabulares. Neste tutorial, você pode usar colunas toocreate calculada, medidas e filtros de função DAX. mais, consulte toolearn [DAX em modelos de tabela](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Estimado tempo toocomplete nesta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 4: criar relações](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Criar colunas calculadas  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Criar uma coluna calculada MonthCalendar na tabela de DimDate Olá  
  
1.  Clique em Olá **modelo** menu > **exibição do modelo de** > **exibição dados**.  
  
    Colunas calculadas só podem ser criadas usando o designer de modelo de saudação na exibição de dados.  
  
2.  No designer de modelo hello, clique em Olá **DimDate** tabela (guia).  
  
3.  Saudação de atalho **CalendarQuarter** cabeçalho de coluna e clique **Inserir coluna**.  
  
    Uma nova coluna chamada **calculado coluna 1** é inserido toohello esquerda da saudação **trimestre do calendário** coluna.  
  
4.  Na barra de fórmulas Olá acima tabela hello, digite hello seguinte fórmula DAX: preenchimento automático ajuda você digitar Olá nomes totalmente qualificados de colunas e tabelas e listas Olá funções que estão disponíveis.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Os valores são preenchidos em todas as linhas de saudação na coluna calculada hello. Se você rolar para baixo na tabela de saudação, você verá linhas podem ter valores diferentes para essa coluna, com base nos dados de saudação em cada linha.    
  
5.  Renomear esta coluna também**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
coluna calculada de MonthCalendar Olá fornece um nome classificável para o mês.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Criar uma coluna calculada DayOfWeek tabela DimDate de saudação  
  
1.  Com hello **DimDate** tabela ainda ativa, clique em Olá **coluna** menu e clique **adicionar coluna**.  
  
2.  Na barra de fórmulas hello, digite Olá seguinte fórmula:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Quando terminar de criar a fórmula de saudação, pressione ENTER. Olá nova coluna é adicionada toohello extrema direita da tabela de saudação.  
  
3.  Renomear a coluna de saudação muito**DayOfWeek**.  
  
4.  Clique no cabeçalho de coluna hello e, em seguida, arraste a coluna de saudação entre hello **EnglishDayNameOfWeek** coluna e hello **DayNumberOfMonth** coluna.  
  
    > [!TIP]  
    > A movimentação das colunas na tabela torna mais fácil toonavigate.  
  
coluna calculada do Hello DayOfWeek fornece um nome classificável para o dia de saudação da semana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Criar uma coluna calculada ProductSubcategoryName na tabela DimProduct de saudação  
  
  
1.  Em Olá **DimProduct** de tabela, role toohello à direita da tabela de saudação. Aviso hello mais à direita coluna é nomeada **adicionar coluna** (em itálico), clique no cabeçalho da coluna de saudação.  
  
2.  Na barra de fórmulas hello, digite Olá seguinte fórmula:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Renomear a coluna de saudação muito**ProductSubcategoryName**.  
  
coluna calculada do Hello ProductSubcategoryName está toocreate usado uma hierarquia na tabela DimProduct hello, o que inclui dados de saudação EnglishProductSubcategoryName coluna na tabela de DimProductSubcategory de saudação. Hierarquias não podem abranger mais de uma tabela. Você criará hierarquias posteriormente, na Lição 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Criar uma coluna calculada ProductCategoryName na tabela DimProduct de saudação  
  
1.  Com hello **DimProduct** tabela ainda ativa, clique em Olá **coluna** menu e clique **adicionar coluna**.  
  
2.  Na barra de fórmulas hello, digite Olá seguinte fórmula:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Renomear a coluna de saudação muito**ProductCategoryName**.  
  
coluna calculada do Hello ProductCategoryName é usado toocreate uma hierarquia na tabela DimProduct hello, o que inclui dados de saudação EnglishProductCategoryName coluna na tabela de DimProductCategory de saudação. Hierarquias não podem abranger mais de uma tabela.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Criar uma coluna calculada Margin na tabela de FactInternetSales Olá  
  
1.  No designer de modelo hello, selecione Olá **FactInternetSales** tabela.  
  
2.  Criar uma nova coluna calculada entre hello **SalesAmount** coluna e hello **TaxAmt** coluna.  
  
3.  Na barra de fórmulas hello, digite Olá seguinte fórmula:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Renomear a coluna de saudação muito**margem**.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    coluna calculada do Hello Margin é usado tooanalyze as margens de lucro para cada venda.  
  
## <a name="whats-next"></a>O que vem a seguir?
[Lição 6: criar medidas](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
