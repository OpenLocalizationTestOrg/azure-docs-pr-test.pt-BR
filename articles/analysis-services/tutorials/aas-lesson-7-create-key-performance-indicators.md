---
title: "Lição 7 do tutorial do Azure Analysis Services: criar indicadores chave de desempenho | Microsoft Docs"
description: Descreve como criar indicadores chave de desempenho no projeto de tutorial do Azure Analysis Services.
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: d78808421dd5acd907aa9e9000bb3b770a42c061
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="81ce7-103">Lição 7: criar indicadores chave de desempenho</span><span class="sxs-lookup"><span data-stu-id="81ce7-103">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="81ce7-104">Nesta lição, você cria KPIs (indicadores chave de desempenho).</span><span class="sxs-lookup"><span data-stu-id="81ce7-104">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="81ce7-105">Os KPIs são usados para medir o desempenho de um valor, definido por uma medida *Base* contra um valor de *Destino*, também definido por uma medida ou um valor absoluto.</span><span class="sxs-lookup"><span data-stu-id="81ce7-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="81ce7-106">Em aplicativos cliente de relatório, KPIs podem fornecer aos profissionais de negócios uma maneira rápida e fácil de entender um resumo de sucesso nos negócios ou para identificar tendências.</span><span class="sxs-lookup"><span data-stu-id="81ce7-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span></span> <span data-ttu-id="81ce7-107">Para obter mais informações, consulte [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="81ce7-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="81ce7-108">Tempo estimado para conclusão desta lição: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="81ce7-108">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="81ce7-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="81ce7-109">Prerequisites</span></span>  
<span data-ttu-id="81ce7-110">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="81ce7-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="81ce7-111">Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 6: criar medidas](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="81ce7-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="81ce7-112">Criar indicadores chave de desempenho</span><span class="sxs-lookup"><span data-stu-id="81ce7-112">Create Key Performance Indicators</span></span>  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="81ce7-113">Para criar um KPI de InternetCurrentQuarterSalesPerformance</span><span class="sxs-lookup"><span data-stu-id="81ce7-113">To create an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="81ce7-114">No designer de modelos, clique na tabela **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-114">In the model designer, click the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="81ce7-115">Na grade de medida, clique em uma célula vazia.</span><span class="sxs-lookup"><span data-stu-id="81ce7-115">In the measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="81ce7-116">Na barra de fórmulas acima da tabela, digite a fórmula a seguir:</span><span class="sxs-lookup"><span data-stu-id="81ce7-116">In the formula bar, above the table, type the following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="81ce7-117">Essa medida servirá como a medida Base para o KPI.</span><span class="sxs-lookup"><span data-stu-id="81ce7-117">This measure serves as the Base measure for the KPI.</span></span>  
  
4.  <span data-ttu-id="81ce7-118">Clique com o botão direito do mouse em **InternetCurrentQuarterSalesPerformance** > **Criar KPI**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-118">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="81ce7-119">Na caixa de diálogo KPI (Indicador Chave de Desempenho), em **Destino**, selecione **Valor Absoluto** e, em seguida, digite **1.1**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="81ce7-120">No campo de controle deslizante da esquerda (baixo), digite **1** e então, no campo de controle deslizante da direita (alto), digite **1.07**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="81ce7-121">Em **Selecionar Estilo de Ícone**, selecione o tipo de ícone losango (vermelho), triângulo (amarelo) e círculo (verde).</span><span class="sxs-lookup"><span data-stu-id="81ce7-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="81ce7-123">Observe o rótulo expansível **Descrições** abaixo dos estilos de ícone disponíveis.</span><span class="sxs-lookup"><span data-stu-id="81ce7-123">Notice the expandable **Descriptions** label below the available icon styles.</span></span> <span data-ttu-id="81ce7-124">Use as descrições para os vários elementos de KPI para torná-los mais identificáveis nos aplicativos cliente.</span><span class="sxs-lookup"><span data-stu-id="81ce7-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="81ce7-125">Clique em **OK** para concluir o KPI.</span><span class="sxs-lookup"><span data-stu-id="81ce7-125">Click **OK** to complete the KPI.</span></span>  
  
    <span data-ttu-id="81ce7-126">Na grade de medida, observe o ícone ao lado da medida **InternetCurrentQuarterSalesPerformance**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="81ce7-127">Esse ícone indica que essa medida serve como um valor Base para um KPI.</span><span class="sxs-lookup"><span data-stu-id="81ce7-127">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="81ce7-128">Para criar um KPI de InternetCurrentQuarterMarginPerformance</span><span class="sxs-lookup"><span data-stu-id="81ce7-128">To create an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="81ce7-129">Na grade de medida para a tabela **FactInternetSales**, clique em uma célula vazia.</span><span class="sxs-lookup"><span data-stu-id="81ce7-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="81ce7-130">Na barra de fórmulas acima da tabela, digite a fórmula a seguir:</span><span class="sxs-lookup"><span data-stu-id="81ce7-130">In the formula bar, above the table, type the following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="81ce7-131">Clique com o botão direito do mouse em **InternetCurrentQuarterMarginPerformance** > **Criar KPI**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="81ce7-132">Na caixa de diálogo KPI (Indicador Chave de Desempenho), em **Destino**, selecione **Valor Absoluto** e, em seguida, digite **1.25**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="81ce7-133">No campo de controle deslizante da esquerda (baixo), deslize até que o campo exiba **0.8** e, em seguida, deslize o campo de controle deslizante à direita (alto) até que o campo exiba **1.03**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="81ce7-134">Em **Selecionar Estilo de Ícone**, selecione o tipo de ícone losango (vermelho), triângulo (amarelo), círculo (verde) e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="81ce7-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="81ce7-135">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="81ce7-135">What's next?</span></span>
<span data-ttu-id="81ce7-136">[Lição 8: criar perspectivas](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="81ce7-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
