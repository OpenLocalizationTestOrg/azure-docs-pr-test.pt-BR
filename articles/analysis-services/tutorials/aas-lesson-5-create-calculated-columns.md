---
title: "Lição 5 do tutorial do Azure Analysis Services: criar colunas calculadas | Microsoft Docs"
description: Descreve como criar colunas calculadas no projeto de tutorial do Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 893371145d77e156843271907aeef0c3756d0403
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="11a16-103">Lição 5: criar colunas calculadas</span><span class="sxs-lookup"><span data-stu-id="11a16-103">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="11a16-104">Nesta lição, você criará novos dados em seu modelo adicionando colunas calculadas.</span><span class="sxs-lookup"><span data-stu-id="11a16-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="11a16-105">Você pode criar colunas calculadas (como colunas personalizadas) ao usar Obter Dados usando o Editor de Consultas ou posteriormente no designer de modelos, do mesmo modo que você fará aqui.</span><span class="sxs-lookup"><span data-stu-id="11a16-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="11a16-106">Para saber mais, consulte [Colunas calculadas](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="11a16-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="11a16-107">Você criará cinco novas colunas calculadas em três tabelas diferentes.</span><span class="sxs-lookup"><span data-stu-id="11a16-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="11a16-108">As etapas são ligeiramente diferentes para cada tarefa, mostrando que há várias maneiras de criar colunas, renomeá-las e colocá-las em vários localizações em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="11a16-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="11a16-109">Nesta lição, você também usará primeiro as DAX (Expressões de Análise de Dados).</span><span class="sxs-lookup"><span data-stu-id="11a16-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="11a16-110">DAX é uma linguagem especial para criar expressões de fórmula altamente personalizáveis para modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="11a16-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="11a16-111">Neste tutorial, você usará o DAX para criar colunas calculadas, medidas e filtros de função.</span><span class="sxs-lookup"><span data-stu-id="11a16-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="11a16-112">Para saber mais, veja [DAX em modelos tabulares](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="11a16-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="11a16-113">Tempo estimado para conclusão desta lição: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="11a16-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="11a16-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="11a16-114">Prerequisites</span></span>  
<span data-ttu-id="11a16-115">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="11a16-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="11a16-116">Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 4: criar relações](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="11a16-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="11a16-117">Criar colunas calculadas</span><span class="sxs-lookup"><span data-stu-id="11a16-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="11a16-118">Criar uma coluna calculada MonthCalendar na tabela DimDate</span><span class="sxs-lookup"><span data-stu-id="11a16-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="11a16-119">Clique no menu **Modelo** > **Exibição de Modelo** > **Exibição de Dados**.</span><span class="sxs-lookup"><span data-stu-id="11a16-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="11a16-120">Colunas calculadas só podem ser criadas usando o designer de modelo na Exibição de Dados.</span><span class="sxs-lookup"><span data-stu-id="11a16-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="11a16-121">No designer de modelos, clique na tabela **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="11a16-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="11a16-122">Clique com o botão direito do mouse no cabeçalho de coluna **CalendarQuarter** e clique em **Inserir Coluna**.</span><span class="sxs-lookup"><span data-stu-id="11a16-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="11a16-123">Uma nova coluna chamada **Coluna Calculada 1** é inserida à esquerda da coluna **Trimestre do Calendário**.</span><span class="sxs-lookup"><span data-stu-id="11a16-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="11a16-124">Na barra de fórmulas acima da tabela, digite a seguinte fórmula DAX: o Preenchimento Automático ajuda você a digitar os nomes totalmente qualificados de colunas e tabelas e lista as funções que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="11a16-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="11a16-125">Os valores são populados para todas as linhas na coluna calculada.</span><span class="sxs-lookup"><span data-stu-id="11a16-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="11a16-126">Se você rolar para baixo na tabela, verá que linhas podem ter valores diferentes para esta coluna, com base nos dados que estão em cada linha.</span><span class="sxs-lookup"><span data-stu-id="11a16-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="11a16-127">Renomeie esta coluna para **MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="11a16-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="11a16-129">A coluna calculada MonthCalendar fornece um nome classificável para o Mês.</span><span class="sxs-lookup"><span data-stu-id="11a16-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="11a16-130">Criar uma coluna calculada DayOfWeek na tabela DimDate</span><span class="sxs-lookup"><span data-stu-id="11a16-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="11a16-131">Com a tabela **DimDate** ainda ativa, clique no menu **Coluna** e depois em **Adicionar Coluna**.</span><span class="sxs-lookup"><span data-stu-id="11a16-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="11a16-132">Na barra de fórmulas, digite a seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="11a16-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="11a16-133">Quando você terminar de criar a fórmula, pressione ENTER.</span><span class="sxs-lookup"><span data-stu-id="11a16-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="11a16-134">A nova coluna é adicionada mais à direita da tabela.</span><span class="sxs-lookup"><span data-stu-id="11a16-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="11a16-135">Renomeie a coluna para **DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="11a16-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="11a16-136">Clique no título de coluna e arraste a coluna entre a coluna **EnglishDayNameOfWeek** e a coluna **DayNumberOfMonth**.</span><span class="sxs-lookup"><span data-stu-id="11a16-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="11a16-137">Mover as colunas na tabela facilita a navegação.</span><span class="sxs-lookup"><span data-stu-id="11a16-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="11a16-138">A coluna calculada DayOfWeek fornece um nome classificável para o dia da semana.</span><span class="sxs-lookup"><span data-stu-id="11a16-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="11a16-139">Criar uma coluna calculada ProductSubcategoryName na tabela DimProduct</span><span class="sxs-lookup"><span data-stu-id="11a16-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="11a16-140">Na tabela **DimProduct**, role até mais à direita da tabela.</span><span class="sxs-lookup"><span data-stu-id="11a16-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="11a16-141">Observe que a coluna mais à direita é denominada **Adicionar Coluna** (em itálico), clique no título de coluna.</span><span class="sxs-lookup"><span data-stu-id="11a16-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="11a16-142">Na barra de fórmulas, digite a seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="11a16-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="11a16-143">Renomeie a coluna para **ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="11a16-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="11a16-144">A coluna calculada ProductSubcategoryName é usada para criar uma hierarquia na tabela DimProduct, a qual inclui dados da coluna EnglishProductSubcategoryName na tabela DimProductSubcategory.</span><span class="sxs-lookup"><span data-stu-id="11a16-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="11a16-145">Hierarquias não podem abranger mais de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="11a16-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="11a16-146">Você criará hierarquias posteriormente, na Lição 9.</span><span class="sxs-lookup"><span data-stu-id="11a16-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="11a16-147">Criar uma coluna calculada ProductCategoryName na tabela DimProduct</span><span class="sxs-lookup"><span data-stu-id="11a16-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="11a16-148">Com a tabela **DimProduct** ainda ativa, clique no menu **Coluna** e depois em **Adicionar Coluna**.</span><span class="sxs-lookup"><span data-stu-id="11a16-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="11a16-149">Na barra de fórmulas, digite a seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="11a16-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="11a16-150">Renomeie a coluna para **ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="11a16-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="11a16-151">A coluna calculada ProductCategoryName é usada para criar uma hierarquia na tabela DimProduct, a qual inclui dados da coluna EnglishProductCategoryName na tabela DimProductCategory.</span><span class="sxs-lookup"><span data-stu-id="11a16-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="11a16-152">Hierarquias não podem abranger mais de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="11a16-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="11a16-153">Criar uma coluna calculada Margin na tabela FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="11a16-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="11a16-154">No designer de modelos, selecione a tabela **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="11a16-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="11a16-155">Crie uma nova coluna calculada entre a coluna **SalesAmount** e a coluna **TaxAmt**.</span><span class="sxs-lookup"><span data-stu-id="11a16-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="11a16-156">Na barra de fórmulas, digite a seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="11a16-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="11a16-157">Renomeie a coluna para **Margin**.</span><span class="sxs-lookup"><span data-stu-id="11a16-157">Rename the column to **Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="11a16-159">A coluna calculada Margin é usada para analisar as margens de lucro de cada venda.</span><span class="sxs-lookup"><span data-stu-id="11a16-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="11a16-160">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="11a16-160">What's next?</span></span>
<span data-ttu-id="11a16-161">[Lição 6: criar medidas](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="11a16-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
