---
<span data-ttu-id="eb46d-101">título: aaa "lição do tutorial do Azure Analysis Services 7: criar indicadores chave de desempenho | Descrição de Microsoft Docs": descreve como indicadores de desempenho chave toocreate em Olá projeto do tutorial do Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="eb46d-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="eb46d-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="eb46d-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="eb46d-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="eb46d-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="eb46d-104">Lição 7: criar indicadores chave de desempenho</span><span class="sxs-lookup"><span data-stu-id="eb46d-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="eb46d-105">Nesta lição, você cria KPIs (indicadores chave de desempenho).</span><span class="sxs-lookup"><span data-stu-id="eb46d-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="eb46d-106">Os KPIs são usados toogauge o desempenho de um valor definido por um *Base* medidas, em relação a um *destino* também definido por uma medida ou valor absoluto do valor.</span><span class="sxs-lookup"><span data-stu-id="eb46d-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="eb46d-107">Em aplicativos cliente de relatório, os KPIs podem proporcionar os profissionais de negócios toounderstand uma maneira rápida e fácil um resumo das tendências de êxito ou tooidentify de negócios.</span><span class="sxs-lookup"><span data-stu-id="eb46d-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="eb46d-108">toolearn mais, consulte [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="eb46d-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="eb46d-109">Estimado tempo toocomplete nesta lição: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="eb46d-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="eb46d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eb46d-110">Prerequisites</span></span>  
<span data-ttu-id="eb46d-111">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="eb46d-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="eb46d-112">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 6: criar medidas](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="eb46d-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="eb46d-113">Criar indicadores chave de desempenho</span><span class="sxs-lookup"><span data-stu-id="eb46d-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="eb46d-114">toocreate um KPI InternetCurrentQuarterSalesPerformance</span><span class="sxs-lookup"><span data-stu-id="eb46d-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="eb46d-115">No designer de modelo hello, clique em Olá **FactInternetSales** tabela.</span><span class="sxs-lookup"><span data-stu-id="eb46d-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="eb46d-116">Na grade de medida hello, clique em uma célula vazia.</span><span class="sxs-lookup"><span data-stu-id="eb46d-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="eb46d-117">Na barra de fórmulas hello, acima da tabela hello, digite Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="eb46d-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="eb46d-118">Essa medida serve como a medida Base Olá Olá KPI.</span><span class="sxs-lookup"><span data-stu-id="eb46d-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="eb46d-119">Clique com o botão direito do mouse em **InternetCurrentQuarterSalesPerformance** > **Criar KPI**.</span><span class="sxs-lookup"><span data-stu-id="eb46d-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="eb46d-120">Na caixa de diálogo do hello desempenho KPI (indicador chave), em **destino** selecione **valor absoluto**e, em seguida, digite **1.1**.</span><span class="sxs-lookup"><span data-stu-id="eb46d-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="eb46d-121">No campo de (baixa) de controle deslizante esquerdo hello, digite **1**e, em seguida, no controle deslizante à direita (alto) de hello, digite **1.07**.</span><span class="sxs-lookup"><span data-stu-id="eb46d-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="eb46d-122">Em **selecionar estilo de ícone**, selecione o triângulo de losango (vermelho), hello (amarelo), círculo de tipo de ícone (verde).</span><span class="sxs-lookup"><span data-stu-id="eb46d-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="eb46d-124">Saudação de aviso expansível **descrições** rótulo abaixo estilos de ícone disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="eb46d-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="eb46d-125">Use as descrições para Olá várias toomake de elementos KPI-los mais identificáveis nos aplicativos cliente.</span><span class="sxs-lookup"><span data-stu-id="eb46d-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="eb46d-126">Clique em **Okey** toocomplete Olá KPI.</span><span class="sxs-lookup"><span data-stu-id="eb46d-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="eb46d-127">Na grade de medida hello, observe Olá ícone próximo toohello **InternetCurrentQuarterSalesPerformance** medidas.</span><span class="sxs-lookup"><span data-stu-id="eb46d-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="eb46d-128">Esse ícone indica que essa medida serve como um valor Base para um KPI.</span><span class="sxs-lookup"><span data-stu-id="eb46d-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="eb46d-129">toocreate um KPI InternetCurrentQuarterMarginPerformance</span><span class="sxs-lookup"><span data-stu-id="eb46d-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="eb46d-130">Na grade de medida Olá para Olá **FactInternetSales** da tabela, clique em uma célula vazia.</span><span class="sxs-lookup"><span data-stu-id="eb46d-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="eb46d-131">Na barra de fórmulas hello, acima da tabela hello, digite Olá seguinte fórmula:</span><span class="sxs-lookup"><span data-stu-id="eb46d-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="eb46d-132">Clique com o botão direito do mouse em **InternetCurrentQuarterMarginPerformance** > **Criar KPI**.</span><span class="sxs-lookup"><span data-stu-id="eb46d-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="eb46d-133">Na caixa de diálogo do hello desempenho KPI (indicador chave), em **destino** selecione **valor absoluto**e, em seguida, digite **1.25**.</span><span class="sxs-lookup"><span data-stu-id="eb46d-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="eb46d-134">No campo de controle deslizante de (baixa) à esquerda de hello, slides até que o campo Olá exibe **0,8**, e saudação de slide, em seguida, no campo de controle deslizante (alto), até que o campo Olá exibe **1.03**.</span><span class="sxs-lookup"><span data-stu-id="eb46d-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="eb46d-135">Em **selecionar estilo de ícone**, selecione a forma de losango hello (vermelha), triângulo (amarelo), tipo de ícone de círculo (verde) e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="eb46d-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="eb46d-136">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="eb46d-136">What's next?</span></span>
<span data-ttu-id="eb46d-137">[Lição 8: criar perspectivas](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="eb46d-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
