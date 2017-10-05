---
title: "Lição suplementar de tutorial do Azure Analysis Services: hierarquias desbalanceadas | Microsoft Docs"
description: Descreve como corrigir hierarquias desbalanceadas no tutorial do Azure Analysis Services.
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
ms.openlocfilehash: 0f02ff73eb126cc397312e87bde50b3ee2d6ce53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="214ce-103">Lição suplementar – hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="214ce-103">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="214ce-104">Nesta lição suplementar, você resolver um problema comum ao dinamizar hierarquias que contêm valores em branco (membros) em diferentes níveis.</span><span class="sxs-lookup"><span data-stu-id="214ce-104">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="214ce-105">Por exemplo, uma organização em que um gerente de alto nível tem tanto gerentes departamentais quanto não gerentes como subordinados diretos.</span><span class="sxs-lookup"><span data-stu-id="214ce-105">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="214ce-106">Ou então, hierarquias geográficas compostas por país-região-cidade, em que algumas cidades não têm um estado ou província pai, por exemplo, Washington D.C. e Cidade do Vaticano.</span><span class="sxs-lookup"><span data-stu-id="214ce-106">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="214ce-107">Quando uma hierarquia tem membros em branco, ela geralmente desce a níveis diferentes ou desbalanceados.</span><span class="sxs-lookup"><span data-stu-id="214ce-107">When a hierarchy has blank members, it often descends to different, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="214ce-109">Modelos tabulares no nível de compatibilidade 1400 têm uma propriedade **Ocultar Membros** adicional para hierarquias.</span><span class="sxs-lookup"><span data-stu-id="214ce-109">Tabular models at the 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="214ce-110">A configuração **Padrão** pressupõe que não existem membros em branco em nenhum nível.</span><span class="sxs-lookup"><span data-stu-id="214ce-110">The **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="214ce-111">A configuração **Ocultar membros em branco** exclui membros em branco da hierarquia quando adicionada a uma tabela dinâmica ou relatório.</span><span class="sxs-lookup"><span data-stu-id="214ce-111">The **Hide blank members** setting excludes blank members from the hierarchy when added to a PivotTable or report.</span></span>  
  
<span data-ttu-id="214ce-112">Tempo estimado para conclusão desta lição: **20 minutos**</span><span class="sxs-lookup"><span data-stu-id="214ce-112">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="214ce-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="214ce-113">Prerequisites</span></span>  
<span data-ttu-id="214ce-114">Este tópico de lição suplementar faz parte de um tutorial de modelagem Tabular.</span><span class="sxs-lookup"><span data-stu-id="214ce-114">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="214ce-115">Antes de executar as tarefas desta lição suplementar, você deve ter concluído todas as lições anteriores ou ter um projeto de modelo de amostra de Vendas pela Internet da Adventure Works concluído.</span><span class="sxs-lookup"><span data-stu-id="214ce-115">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="214ce-116">Se você criou o projeto de vendas pela Internet da AW como parte do tutorial, o modelo ainda não contém nenhum dado ou hierarquias desbalanceadas.</span><span class="sxs-lookup"><span data-stu-id="214ce-116">If you've created the AW Internet Sales project as part of the tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="214ce-117">Para concluir esta lição suplementar, você precisa primeiro criar o problema adicionando algumas tabelas adicionais, criar relações, colunas calculadas, uma medida e uma nova hierarquia de Organização.</span><span class="sxs-lookup"><span data-stu-id="214ce-117">To complete this supplemental lesson, you first have to create the problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="214ce-118">Essa parte leva cerca de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="214ce-118">That part takes about 15 minutes.</span></span> <span data-ttu-id="214ce-119">Em seguida, você pode resolvê-la em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="214ce-119">Then, you get to solve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="214ce-120">Adicionar tabelas e objetos</span><span class="sxs-lookup"><span data-stu-id="214ce-120">Add tables and objects</span></span>
  
### <a name="to-add-new-tables-to-your-model"></a><span data-ttu-id="214ce-121">Para adicionar novas tabelas ao seu modelo</span><span class="sxs-lookup"><span data-stu-id="214ce-121">To add new tables to your model</span></span>
  
1.  <span data-ttu-id="214ce-122">No Gerenciador de Modelos tabulares, expanda **Fontes de Dados**, clique com o botão direito do mouse em sua conexão > **Importar Novas Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="214ce-122">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="214ce-123">No navegador, selecione **DimEmployee** e **FactResellerSales** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="214ce-123">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="214ce-124">No Editor de Consultas, clique em **Importar**</span><span class="sxs-lookup"><span data-stu-id="214ce-124">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="214ce-125">Crie as seguintes [relações](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="214ce-125">Create the following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="214ce-126">Tabela 1</span><span class="sxs-lookup"><span data-stu-id="214ce-126">Table 1</span></span>           | <span data-ttu-id="214ce-127">Coluna</span><span class="sxs-lookup"><span data-stu-id="214ce-127">Column</span></span>       | <span data-ttu-id="214ce-128">Direção do Filtro</span><span class="sxs-lookup"><span data-stu-id="214ce-128">Filter Direction</span></span>   | <span data-ttu-id="214ce-129">Tabela 2</span><span class="sxs-lookup"><span data-stu-id="214ce-129">Table 2</span></span>     | <span data-ttu-id="214ce-130">Coluna</span><span class="sxs-lookup"><span data-stu-id="214ce-130">Column</span></span>      | <span data-ttu-id="214ce-131">Ativo</span><span class="sxs-lookup"><span data-stu-id="214ce-131">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="214ce-132">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="214ce-132">FactResellerSales</span></span> | <span data-ttu-id="214ce-133">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="214ce-133">OrderDateKey</span></span> | <span data-ttu-id="214ce-134">Padrão</span><span class="sxs-lookup"><span data-stu-id="214ce-134">Default</span></span>            | <span data-ttu-id="214ce-135">DimDate</span><span class="sxs-lookup"><span data-stu-id="214ce-135">DimDate</span></span>     | <span data-ttu-id="214ce-136">Data</span><span class="sxs-lookup"><span data-stu-id="214ce-136">Date</span></span>        | <span data-ttu-id="214ce-137">Sim</span><span class="sxs-lookup"><span data-stu-id="214ce-137">Yes</span></span>    |
    | <span data-ttu-id="214ce-138">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="214ce-138">FactResellerSales</span></span> | <span data-ttu-id="214ce-139">DueDate</span><span class="sxs-lookup"><span data-stu-id="214ce-139">DueDate</span></span>      | <span data-ttu-id="214ce-140">Padrão</span><span class="sxs-lookup"><span data-stu-id="214ce-140">Default</span></span>            | <span data-ttu-id="214ce-141">DimDate</span><span class="sxs-lookup"><span data-stu-id="214ce-141">DimDate</span></span>     | <span data-ttu-id="214ce-142">Data</span><span class="sxs-lookup"><span data-stu-id="214ce-142">Date</span></span>        | <span data-ttu-id="214ce-143">Não</span><span class="sxs-lookup"><span data-stu-id="214ce-143">No</span></span>     |
    | <span data-ttu-id="214ce-144">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="214ce-144">FactResellerSales</span></span> | <span data-ttu-id="214ce-145">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="214ce-145">ShipDateKey</span></span>  | <span data-ttu-id="214ce-146">Padrão</span><span class="sxs-lookup"><span data-stu-id="214ce-146">Default</span></span>            | <span data-ttu-id="214ce-147">DimDate</span><span class="sxs-lookup"><span data-stu-id="214ce-147">DimDate</span></span>     | <span data-ttu-id="214ce-148">Data</span><span class="sxs-lookup"><span data-stu-id="214ce-148">Date</span></span>        | <span data-ttu-id="214ce-149">Não</span><span class="sxs-lookup"><span data-stu-id="214ce-149">No</span></span>     |
    | <span data-ttu-id="214ce-150">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="214ce-150">FactResellerSales</span></span> | <span data-ttu-id="214ce-151">ProductKey</span><span class="sxs-lookup"><span data-stu-id="214ce-151">ProductKey</span></span>   | <span data-ttu-id="214ce-152">Padrão</span><span class="sxs-lookup"><span data-stu-id="214ce-152">Default</span></span>            | <span data-ttu-id="214ce-153">DimProduct</span><span class="sxs-lookup"><span data-stu-id="214ce-153">DimProduct</span></span>  | <span data-ttu-id="214ce-154">ProductKey</span><span class="sxs-lookup"><span data-stu-id="214ce-154">ProductKey</span></span>  | <span data-ttu-id="214ce-155">Sim</span><span class="sxs-lookup"><span data-stu-id="214ce-155">Yes</span></span>    |
    | <span data-ttu-id="214ce-156">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="214ce-156">FactResellerSales</span></span> | <span data-ttu-id="214ce-157">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="214ce-157">EmployeeKey</span></span>  | <span data-ttu-id="214ce-158">Para Ambas as Tabelas</span><span class="sxs-lookup"><span data-stu-id="214ce-158">To Both Tables</span></span> | <span data-ttu-id="214ce-159">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="214ce-159">DimEmployee</span></span> | <span data-ttu-id="214ce-160">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="214ce-160">EmployeeKey</span></span> | <span data-ttu-id="214ce-161">Sim</span><span class="sxs-lookup"><span data-stu-id="214ce-161">Yes</span></span>    |

5. <span data-ttu-id="214ce-162">Na tabela **DimEmployee**, crie as seguintes [colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="214ce-162">In the **DimEmployee** table, create the following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="214ce-163">**Caminho**</span><span class="sxs-lookup"><span data-stu-id="214ce-163">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="214ce-164">**FullName**</span><span class="sxs-lookup"><span data-stu-id="214ce-164">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="214ce-165">**Level1**</span><span class="sxs-lookup"><span data-stu-id="214ce-165">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="214ce-166">**Level2**</span><span class="sxs-lookup"><span data-stu-id="214ce-166">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="214ce-167">**Level3**</span><span class="sxs-lookup"><span data-stu-id="214ce-167">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="214ce-168">**Level4**</span><span class="sxs-lookup"><span data-stu-id="214ce-168">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="214ce-169">**Level5**</span><span class="sxs-lookup"><span data-stu-id="214ce-169">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="214ce-170">Na tabela **DimEmployee**, crie uma [hierarquia](../tutorials/aas-lesson-9-create-hierarchies.md) chamada **Organização**.</span><span class="sxs-lookup"><span data-stu-id="214ce-170">In the **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="214ce-171">Adicione a seguintes colunas, em ordem: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="214ce-171">Add the following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="214ce-172">Na tabela **FactResellerSales**, crie a seguinte [medida](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="214ce-172">In the **FactResellerSales** table, create the following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="214ce-173">Use [Analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) para abrir o Excel e criar uma tabela dinâmica automaticamente.</span><span class="sxs-lookup"><span data-stu-id="214ce-173">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) to open Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="214ce-174">Em **Campos de Tabela Dinâmica**, adicione a hierarquia **Organização** da tabela **DimEmployee** a **Linhas** e a medida **ResellerTotalSales** da tabela **FactResellerSales** a **valores**.</span><span class="sxs-lookup"><span data-stu-id="214ce-174">In **PivotTable Fields**, add the **Organization** hierarchy from the **DimEmployee** table to **Rows**, and the **ResellerTotalSales** measure from the **FactResellerSales**  table to **Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="214ce-176">Como você pode ver na tabela dinâmica, a hierarquia exibe linhas que são irregulares.</span><span class="sxs-lookup"><span data-stu-id="214ce-176">As you can see in the PivotTable, the hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="214ce-177">Há muitas linhas em que os membros em branco são mostrados.</span><span class="sxs-lookup"><span data-stu-id="214ce-177">There are many rows where blank members are shown.</span></span>

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a><span data-ttu-id="214ce-178">Para corrigir a hierarquia desbalanceada definindo a propriedade Ocultar membros</span><span class="sxs-lookup"><span data-stu-id="214ce-178">To fix the ragged hierarchy by setting the Hide members property</span></span>

1.  <span data-ttu-id="214ce-179">Em **Gerenciador de Modelos tabulares**, expanda **Tabelas** > **DimEmployee** > **Hierarquias** > **Organização**.</span><span class="sxs-lookup"><span data-stu-id="214ce-179">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="214ce-180">Em **Propriedades** > **Ocultar Membros**, selecione **Ocultar membros em branco**.</span><span class="sxs-lookup"><span data-stu-id="214ce-180">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="214ce-182">De volta ao Excel, atualize a tabela dinâmica.</span><span class="sxs-lookup"><span data-stu-id="214ce-182">Back in Excel, refresh the PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="214ce-184">Agora isso tem uma aparência muito melhor!</span><span class="sxs-lookup"><span data-stu-id="214ce-184">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="214ce-185">Consulte também</span><span class="sxs-lookup"><span data-stu-id="214ce-185">See Also</span></span>   
[<span data-ttu-id="214ce-186">Lição 9: criar hierarquias</span><span class="sxs-lookup"><span data-stu-id="214ce-186">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="214ce-187">Lição Suplementar – Segurança Dinâmica</span><span class="sxs-lookup"><span data-stu-id="214ce-187">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="214ce-188">Lição suplementar – linhas de detalhes</span><span class="sxs-lookup"><span data-stu-id="214ce-188">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  