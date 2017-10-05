---
title: "Lição 6 do tutorial do Azure Analysis Services: criar medidas | Microsoft Docs"
description: Descreve como criar medidas no projeto de tutorial do Azure Analysis Services.
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
ms.openlocfilehash: 90833fa9744eac298b0da82cd3d12f27cc237510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="0fb77-103">Lição 6: criar medidas</span><span class="sxs-lookup"><span data-stu-id="0fb77-103">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="0fb77-104">Nesta lição, você criará medidas a serem incluídas no modelo.</span><span class="sxs-lookup"><span data-stu-id="0fb77-104">In this lesson, you create measures to be included in your model.</span></span> <span data-ttu-id="0fb77-105">Semelhante às colunas calculadas que você criou, uma medida é um cálculo criado usando uma fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="0fb77-105">Similar to the calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="0fb77-106">No entanto, ao contrário de colunas calculadas, as medidas são avaliadas com base em um *filtro* selecionado pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="0fb77-106">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="0fb77-107">Por exemplo, uma coluna ou segmentação de dados específica adicionada ao campo Rótulos de Linha em uma Tabela Dinâmica.</span><span class="sxs-lookup"><span data-stu-id="0fb77-107">For example, a particular column or slicer added to the Row Labels field in a PivotTable.</span></span> <span data-ttu-id="0fb77-108">Um valor para cada célula no filtro é então calculado pela medida aplicada.</span><span class="sxs-lookup"><span data-stu-id="0fb77-108">A value for each cell in the filter is then calculated by the applied measure.</span></span> <span data-ttu-id="0fb77-109">As medidas são cálculos avançados e flexíveis que você desejará incluir em quase todos os modelos tabulares para executar cálculos dinâmicos em dados numéricos.</span><span class="sxs-lookup"><span data-stu-id="0fb77-109">Measures are powerful, flexible calculations that you want to include in almost all tabular models to perform dynamic calculations on numerical data.</span></span> <span data-ttu-id="0fb77-110">Para saber mais, veja [Medidas](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="0fb77-110">To learn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="0fb77-111">Para criar medidas, você deve usar a *Grade de Medida*.</span><span class="sxs-lookup"><span data-stu-id="0fb77-111">To create measures, you use the *Measure Grid*.</span></span> <span data-ttu-id="0fb77-112">Por padrão, cada tabela tem uma grade de medida vazia; no entanto, você normalmente não criará medidas para todas as tabelas.</span><span class="sxs-lookup"><span data-stu-id="0fb77-112">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="0fb77-113">A grade de medida aparece abaixo de uma tabela no designer de modelo na Exibição de Dados.</span><span class="sxs-lookup"><span data-stu-id="0fb77-113">The measure grid appears below a table in the model designer when in Data View.</span></span> <span data-ttu-id="0fb77-114">Para ocultar ou mostrar a grade de medida para uma tabela, clique no menu **tabela** e clique em **Mostrar Grade de Medida**.</span><span class="sxs-lookup"><span data-stu-id="0fb77-114">To hide or show the measure grid for a table, click the **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="0fb77-115">Você pode criar uma medida clicando em uma célula vazia na grade de medida e digitando uma fórmula DAX na barra de fórmulas.</span><span class="sxs-lookup"><span data-stu-id="0fb77-115">You can create a measure by clicking an empty cell in the measure grid, and then typing a DAX formula in the formula bar.</span></span> <span data-ttu-id="0fb77-116">Quando você clicar em ENTER para completar a fórmula, a medida aparecerá na célula.</span><span class="sxs-lookup"><span data-stu-id="0fb77-116">When you click ENTER to complete the formula, the measure then appears in the cell.</span></span> <span data-ttu-id="0fb77-117">Você também pode criar medidas usando uma função de agregação padrão clicando em uma coluna e, em seguida, clicando no botão AutoSoma (**∑**) na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="0fb77-117">You can also create measures using a standard aggregation function by clicking a column, and then clicking the AutoSum button (**∑**) on the toolbar.</span></span> <span data-ttu-id="0fb77-118">As medidas criadas usando o recurso AutoSoma aparecerão na célula da grade de medida diretamente abaixo da coluna, mas podem ser movidas.</span><span class="sxs-lookup"><span data-stu-id="0fb77-118">Measures created using the AutoSum feature appear in the measure grid cell directly beneath the column, but can be moved.</span></span>  
  
<span data-ttu-id="0fb77-119">Nesta lição, você criará medidas inserindo uma fórmula DAX na barra de fórmulas e usando o recurso AutoSoma.</span><span class="sxs-lookup"><span data-stu-id="0fb77-119">In this lesson, you create measures by both entering a DAX formula in the formula bar, and by using the AutoSum feature.</span></span>  
  
<span data-ttu-id="0fb77-120">Tempo estimado para conclusão desta lição: **30 minutos**</span><span class="sxs-lookup"><span data-stu-id="0fb77-120">Estimated time to complete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="0fb77-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0fb77-121">Prerequisites</span></span>  
<span data-ttu-id="0fb77-122">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="0fb77-122">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="0fb77-123">Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 5: criar colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0fb77-123">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="0fb77-124">Criar medidas</span><span class="sxs-lookup"><span data-stu-id="0fb77-124">Create measures</span></span>  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a><span data-ttu-id="0fb77-125">Para criar uma medida DaysCurrentQuarterToDate na tabela DimDate</span><span class="sxs-lookup"><span data-stu-id="0fb77-125">To create a DaysCurrentQuarterToDate measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="0fb77-126">No designer de modelo, clique na tabela **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="0fb77-126">In the model designer, click the **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="0fb77-127">Na grade de medida, clique na célula vazia superior esquerda.</span><span class="sxs-lookup"><span data-stu-id="0fb77-127">In the measure grid, click the top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="0fb77-128">Na barra de fórmulas, digite a seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="0fb77-128">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="0fb77-129">Observe que a célula superior esquerda agora contém um nome de medida, **DaysCurrentQuarterToDate**, seguido pelo resultado, **92**.</span><span class="sxs-lookup"><span data-stu-id="0fb77-129">Notice the top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by the result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="0fb77-131">Ao contrário do que ocorre com colunas calculadas, com as fórmulas de medida você pode digitar o nome da medida, seguido por um ponto-e-vírgula, seguido pela expressão da fórmula.</span><span class="sxs-lookup"><span data-stu-id="0fb77-131">Unlike calculated columns, with measure formulas you can type the measure name, followed by a colon, followed by the formula expression.</span></span>

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a><span data-ttu-id="0fb77-132">Para criar uma medida DaysInCurrentQuarter na tabela DimDate</span><span class="sxs-lookup"><span data-stu-id="0fb77-132">To create a DaysInCurrentQuarter measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="0fb77-133">Com a tabela **DimDate** ainda ativa no designer de modelo, na grade de medida, clique na célula vazia abaixo da medida que você criou.</span><span class="sxs-lookup"><span data-stu-id="0fb77-133">With the **DimDate** table still active in the model designer, in the measure grid, click the empty cell below the measure you created.</span></span>  
  
2.  <span data-ttu-id="0fb77-134">Na barra de fórmulas, digite a seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="0fb77-134">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="0fb77-135">Ao criar uma taxa de comparação entre um período incompleto e o período anterior.</span><span class="sxs-lookup"><span data-stu-id="0fb77-135">When creating a comparison ratio between one incomplete period and the previous period.</span></span> <span data-ttu-id="0fb77-136">A fórmula deve calcular a proporção do período decorrido e compará-la à mesma proporção do período anterior.</span><span class="sxs-lookup"><span data-stu-id="0fb77-136">The formula must calculate the proportion of the period that has elapsed and compare it to the same proportion in the previous period.</span></span> <span data-ttu-id="0fb77-137">Nesse caso, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] fornece a proporção decorrida no período atual.</span><span class="sxs-lookup"><span data-stu-id="0fb77-137">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives the proportion elapsed in the current period.</span></span>  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a><span data-ttu-id="0fb77-138">Para criar uma medida InternetDistinctCountSalesOrder na tabela FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="0fb77-138">To create an InternetDistinctCountSalesOrder measure in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="0fb77-139">Clique na tabela **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="0fb77-139">Click the **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="0fb77-140">Clique no título de coluna **SalesOrderNumber**.</span><span class="sxs-lookup"><span data-stu-id="0fb77-140">Click the **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="0fb77-141">Na barra de ferramentas, clique na seta para baixo ao lado de AutoSoma (**∑**) e selecione **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="0fb77-141">On the toolbar, click the down-arrow next to the AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="0fb77-142">O recurso AutoSoma cria automaticamente uma medida para a coluna selecionada usando a fórmula de agregação padrão DistinctCount.</span><span class="sxs-lookup"><span data-stu-id="0fb77-142">The AutoSum feature automatically creates a measure for the selected column using the DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="0fb77-144">Na grade de medida, clique em nova medida e, em seguida, na janela **Propriedades**, em **Nome da Medida**, renomeie a medida para **InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="0fb77-144">In the measure grid, click the new measure, and then in the **Properties** window, in **Measure Name**, rename the measure to **InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a><span data-ttu-id="0fb77-145">Para criar medidas adicionais na tabela FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="0fb77-145">To create additional measures in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="0fb77-146">Usando o recurso AutoSoma, crie e nomeie as seguintes medidas:</span><span class="sxs-lookup"><span data-stu-id="0fb77-146">By using the AutoSum feature, create and name the following measures:</span></span>  

    |<span data-ttu-id="0fb77-147">Coluna</span><span class="sxs-lookup"><span data-stu-id="0fb77-147">Column</span></span>|<span data-ttu-id="0fb77-148">Nome da medida</span><span class="sxs-lookup"><span data-stu-id="0fb77-148">Measure name</span></span>|<span data-ttu-id="0fb77-149">AutoSoma (∑)</span><span class="sxs-lookup"><span data-stu-id="0fb77-149">AutoSum (∑)</span></span>|<span data-ttu-id="0fb77-150">Fórmula</span><span class="sxs-lookup"><span data-stu-id="0fb77-150">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="0fb77-151">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="0fb77-151">SalesOrderLineNumber</span></span>|<span data-ttu-id="0fb77-152">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="0fb77-152">InternetOrderLinesCount</span></span>|<span data-ttu-id="0fb77-153">Contagem</span><span class="sxs-lookup"><span data-stu-id="0fb77-153">Count</span></span>|<span data-ttu-id="0fb77-154">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="0fb77-154">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="0fb77-155">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="0fb77-155">OrderQuantity</span></span>|<span data-ttu-id="0fb77-156">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="0fb77-156">InternetTotalUnits</span></span>|<span data-ttu-id="0fb77-157">Soma</span><span class="sxs-lookup"><span data-stu-id="0fb77-157">Sum</span></span>|<span data-ttu-id="0fb77-158">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="0fb77-158">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="0fb77-159">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="0fb77-159">DiscountAmount</span></span>|<span data-ttu-id="0fb77-160">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="0fb77-160">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="0fb77-161">Soma</span><span class="sxs-lookup"><span data-stu-id="0fb77-161">Sum</span></span>|<span data-ttu-id="0fb77-162">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="0fb77-162">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="0fb77-163">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="0fb77-163">TotalProductCost</span></span>|<span data-ttu-id="0fb77-164">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="0fb77-164">InternetTotalProductCost</span></span>|<span data-ttu-id="0fb77-165">Soma</span><span class="sxs-lookup"><span data-stu-id="0fb77-165">Sum</span></span>|<span data-ttu-id="0fb77-166">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="0fb77-166">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="0fb77-167">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="0fb77-167">SalesAmount</span></span>|<span data-ttu-id="0fb77-168">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="0fb77-168">InternetTotalSales</span></span>|<span data-ttu-id="0fb77-169">Soma</span><span class="sxs-lookup"><span data-stu-id="0fb77-169">Sum</span></span>|<span data-ttu-id="0fb77-170">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="0fb77-170">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="0fb77-171">Margin</span><span class="sxs-lookup"><span data-stu-id="0fb77-171">Margin</span></span>|<span data-ttu-id="0fb77-172">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="0fb77-172">InternetTotalMargin</span></span>|<span data-ttu-id="0fb77-173">Soma</span><span class="sxs-lookup"><span data-stu-id="0fb77-173">Sum</span></span>|<span data-ttu-id="0fb77-174">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="0fb77-174">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="0fb77-175">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="0fb77-175">TaxAmt</span></span>|<span data-ttu-id="0fb77-176">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="0fb77-176">InternetTotalTaxAmt</span></span>|<span data-ttu-id="0fb77-177">Soma</span><span class="sxs-lookup"><span data-stu-id="0fb77-177">Sum</span></span>|<span data-ttu-id="0fb77-178">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="0fb77-178">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="0fb77-179">Freight</span><span class="sxs-lookup"><span data-stu-id="0fb77-179">Freight</span></span>|<span data-ttu-id="0fb77-180">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="0fb77-180">InternetTotalFreight</span></span>|<span data-ttu-id="0fb77-181">Soma</span><span class="sxs-lookup"><span data-stu-id="0fb77-181">Sum</span></span>|<span data-ttu-id="0fb77-182">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="0fb77-182">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="0fb77-183">Clicando em uma célula vazia na grade de medida e usando a barra de fórmulas, crie e nomeie, em ordem, as seguintes medidas:</span><span class="sxs-lookup"><span data-stu-id="0fb77-183">By clicking an empty cell in the measure grid, and by using the formula bar, create, and name the following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="0fb77-184">As medidas criadas para a tabela FactInternetSales podem ser usadas para analisar dados financeiros essenciais, como vendas, custos e margem de lucro para itens definidos pelo filtro selecionado pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="0fb77-184">Measures created for the FactInternetSales table can be used to analyze critical financial data such as sales, costs, and profit margin for items defined by the user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="0fb77-185">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="0fb77-185">What's next?</span></span>
<span data-ttu-id="0fb77-186">[Lição 7: criar indicadores chave de desempenho](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="0fb77-186">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
