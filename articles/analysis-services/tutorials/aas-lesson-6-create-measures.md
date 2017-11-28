---
<span data-ttu-id="e225a-101">título: aaa "lição do tutorial do Azure Analysis Services 6: criar medidas | Descrição de Microsoft Docs": descreve como toocreate medidas no projeto do tutorial hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="e225a-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="e225a-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="e225a-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="e225a-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 01/06/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="e225a-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="e225a-104">Lição 6: criar medidas</span><span class="sxs-lookup"><span data-stu-id="e225a-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="e225a-105">Nesta lição, você criará medidas toobe incluído em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="e225a-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="e225a-106">Toohello semelhante calculado colunas que você criou, uma medida é um cálculo criado usando uma fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="e225a-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="e225a-107">No entanto, ao contrário de colunas calculadas, as medidas são avaliadas com base em um *filtro* selecionado pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="e225a-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="e225a-108">Por exemplo, uma coluna particular ou uma segmentação de dados adicionados toohello campo de rótulos de linha em uma tabela dinâmica.</span><span class="sxs-lookup"><span data-stu-id="e225a-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="e225a-109">Um valor para cada célula no filtro de saudação é calculado pela medida de saudação aplicada.</span><span class="sxs-lookup"><span data-stu-id="e225a-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="e225a-110">As medidas são cálculos avançados e flexíveis que você deseja tooinclude em quase todos os modelos de tabela tooperform dinâmico cálculos em dados numéricos.</span><span class="sxs-lookup"><span data-stu-id="e225a-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="e225a-111">mais, consulte toolearn [medidas](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="e225a-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="e225a-112">toocreate medidas, que você usar o hello *grade de medida*.</span><span class="sxs-lookup"><span data-stu-id="e225a-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="e225a-113">Por padrão, cada tabela tem uma grade de medida vazia; no entanto, você normalmente não criará medidas para todas as tabelas.</span><span class="sxs-lookup"><span data-stu-id="e225a-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="e225a-114">grade de medida de saudação aparece abaixo de uma tabela no designer de modelo hello quando no modo de exibição de dados.</span><span class="sxs-lookup"><span data-stu-id="e225a-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="e225a-115">toohide ou Mostrar grade de medida Olá para uma tabela, clique em Olá **tabela** menu e clique **Mostrar grade de medida**.</span><span class="sxs-lookup"><span data-stu-id="e225a-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="e225a-116">Você pode criar uma medida clicando em uma célula vazia na grade de medida hello e digitando uma fórmula DAX na barra de fórmulas hello.</span><span class="sxs-lookup"><span data-stu-id="e225a-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="e225a-117">Quando você clique insira toocomplete Olá a fórmula, medida hello e aparece na célula de saudação.</span><span class="sxs-lookup"><span data-stu-id="e225a-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="e225a-118">Você também pode criar medidas usando uma função de agregação padrão clicando em uma coluna e, em seguida, clicando em Olá botão AutoSoma (**∑**) na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e225a-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="e225a-119">As medidas criadas usando o recurso de AutoSoma Olá aparecem na célula de grade de medida Olá diretamente sob a coluna de hello, mas podem ser movidas.</span><span class="sxs-lookup"><span data-stu-id="e225a-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="e225a-120">Nesta lição, você criará medidas inserindo uma fórmula DAX na barra de fórmulas hello e pelo recurso de AutoSoma hello.</span><span class="sxs-lookup"><span data-stu-id="e225a-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="e225a-121">Estimado tempo toocomplete nesta lição: **30 minutos**</span><span class="sxs-lookup"><span data-stu-id="e225a-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="e225a-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e225a-122">Prerequisites</span></span>  
<span data-ttu-id="e225a-123">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="e225a-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="e225a-124">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 5: criar colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e225a-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="e225a-125">Criar medidas</span><span class="sxs-lookup"><span data-stu-id="e225a-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="e225a-126">uma medida de DaysCurrentQuarterToDate na tabela DimDate de saudação do toocreate</span><span class="sxs-lookup"><span data-stu-id="e225a-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="e225a-127">No designer de modelo hello, clique em Olá **DimDate** tabela.</span><span class="sxs-lookup"><span data-stu-id="e225a-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="e225a-128">Na grade de medida hello, clique em célula vazia do hello superior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="e225a-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="e225a-129">Na barra de fórmulas hello, digite Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="e225a-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="e225a-130">Célula do aviso Olá superior esquerda agora contém um nome de medida, **DaysCurrentQuarterToDate**, seguido pelo resultado hello, **92**.</span><span class="sxs-lookup"><span data-stu-id="e225a-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="e225a-132">Diferente das colunas calculadas, com fórmulas de medida, você pode digitar o nome de medida hello, seguido por dois-pontos, seguido pela expressão de fórmula hello.</span><span class="sxs-lookup"><span data-stu-id="e225a-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="e225a-133">uma medida de DaysInCurrentQuarter na tabela DimDate de saudação do toocreate</span><span class="sxs-lookup"><span data-stu-id="e225a-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="e225a-134">Com hello **DimDate** ainda ativa no designer de modelo hello, na grade de medida de saudação da tabela, clique Olá a célula vazia abaixo da medida Olá criada.</span><span class="sxs-lookup"><span data-stu-id="e225a-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="e225a-135">Na barra de fórmulas hello, digite Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="e225a-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="e225a-136">Ao criar uma taxa de comparação entre um período incompleto e hello período anterior.</span><span class="sxs-lookup"><span data-stu-id="e225a-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="e225a-137">fórmula de Olá deve calcular a proporção de saudação do período de saudação decorrido e compará-la toohello mesma proporção em Olá período anterior.</span><span class="sxs-lookup"><span data-stu-id="e225a-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="e225a-138">Nesse caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] fornece Olá proporção decorrido em Olá período atual.</span><span class="sxs-lookup"><span data-stu-id="e225a-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="e225a-139">toocreate uma medida InternetDistinctCountSalesOrder na tabela de FactInternetSales Olá</span><span class="sxs-lookup"><span data-stu-id="e225a-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="e225a-140">Clique em Olá **FactInternetSales** tabela.</span><span class="sxs-lookup"><span data-stu-id="e225a-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="e225a-141">Clique em Olá **SalesOrderNumber** título de coluna.</span><span class="sxs-lookup"><span data-stu-id="e225a-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="e225a-142">Na barra de ferramentas hello, clique em Olá de seta para baixo próxima toohello AutoSoma (**∑**) botão e, em seguida, selecione **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="e225a-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="e225a-143">recurso de AutoSoma Olá automaticamente cria uma medida para a coluna selecionada hello, usando a fórmula de agregação padrão DistinctCount hello.</span><span class="sxs-lookup"><span data-stu-id="e225a-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="e225a-145">Na grade de medida hello, clique em nova medida de Olá e, em seguida, em Olá **propriedades** janela, na **nome da medida**, renomeie a medida de saudação muito**InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="e225a-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="e225a-146">medidas adicionais na tabela de FactInternetSales Olá toocreate</span><span class="sxs-lookup"><span data-stu-id="e225a-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="e225a-147">Usando o recurso de AutoSoma hello, crie e nomeie Olá medidas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e225a-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="e225a-148">Coluna</span><span class="sxs-lookup"><span data-stu-id="e225a-148">Column</span></span>|<span data-ttu-id="e225a-149">Nome da medida</span><span class="sxs-lookup"><span data-stu-id="e225a-149">Measure name</span></span>|<span data-ttu-id="e225a-150">AutoSoma (∑)</span><span class="sxs-lookup"><span data-stu-id="e225a-150">AutoSum (∑)</span></span>|<span data-ttu-id="e225a-151">Fórmula</span><span class="sxs-lookup"><span data-stu-id="e225a-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="e225a-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="e225a-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="e225a-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="e225a-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="e225a-154">Contagem</span><span class="sxs-lookup"><span data-stu-id="e225a-154">Count</span></span>|<span data-ttu-id="e225a-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="e225a-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="e225a-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="e225a-156">OrderQuantity</span></span>|<span data-ttu-id="e225a-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="e225a-157">InternetTotalUnits</span></span>|<span data-ttu-id="e225a-158">Soma</span><span class="sxs-lookup"><span data-stu-id="e225a-158">Sum</span></span>|<span data-ttu-id="e225a-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="e225a-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="e225a-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="e225a-160">DiscountAmount</span></span>|<span data-ttu-id="e225a-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="e225a-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="e225a-162">Soma</span><span class="sxs-lookup"><span data-stu-id="e225a-162">Sum</span></span>|<span data-ttu-id="e225a-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="e225a-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="e225a-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="e225a-164">TotalProductCost</span></span>|<span data-ttu-id="e225a-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="e225a-165">InternetTotalProductCost</span></span>|<span data-ttu-id="e225a-166">Soma</span><span class="sxs-lookup"><span data-stu-id="e225a-166">Sum</span></span>|<span data-ttu-id="e225a-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="e225a-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="e225a-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="e225a-168">SalesAmount</span></span>|<span data-ttu-id="e225a-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="e225a-169">InternetTotalSales</span></span>|<span data-ttu-id="e225a-170">Soma</span><span class="sxs-lookup"><span data-stu-id="e225a-170">Sum</span></span>|<span data-ttu-id="e225a-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="e225a-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="e225a-172">Margin</span><span class="sxs-lookup"><span data-stu-id="e225a-172">Margin</span></span>|<span data-ttu-id="e225a-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="e225a-173">InternetTotalMargin</span></span>|<span data-ttu-id="e225a-174">Soma</span><span class="sxs-lookup"><span data-stu-id="e225a-174">Sum</span></span>|<span data-ttu-id="e225a-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="e225a-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="e225a-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="e225a-176">TaxAmt</span></span>|<span data-ttu-id="e225a-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="e225a-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="e225a-178">Soma</span><span class="sxs-lookup"><span data-stu-id="e225a-178">Sum</span></span>|<span data-ttu-id="e225a-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="e225a-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="e225a-180">Freight</span><span class="sxs-lookup"><span data-stu-id="e225a-180">Freight</span></span>|<span data-ttu-id="e225a-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="e225a-181">InternetTotalFreight</span></span>|<span data-ttu-id="e225a-182">Soma</span><span class="sxs-lookup"><span data-stu-id="e225a-182">Sum</span></span>|<span data-ttu-id="e225a-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="e225a-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="e225a-184">Ao clicar em uma célula vazia na grade de medida hello e usando a barra de fórmulas hello, criar e mede a seguir Olá nome em ordem:</span><span class="sxs-lookup"><span data-stu-id="e225a-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
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
  
<span data-ttu-id="e225a-185">Medidas criadas para Olá FactInternetSales tabela podem ser dados financeiros essenciais de tooanalyze usadas, como vendas, custos e margem de lucro para itens definidos pelo filtro selecionado do usuário Olá.</span><span class="sxs-lookup"><span data-stu-id="e225a-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="e225a-186">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="e225a-186">What's next?</span></span>
<span data-ttu-id="e225a-187">[Lição 7: criar indicadores chave de desempenho](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="e225a-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
