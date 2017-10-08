---
<span data-ttu-id="e48b0-101">título: aaa "lição do tutorial do Azure Analysis Services 5: criar colunas calculadas | Descrição de Microsoft Docs": descreve como toocreate calculados colunas no projeto do tutorial hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="e48b0-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="e48b0-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="e48b0-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="e48b0-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 01/06/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="e48b0-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="e48b0-104">Lição 5: criar colunas calculadas</span><span class="sxs-lookup"><span data-stu-id="e48b0-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="e48b0-105">Nesta lição, você criará novos dados em seu modelo adicionando colunas calculadas.</span><span class="sxs-lookup"><span data-stu-id="e48b0-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="e48b0-106">Você pode criar colunas calculadas (como colunas personalizadas) ao usar obter dados, usando Olá Editor de consultas ou posterior no como designer do modelo de saudação fazer aqui.</span><span class="sxs-lookup"><span data-stu-id="e48b0-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="e48b0-107">mais, consulte toolearn [colunas calculadas](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="e48b0-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="e48b0-108">Você criará cinco novas colunas calculadas em três tabelas diferentes.</span><span class="sxs-lookup"><span data-stu-id="e48b0-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="e48b0-109">etapas de saudação são ligeiramente diferentes para cada tarefa mostra que há várias maneiras toocreate colunas, renomeá-las e colocá-los em vários locais em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e48b0-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="e48b0-110">Nesta lição, você também usará primeiro as DAX (Expressões de Análise de Dados).</span><span class="sxs-lookup"><span data-stu-id="e48b0-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="e48b0-111">DAX é uma linguagem especial para criar expressões de fórmula altamente personalizáveis para modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="e48b0-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="e48b0-112">Neste tutorial, você pode usar colunas toocreate calculada, medidas e filtros de função DAX.</span><span class="sxs-lookup"><span data-stu-id="e48b0-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="e48b0-113">mais, consulte toolearn [DAX em modelos de tabela](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="e48b0-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="e48b0-114">Estimado tempo toocomplete nesta lição: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="e48b0-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="e48b0-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e48b0-115">Prerequisites</span></span>  
<span data-ttu-id="e48b0-116">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="e48b0-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="e48b0-117">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 4: criar relações](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="e48b0-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="e48b0-118">Criar colunas calculadas</span><span class="sxs-lookup"><span data-stu-id="e48b0-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="e48b0-119">Criar uma coluna calculada MonthCalendar na tabela de DimDate Olá</span><span class="sxs-lookup"><span data-stu-id="e48b0-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="e48b0-120">Clique em Olá **modelo** menu > **exibição do modelo de** > **exibição dados**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="e48b0-121">Colunas calculadas só podem ser criadas usando o designer de modelo de saudação na exibição de dados.</span><span class="sxs-lookup"><span data-stu-id="e48b0-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="e48b0-122">No designer de modelo hello, clique em Olá **DimDate** tabela (guia).</span><span class="sxs-lookup"><span data-stu-id="e48b0-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="e48b0-123">Saudação de atalho **CalendarQuarter** cabeçalho de coluna e clique **Inserir coluna**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="e48b0-124">Uma nova coluna chamada **calculado coluna 1** é inserido toohello esquerda da saudação **trimestre do calendário** coluna.</span><span class="sxs-lookup"><span data-stu-id="e48b0-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="e48b0-125">Na barra de fórmulas Olá acima tabela hello, digite hello seguinte fórmula DAX: preenchimento automático ajuda você digitar Olá nomes totalmente qualificados de colunas e tabelas e listas Olá funções que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e48b0-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="e48b0-126">Os valores são preenchidos em todas as linhas de saudação na coluna calculada hello.</span><span class="sxs-lookup"><span data-stu-id="e48b0-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="e48b0-127">Se você rolar para baixo na tabela de saudação, você verá linhas podem ter valores diferentes para essa coluna, com base nos dados de saudação em cada linha.</span><span class="sxs-lookup"><span data-stu-id="e48b0-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="e48b0-128">Renomear esta coluna também**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="e48b0-130">coluna calculada de MonthCalendar Olá fornece um nome classificável para o mês.</span><span class="sxs-lookup"><span data-stu-id="e48b0-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="e48b0-131">Criar uma coluna calculada DayOfWeek tabela DimDate de saudação</span><span class="sxs-lookup"><span data-stu-id="e48b0-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="e48b0-132">Com hello **DimDate** tabela ainda ativa, clique em Olá **coluna** menu e clique **adicionar coluna**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="e48b0-133">Na barra de fórmulas hello, digite Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="e48b0-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="e48b0-134">Quando terminar de criar a fórmula de saudação, pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="e48b0-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="e48b0-135">Olá nova coluna é adicionada toohello extrema direita da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48b0-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="e48b0-136">Renomear a coluna de saudação muito**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="e48b0-137">Clique no cabeçalho de coluna hello e, em seguida, arraste a coluna de saudação entre hello **EnglishDayNameOfWeek** coluna e hello **DayNumberOfMonth** coluna.</span><span class="sxs-lookup"><span data-stu-id="e48b0-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="e48b0-138">A movimentação das colunas na tabela torna mais fácil toonavigate.</span><span class="sxs-lookup"><span data-stu-id="e48b0-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="e48b0-139">coluna calculada do Hello DayOfWeek fornece um nome classificável para o dia de saudação da semana.</span><span class="sxs-lookup"><span data-stu-id="e48b0-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="e48b0-140">Criar uma coluna calculada ProductSubcategoryName na tabela DimProduct de saudação</span><span class="sxs-lookup"><span data-stu-id="e48b0-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="e48b0-141">Em Olá **DimProduct** de tabela, role toohello à direita da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48b0-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="e48b0-142">Aviso hello mais à direita coluna é nomeada **adicionar coluna** (em itálico), clique no cabeçalho da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48b0-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="e48b0-143">Na barra de fórmulas hello, digite Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="e48b0-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="e48b0-144">Renomear a coluna de saudação muito**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="e48b0-145">coluna calculada do Hello ProductSubcategoryName está toocreate usado uma hierarquia na tabela DimProduct hello, o que inclui dados de saudação EnglishProductSubcategoryName coluna na tabela de DimProductSubcategory de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48b0-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="e48b0-146">Hierarquias não podem abranger mais de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e48b0-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="e48b0-147">Você criará hierarquias posteriormente, na Lição 9.</span><span class="sxs-lookup"><span data-stu-id="e48b0-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="e48b0-148">Criar uma coluna calculada ProductCategoryName na tabela DimProduct de saudação</span><span class="sxs-lookup"><span data-stu-id="e48b0-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="e48b0-149">Com hello **DimProduct** tabela ainda ativa, clique em Olá **coluna** menu e clique **adicionar coluna**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="e48b0-150">Na barra de fórmulas hello, digite Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="e48b0-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="e48b0-151">Renomear a coluna de saudação muito**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="e48b0-152">coluna calculada do Hello ProductCategoryName é usado toocreate uma hierarquia na tabela DimProduct hello, o que inclui dados de saudação EnglishProductCategoryName coluna na tabela de DimProductCategory de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48b0-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="e48b0-153">Hierarquias não podem abranger mais de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="e48b0-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="e48b0-154">Criar uma coluna calculada Margin na tabela de FactInternetSales Olá</span><span class="sxs-lookup"><span data-stu-id="e48b0-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="e48b0-155">No designer de modelo hello, selecione Olá **FactInternetSales** tabela.</span><span class="sxs-lookup"><span data-stu-id="e48b0-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="e48b0-156">Criar uma nova coluna calculada entre hello **SalesAmount** coluna e hello **TaxAmt** coluna.</span><span class="sxs-lookup"><span data-stu-id="e48b0-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="e48b0-157">Na barra de fórmulas hello, digite Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="e48b0-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="e48b0-158">Renomear a coluna de saudação muito**margem**.</span><span class="sxs-lookup"><span data-stu-id="e48b0-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="e48b0-160">coluna calculada do Hello Margin é usado tooanalyze as margens de lucro para cada venda.</span><span class="sxs-lookup"><span data-stu-id="e48b0-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="e48b0-161">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="e48b0-161">What's next?</span></span>
<span data-ttu-id="e48b0-162">[Lição 6: criar medidas](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="e48b0-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
