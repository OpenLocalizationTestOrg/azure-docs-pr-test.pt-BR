---
title: "Lição suplementar de tutorial do Azure Analysis Services: linhas de detalhes | Microsoft Docs"
description: "Descreve como criar uma expressão de linhas de detalhes no tutorial do Azure Analysis Services."
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
ms.openlocfilehash: fde5cd9a9efc3a13e731a91962ced5c086a72355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="777d7-103">Lição suplementar – Linhas de Detalhes</span><span class="sxs-lookup"><span data-stu-id="777d7-103">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="777d7-104">Nesta lição suplementar, você pode usar o Editor do DAX para definir uma expressão de linhas de detalhes personalizada.</span><span class="sxs-lookup"><span data-stu-id="777d7-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="777d7-105">Uma expressão de linhas de detalhes é uma propriedade em uma medida, fornecendo aos usuários finais mais informações sobre os resultados agregados de uma medida.</span><span class="sxs-lookup"><span data-stu-id="777d7-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="777d7-106">Tempo estimado para conclusão desta lição: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="777d7-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="777d7-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="777d7-107">Prerequisites</span></span>  
<span data-ttu-id="777d7-108">Este tópico de lição suplementar faz parte de um tutorial de modelagem Tabular.</span><span class="sxs-lookup"><span data-stu-id="777d7-108">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="777d7-109">Antes de executar as tarefas desta lição suplementar, você deve ter concluído todas as lições anteriores ou ter um projeto de modelo de amostra de Vendas pela Internet da Adventure Works concluído.</span><span class="sxs-lookup"><span data-stu-id="777d7-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-to-solve"></a><span data-ttu-id="777d7-110">O que precisamos resolver?</span><span class="sxs-lookup"><span data-stu-id="777d7-110">What do we need to solve?</span></span>
<span data-ttu-id="777d7-111">Examinaremos os detalhes de nossa medida InternetTotalSales antes de adicionarmos uma expressão de linhas de detalhes.</span><span class="sxs-lookup"><span data-stu-id="777d7-111">Let's look at the details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="777d7-112">No SSDT, clique no menu **Modelo** > **Analisar no Excel** para abrir o Excel e criar uma tabela dinâmica em branco.</span><span class="sxs-lookup"><span data-stu-id="777d7-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="777d7-113">Em **Campos de Tabela Dinâmica**, adicione a medida **InternetTotalSales** da tabela FactInternetSales a **Valores**, **CalendarYear** da tabela DimDate a **Colunas** e **EnglishCountryRegionName** a **Linhas**.</span><span class="sxs-lookup"><span data-stu-id="777d7-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="777d7-114">Nossa tabela dinâmica agora nos oferece resultados agregados da medida InternetTotalSales por regiões e por ano.</span><span class="sxs-lookup"><span data-stu-id="777d7-114">Our PivotTable now gives us aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="777d7-116">Na tabela dinâmica, clique duas vezes em um valor agregado para um ano e um nome de região.</span><span class="sxs-lookup"><span data-stu-id="777d7-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="777d7-117">Aqui, clicamos duas vezes no valor para Austrália e o ano de 2014.</span><span class="sxs-lookup"><span data-stu-id="777d7-117">Here we double-clicked the value for Australia and the year 2014.</span></span> <span data-ttu-id="777d7-118">Uma nova planilha abre os dados contidos, mas não os dados úteis.</span><span class="sxs-lookup"><span data-stu-id="777d7-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="777d7-120">O que gostaríamos de ver aqui é uma tabela contendo colunas e linhas de dados que contribuam para o resultado agregado de nossa medida InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="777d7-120">What we would like to see here is a table containing columns and rows of data that contribute to the aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="777d7-121">Para fazer isso, podemos adicionar uma expressão de linhas de detalhes como uma propriedade da medida.</span><span class="sxs-lookup"><span data-stu-id="777d7-121">To do that, we can add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="777d7-122">Adicionar uma expressão de linhas de detalhes</span><span class="sxs-lookup"><span data-stu-id="777d7-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="777d7-123">Para criar uma expressão de linhas de detalhes</span><span class="sxs-lookup"><span data-stu-id="777d7-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="777d7-124">No SSDT, na grade de medida da tabela FactInternetSales, clique na medida **InternetTotalSales**.</span><span class="sxs-lookup"><span data-stu-id="777d7-124">In SSDT, in the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="777d7-125">Em **Propriedades** > **Expressão de Linhas de Detalhes**, clique no botão do editor para abrir o Editor do DAX.</span><span class="sxs-lookup"><span data-stu-id="777d7-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="777d7-127">No Editor do DAX, digite a expressão a seguir:</span><span class="sxs-lookup"><span data-stu-id="777d7-127">In DAX Editor, enter the following expression:</span></span>

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

    <span data-ttu-id="777d7-128">Essa expressão especifica nomes de colunas, sendo que os resultados de medidas da tabela FactInternetSales e tabelas relacionadas são retornados quando um usuário clica duas vezes em um resultado agregado em uma tabela dinâmica ou relatório.</span><span class="sxs-lookup"><span data-stu-id="777d7-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="777d7-129">No Excel, exclua a planilha criada na Etapa 3, clique duas vezes um valor agregado.</span><span class="sxs-lookup"><span data-stu-id="777d7-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="777d7-130">Desta vez, com uma propriedade de expressão de linhas de detalhes definida para a medida, uma nova planilha será aberta contendo dados muito mais úteis.</span><span class="sxs-lookup"><span data-stu-id="777d7-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="777d7-132">Reimplante o modelo.</span><span class="sxs-lookup"><span data-stu-id="777d7-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="777d7-133">Consulte também</span><span class="sxs-lookup"><span data-stu-id="777d7-133">See Also</span></span>  
<span data-ttu-id="777d7-134">[Função SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="777d7-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="777d7-135">Lição Suplementar – Segurança Dinâmica</span><span class="sxs-lookup"><span data-stu-id="777d7-135">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="777d7-136">Lição Suplementar – hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="777d7-136">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
