---
<span data-ttu-id="bb419-101">título: aaa "lição suplementar do tutorial do Azure Analysis Services: linhas de detalhes | Descrição de Microsoft Docs": descreve como toocreate uma expressão de linhas de detalhes em Olá tutorial do Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="bb419-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="bb419-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="bb419-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="bb419-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="bb419-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="bb419-104">Lição suplementar – Linhas de Detalhes</span><span class="sxs-lookup"><span data-stu-id="bb419-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="bb419-105">Nesta lição suplementar, você use Olá Editor DAX toodefine uma expressão personalizada de linhas de detalhes.</span><span class="sxs-lookup"><span data-stu-id="bb419-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="bb419-106">Uma expressão de linhas de detalhes é uma propriedade em uma medida, proporcionando aos usuários finais para obter mais informações sobre os resultados da saudação agregado de uma medida.</span><span class="sxs-lookup"><span data-stu-id="bb419-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="bb419-107">Estimado tempo toocomplete nesta lição: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="bb419-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="bb419-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bb419-108">Prerequisites</span></span>  
<span data-ttu-id="bb419-109">Este tópico de lição suplementar faz parte de um tutorial de modelagem Tabular.</span><span class="sxs-lookup"><span data-stu-id="bb419-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="bb419-110">Antes de executar tarefas de saudação nesta lição suplementar, você deve concluir todas as lições anteriores ou tem um projeto de modelo de exemplo Adventure Works Internet Sales concluído.</span><span class="sxs-lookup"><span data-stu-id="bb419-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="bb419-111">O que fazer precisamos toosolve?</span><span class="sxs-lookup"><span data-stu-id="bb419-111">What do we need toosolve?</span></span>
<span data-ttu-id="bb419-112">Vamos examinar os detalhes de saudação de nossa medida InternetTotalSales, antes de adicionar uma expressão de linhas de detalhes.</span><span class="sxs-lookup"><span data-stu-id="bb419-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="bb419-113">No SSDT, clique em Olá **modelo** menu > **analisar no Excel** tooopen Excel e criar uma tabela dinâmica em branco.</span><span class="sxs-lookup"><span data-stu-id="bb419-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="bb419-114">Em **PivotTable Fields**, adicionar Olá **InternetTotalSales** de medidas da tabela de FactInternetSales Olá muito**valores**, **CalendarYear**de saudação DimDate tabela muito**colunas**, e **EnglishCountryRegionName** muito**linhas**.</span><span class="sxs-lookup"><span data-stu-id="bb419-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="bb419-115">Agora, nossa tabela dinâmica oferece nos resultados agregados de medidas de InternetTotalSales Olá regiões e ano.</span><span class="sxs-lookup"><span data-stu-id="bb419-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="bb419-117">Em Olá tabela dinâmica, clique duas vezes em um valor agregado para um ano e um nome de região.</span><span class="sxs-lookup"><span data-stu-id="bb419-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="bb419-118">Aqui é clicado duas vezes valor Olá Austrália e hello ano 2014.</span><span class="sxs-lookup"><span data-stu-id="bb419-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="bb419-119">Uma nova planilha abre os dados contidos, mas não os dados úteis.</span><span class="sxs-lookup"><span data-stu-id="bb419-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="bb419-121">O que podemos gostariam de ter toosee aqui é uma tabela que contém colunas e linhas de dados que contribuem toohello agregado resultado de nossa medida InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="bb419-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="bb419-122">toodo que podemos adicionar uma expressão de linhas de detalhes como uma propriedade de medida hello.</span><span class="sxs-lookup"><span data-stu-id="bb419-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="bb419-123">Adicionar uma expressão de linhas de detalhes</span><span class="sxs-lookup"><span data-stu-id="bb419-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="bb419-124">toocreate uma expressão de linhas de detalhes</span><span class="sxs-lookup"><span data-stu-id="bb419-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="bb419-125">No SSDT, na grade de medida da tabela de FactInternetSales hello, clique em Olá **InternetTotalSales** medidas.</span><span class="sxs-lookup"><span data-stu-id="bb419-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="bb419-126">Em **propriedades** > **expressão de linhas de detalhes**, clique em Olá editor botão tooopen Olá Editor DAX.</span><span class="sxs-lookup"><span data-stu-id="bb419-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="bb419-128">No Editor do DAX, digite Olá expressão a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb419-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="bb419-129">Essa expressão especifica nomes de colunas, e os resultados de medida de saudação tabelas FactInternetSales e tabelas relacionadas são retornados quando um usuário clica duas vezes em um resultado agregado em uma tabela dinâmica ou relatório.</span><span class="sxs-lookup"><span data-stu-id="bb419-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="bb419-130">Novamente no Excel, excluir planilha Olá criada na etapa 3, em seguida, clique duas vezes em um valor agregado.</span><span class="sxs-lookup"><span data-stu-id="bb419-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="bb419-131">Neste momento, com uma propriedade de expressão de linhas de detalhes definida para medidas hello, uma nova planilha é aberta que contém dados muito mais útil.</span><span class="sxs-lookup"><span data-stu-id="bb419-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="bb419-133">Reimplante o modelo.</span><span class="sxs-lookup"><span data-stu-id="bb419-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="bb419-134">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bb419-134">See Also</span></span>  
<span data-ttu-id="bb419-135">[Função SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="bb419-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="bb419-136">Lição Suplementar – Segurança Dinâmica</span><span class="sxs-lookup"><span data-stu-id="bb419-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="bb419-137">Lição Suplementar – hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="bb419-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
