---
<span data-ttu-id="2c3b8-101">título: aaa "lição suplementar do tutorial do Azure Analysis Services: hierarquias desbalanceadas | Descrição de Microsoft Docs": descreve como toofix hierarquias desbalanceadas tutorial do hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="2c3b8-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="2c3b8-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="2c3b8-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="2c3b8-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="2c3b8-104">Lição suplementar – hierarquias desbalanceadas</span><span class="sxs-lookup"><span data-stu-id="2c3b8-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="2c3b8-105">Nesta lição suplementar, você resolver um problema comum ao dinamizar hierarquias que contêm valores em branco (membros) em diferentes níveis.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="2c3b8-106">Por exemplo, uma organização em que um gerente de alto nível tem tanto gerentes departamentais quanto não gerentes como subordinados diretos.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="2c3b8-107">Ou então, hierarquias geográficas compostas por país-região-cidade, em que algumas cidades não têm um estado ou província pai, por exemplo, Washington D.C. e Cidade do Vaticano.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="2c3b8-108">Quando uma hierarquia tem membros em branco, ele normalmente desce toodifferent ou irregulares, níveis.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="2c3b8-110">Modelos de tabela no nível de compatibilidade Olá 1400 têm adicional **ocultar membros** propriedade para hierarquias.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="2c3b8-111">Olá **padrão** configuração pressupõe que não existem membros em branco em qualquer nível.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="2c3b8-112">Olá **ocultar membros em branco** configuração exclui membros em branco da hierarquia de saudação quando adicionado tooa tabela dinâmica ou relatório.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="2c3b8-113">Estimado tempo toocomplete nesta lição: **20 minutos**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="2c3b8-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2c3b8-114">Prerequisites</span></span>  
<span data-ttu-id="2c3b8-115">Este tópico de lição suplementar faz parte de um tutorial de modelagem Tabular.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="2c3b8-116">Antes de executar tarefas de saudação nesta lição suplementar, você deve concluir todas as lições anteriores ou tem um projeto de modelo de exemplo Adventure Works Internet Sales concluído.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="2c3b8-117">Se você criou o projeto de vendas de Internet da AW hello como parte do tutorial hello, seu modelo ainda não contém dados ou hierarquias desbalanceadas.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="2c3b8-118">toocomplete nesta lição suplementar, você precisa primeiro toocreate Olá problema adicionando algumas tabelas adicionais, criar relações, colunas calculadas, uma medida e uma nova hierarquia da organização.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="2c3b8-119">Essa parte leva cerca de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="2c3b8-120">Em seguida, você pode obter toosolve em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="2c3b8-121">Adicionar tabelas e objetos</span><span class="sxs-lookup"><span data-stu-id="2c3b8-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="2c3b8-122">novo modelo de tooyour tabelas tooadd</span><span class="sxs-lookup"><span data-stu-id="2c3b8-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="2c3b8-123">No Gerenciador de Modelos tabulares, expanda **Fontes de Dados**, clique com o botão direito do mouse em sua conexão > **Importar Novas Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="2c3b8-124">No navegador, selecione **DimEmployee** e **FactResellerSales** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="2c3b8-125">No Editor de Consultas, clique em **Importar**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="2c3b8-126">Crie seguinte Olá [relações](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="2c3b8-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="2c3b8-127">Tabela 1</span><span class="sxs-lookup"><span data-stu-id="2c3b8-127">Table 1</span></span>           | <span data-ttu-id="2c3b8-128">Coluna</span><span class="sxs-lookup"><span data-stu-id="2c3b8-128">Column</span></span>       | <span data-ttu-id="2c3b8-129">Direção do Filtro</span><span class="sxs-lookup"><span data-stu-id="2c3b8-129">Filter Direction</span></span>   | <span data-ttu-id="2c3b8-130">Tabela 2</span><span class="sxs-lookup"><span data-stu-id="2c3b8-130">Table 2</span></span>     | <span data-ttu-id="2c3b8-131">Coluna</span><span class="sxs-lookup"><span data-stu-id="2c3b8-131">Column</span></span>      | <span data-ttu-id="2c3b8-132">Ativo</span><span class="sxs-lookup"><span data-stu-id="2c3b8-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="2c3b8-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2c3b8-133">FactResellerSales</span></span> | <span data-ttu-id="2c3b8-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="2c3b8-134">OrderDateKey</span></span> | <span data-ttu-id="2c3b8-135">Padrão</span><span class="sxs-lookup"><span data-stu-id="2c3b8-135">Default</span></span>            | <span data-ttu-id="2c3b8-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="2c3b8-136">DimDate</span></span>     | <span data-ttu-id="2c3b8-137">Data</span><span class="sxs-lookup"><span data-stu-id="2c3b8-137">Date</span></span>        | <span data-ttu-id="2c3b8-138">Sim</span><span class="sxs-lookup"><span data-stu-id="2c3b8-138">Yes</span></span>    |
    | <span data-ttu-id="2c3b8-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2c3b8-139">FactResellerSales</span></span> | <span data-ttu-id="2c3b8-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="2c3b8-140">DueDate</span></span>      | <span data-ttu-id="2c3b8-141">Padrão</span><span class="sxs-lookup"><span data-stu-id="2c3b8-141">Default</span></span>            | <span data-ttu-id="2c3b8-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="2c3b8-142">DimDate</span></span>     | <span data-ttu-id="2c3b8-143">Data</span><span class="sxs-lookup"><span data-stu-id="2c3b8-143">Date</span></span>        | <span data-ttu-id="2c3b8-144">Não</span><span class="sxs-lookup"><span data-stu-id="2c3b8-144">No</span></span>     |
    | <span data-ttu-id="2c3b8-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2c3b8-145">FactResellerSales</span></span> | <span data-ttu-id="2c3b8-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="2c3b8-146">ShipDateKey</span></span>  | <span data-ttu-id="2c3b8-147">Padrão</span><span class="sxs-lookup"><span data-stu-id="2c3b8-147">Default</span></span>            | <span data-ttu-id="2c3b8-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="2c3b8-148">DimDate</span></span>     | <span data-ttu-id="2c3b8-149">Data</span><span class="sxs-lookup"><span data-stu-id="2c3b8-149">Date</span></span>        | <span data-ttu-id="2c3b8-150">Não</span><span class="sxs-lookup"><span data-stu-id="2c3b8-150">No</span></span>     |
    | <span data-ttu-id="2c3b8-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2c3b8-151">FactResellerSales</span></span> | <span data-ttu-id="2c3b8-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="2c3b8-152">ProductKey</span></span>   | <span data-ttu-id="2c3b8-153">Padrão</span><span class="sxs-lookup"><span data-stu-id="2c3b8-153">Default</span></span>            | <span data-ttu-id="2c3b8-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="2c3b8-154">DimProduct</span></span>  | <span data-ttu-id="2c3b8-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="2c3b8-155">ProductKey</span></span>  | <span data-ttu-id="2c3b8-156">Sim</span><span class="sxs-lookup"><span data-stu-id="2c3b8-156">Yes</span></span>    |
    | <span data-ttu-id="2c3b8-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="2c3b8-157">FactResellerSales</span></span> | <span data-ttu-id="2c3b8-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="2c3b8-158">EmployeeKey</span></span>  | <span data-ttu-id="2c3b8-159">Tabelas de tooBoth</span><span class="sxs-lookup"><span data-stu-id="2c3b8-159">tooBoth Tables</span></span> | <span data-ttu-id="2c3b8-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="2c3b8-160">DimEmployee</span></span> | <span data-ttu-id="2c3b8-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="2c3b8-161">EmployeeKey</span></span> | <span data-ttu-id="2c3b8-162">Sim</span><span class="sxs-lookup"><span data-stu-id="2c3b8-162">Yes</span></span>    |

5. <span data-ttu-id="2c3b8-163">Em Olá **DimEmployee** de tabela, crie a seguinte Olá [colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="2c3b8-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="2c3b8-164">**Caminho**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="2c3b8-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="2c3b8-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="2c3b8-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="2c3b8-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="2c3b8-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="2c3b8-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="2c3b8-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="2c3b8-171">Em Olá **DimEmployee** de tabela, crie um [hierarquia](../tutorials/aas-lesson-9-create-hierarchies.md) chamado **organização**.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="2c3b8-172">Adicionar Olá colunas na ordem a seguir: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="2c3b8-173">Em Olá **FactResellerSales** de tabela, crie a seguinte Olá [medidas](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="2c3b8-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="2c3b8-174">Use [analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel e criar automaticamente uma tabela dinâmica.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="2c3b8-175">Em **PivotTable Fields**, adicionar Olá **organização** hierarquia da saudação **DimEmployee** tabela muito**linhas**e hello **ResellerTotalSales** medida da saudação **FactResellerSales** tabela muito**valores**.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="2c3b8-177">Como você pode ver na tabela dinâmica de hello, hierarquia Olá exibe linhas que são irregulares.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="2c3b8-178">Há muitas linhas em que os membros em branco são mostrados.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="2c3b8-179">Olá toofix hierarquia imperfeita, definindo propriedade de membros de ocultar Olá</span><span class="sxs-lookup"><span data-stu-id="2c3b8-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="2c3b8-180">Em **Gerenciador de Modelos tabulares**, expanda **Tabelas** > **DimEmployee** > **Hierarquias** > **Organização**.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="2c3b8-181">Em **Propriedades** > **Ocultar Membros**, selecione **Ocultar membros em branco**.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="2c3b8-183">No Excel, atualize Olá tabela dinâmica.</span><span class="sxs-lookup"><span data-stu-id="2c3b8-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="2c3b8-185">Agora isso tem uma aparência muito melhor!</span><span class="sxs-lookup"><span data-stu-id="2c3b8-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="2c3b8-186">Consulte também</span><span class="sxs-lookup"><span data-stu-id="2c3b8-186">See Also</span></span>   
[<span data-ttu-id="2c3b8-187">Lição 9: criar hierarquias</span><span class="sxs-lookup"><span data-stu-id="2c3b8-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="2c3b8-188">Lição Suplementar – Segurança Dinâmica</span><span class="sxs-lookup"><span data-stu-id="2c3b8-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="2c3b8-189">Lição suplementar – linhas de detalhes</span><span class="sxs-lookup"><span data-stu-id="2c3b8-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  