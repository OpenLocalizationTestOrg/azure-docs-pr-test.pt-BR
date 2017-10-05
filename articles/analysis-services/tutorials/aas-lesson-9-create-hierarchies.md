---
title: "Lição 9 do tutorial do Azure Analysis Services: criar hierarquias | Microsoft Docs"
description: 
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
ms.openlocfilehash: d628dc621335acf231342a6d9186079de16e85f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="b432f-102">Lição 9: criar hierarquias</span><span class="sxs-lookup"><span data-stu-id="b432f-102">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b432f-103">Nesta lição, você cria hierarquias.</span><span class="sxs-lookup"><span data-stu-id="b432f-103">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="b432f-104">As hierarquias são grupos de colunas organizados em níveis. Por exemplo, uma hierarquia de Geografia pode ter subníveis para País, Estado, Região e Cidade.</span><span class="sxs-lookup"><span data-stu-id="b432f-104">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="b432f-105">As hierarquias podem aparecer separadas de outras colunas em uma lista de campos de aplicativo cliente de relatório, facilitando sua navegação e inclusão em um relatório pelos usuários do cliente.</span><span class="sxs-lookup"><span data-stu-id="b432f-105">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span></span> <span data-ttu-id="b432f-106">Para saber mais, confira [Hierarquias](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="b432f-106">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="b432f-107">Para criar hierarquias, use o designer de modelo em *Exibição de Diagrama*.</span><span class="sxs-lookup"><span data-stu-id="b432f-107">To create hierarchies, use the model designer in *Diagram View*.</span></span> <span data-ttu-id="b432f-108">Não há suporte para criar e gerenciar hierarquias na Exibição de Dados.</span><span class="sxs-lookup"><span data-stu-id="b432f-108">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="b432f-109">Tempo estimado para conclusão desta lição: **20 minutos**</span><span class="sxs-lookup"><span data-stu-id="b432f-109">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b432f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b432f-110">Prerequisites</span></span>  
<span data-ttu-id="b432f-111">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="b432f-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b432f-112">Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 8: criar perspectivas](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="b432f-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="b432f-113">Criar hierarquias</span><span class="sxs-lookup"><span data-stu-id="b432f-113">Create hierarchies</span></span>  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a><span data-ttu-id="b432f-114">Para criar uma hierarquia Categoria na tabela DimProduct</span><span class="sxs-lookup"><span data-stu-id="b432f-114">To create a Category hierarchy in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="b432f-115">No designer de modelo (exibição de diagrama), clique com o botão direito do mouse na tabela **DimProduct** > **Criar Hierarquia**.</span><span class="sxs-lookup"><span data-stu-id="b432f-115">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="b432f-116">Uma nova hierarquia aparece na parte inferior da janela da tabela.</span><span class="sxs-lookup"><span data-stu-id="b432f-116">A new hierarchy appears at the bottom of the table window.</span></span> <span data-ttu-id="b432f-117">Renomeie a hierarquia como **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="b432f-117">Rename the hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="b432f-118">Clique e arraste a coluna **ProductCategoryName** para a nova hierarquia **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="b432f-118">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="b432f-119">Na hierarquia **Categoria**, clique com o botão direito do mouse em **ProductCategoryName** > **Renomear** e, em seguida, digite **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="b432f-119">In the **Category** hierarchy, right-click the **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="b432f-120">Renomear uma coluna em uma hierarquia não renomeia essa coluna na tabela.</span><span class="sxs-lookup"><span data-stu-id="b432f-120">Renaming a column in a hierarchy does not rename that column in the table.</span></span> <span data-ttu-id="b432f-121">Uma coluna em uma hierarquia é apenas uma representação da coluna na tabela.</span><span class="sxs-lookup"><span data-stu-id="b432f-121">A column in a hierarchy is just a representation of the column in the table.</span></span>  
  
4.  <span data-ttu-id="b432f-122">Clique e arraste a coluna **ProductSubcategoryName** para a hierarquia **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="b432f-122">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span></span> <span data-ttu-id="b432f-123">Renomeie-a como **Subcategoria**.</span><span class="sxs-lookup"><span data-stu-id="b432f-123">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="b432f-124">Clique com o botão direito do mouse na coluna **ModelName** > **Adicionar à hierarquia** e, em seguida, selecione **Categoria**.</span><span class="sxs-lookup"><span data-stu-id="b432f-124">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span></span> <span data-ttu-id="b432f-125">Renomeie-a como **Modelo**.</span><span class="sxs-lookup"><span data-stu-id="b432f-125">Rename it **Model**.</span></span>

6.  <span data-ttu-id="b432f-126">Finalmente, adicione **EnglishProductName** à hierarquia Categoria.</span><span class="sxs-lookup"><span data-stu-id="b432f-126">Finally, add **EnglishProductName** to the Category hierarchy.</span></span> <span data-ttu-id="b432f-127">Renomeie-a como **Produto**.</span><span class="sxs-lookup"><span data-stu-id="b432f-127">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a><span data-ttu-id="b432f-129">Para criar hierarquias na tabela DimDate</span><span class="sxs-lookup"><span data-stu-id="b432f-129">To create hierarchies in the DimDate table</span></span>  
  
1.  <span data-ttu-id="b432f-130">Na tabela **DimDate**, crie uma hierarquia chamada **Calendar**.</span><span class="sxs-lookup"><span data-stu-id="b432f-130">In the **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="b432f-131">Adicione as seguintes colunas em ordem:</span><span class="sxs-lookup"><span data-stu-id="b432f-131">Add the following columns in-order:</span></span>

    *  <span data-ttu-id="b432f-132">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="b432f-132">CalendarYear</span></span>
    *  <span data-ttu-id="b432f-133">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="b432f-133">CalendarSemester</span></span>
    *  <span data-ttu-id="b432f-134">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="b432f-134">CalendarQuarter</span></span>
    *  <span data-ttu-id="b432f-135">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="b432f-135">MonthCalendar</span></span>
    *  <span data-ttu-id="b432f-136">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="b432f-136">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="b432f-137">Na tabela **DimDate**, crie uma hierarquia **Fiscal**.</span><span class="sxs-lookup"><span data-stu-id="b432f-137">In the **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="b432f-138">Adicione as seguintes colunas em ordem:</span><span class="sxs-lookup"><span data-stu-id="b432f-138">Include the following columns in-order:</span></span>  
  
    *  <span data-ttu-id="b432f-139">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="b432f-139">FiscalYear</span></span>
    *  <span data-ttu-id="b432f-140">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="b432f-140">FiscalSemester</span></span>
    *  <span data-ttu-id="b432f-141">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="b432f-141">FiscalQuarter</span></span>
    *  <span data-ttu-id="b432f-142">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="b432f-142">MonthCalendar</span></span>
    *  <span data-ttu-id="b432f-143">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="b432f-143">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="b432f-144">Finalmente, na tabela **DimDate**, crie uma hierarquia **ProductionCalendar**.</span><span class="sxs-lookup"><span data-stu-id="b432f-144">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="b432f-145">Adicione as seguintes colunas em ordem:</span><span class="sxs-lookup"><span data-stu-id="b432f-145">Include the following columns in-order:</span></span>  
    *  <span data-ttu-id="b432f-146">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="b432f-146">CalendarYear</span></span>
    *  <span data-ttu-id="b432f-147">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="b432f-147">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="b432f-148">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="b432f-148">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="b432f-149">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="b432f-149">What's next?</span></span>
<span data-ttu-id="b432f-150">[Lição 10: criar partições](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="b432f-150">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
