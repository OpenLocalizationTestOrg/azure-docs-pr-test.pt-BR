---
<span data-ttu-id="105fb-101">título: aaa "lição do tutorial do Azure Analysis Services 10: criar partições | Descrição de Microsoft Docs": descreve como toocreate partições no projeto do tutorial hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="105fb-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="105fb-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="105fb-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="105fb-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="105fb-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="105fb-104">Lição 10: criar partições</span><span class="sxs-lookup"><span data-stu-id="105fb-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="105fb-105">Nesta lição, você pode criar tabelas tabelas FactInternetSales partições toodivide Olá em partes lógicas menores que podem ser processada (atualizadas) independentemente de outras partições.</span><span class="sxs-lookup"><span data-stu-id="105fb-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="105fb-106">Por padrão, cada tabela incluída em seu modelo tem uma partição, o que inclui todas as tabelas Olá colunas e linhas.</span><span class="sxs-lookup"><span data-stu-id="105fb-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="105fb-107">Para a tabela de FactInternetSales hello, queremos dados de saudação toodivide por ano; uma partição para cada um dos cinco anos da tabela hello.</span><span class="sxs-lookup"><span data-stu-id="105fb-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="105fb-108">Cada partição pode ser então processada independentemente.</span><span class="sxs-lookup"><span data-stu-id="105fb-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="105fb-109">mais, consulte toolearn [partições](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="105fb-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="105fb-110">Estimado tempo toocomplete nesta lição: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="105fb-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="105fb-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="105fb-111">Prerequisites</span></span>  
<span data-ttu-id="105fb-112">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="105fb-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="105fb-113">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 9: criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="105fb-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="105fb-114">Criar partições</span><span class="sxs-lookup"><span data-stu-id="105fb-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="105fb-115">toocreate partições na tabela de FactInternetSales Olá</span><span class="sxs-lookup"><span data-stu-id="105fb-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="105fb-116">No Gerenciador de Modelos tabular, expanda **Tabelas** e, em seguida, clique com o botão direito do mouse em **FactInternetSales** > **Partições**.</span><span class="sxs-lookup"><span data-stu-id="105fb-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="105fb-117">No Gerenciador de partições, clique em **cópia**e, em seguida, altere o nome de saudação muito**FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="105fb-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="105fb-118">Porque você quer Olá partição tooinclude somente as linhas dentro de um determinado período, para o ano de saudação 2010, você deve modificar expressão de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="105fb-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="105fb-119">Clique em **Design** tooopen Editor de consultas e, em seguida, clique em Olá **FactInternetSales2010** consulta.</span><span class="sxs-lookup"><span data-stu-id="105fb-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="105fb-120">Na visualização, clique em Olá seta em Olá **OrderDate** título de coluna e clique **filtros de data/hora** > **entre**.</span><span class="sxs-lookup"><span data-stu-id="105fb-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="105fb-122">Na caixa de diálogo Filtrar linhas hello, em **Mostrar linhas onde: OrderDate**, deixe **é depois ou igual a**e, em seguida, no campo de data hello, digite **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="105fb-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="105fb-123">Deixe Olá **e** operador selecionado, selecione **é antes**, no campo de data hello, digite **1/1/2011**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="105fb-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="105fb-125">Observe que, no Editor de Consultas, em ETAPAS APLICADAS, você verá outra etapa chamada Linhas Filtradas.</span><span class="sxs-lookup"><span data-stu-id="105fb-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="105fb-126">Esse filtro é tooselect somente datas de pedido de 2010.</span><span class="sxs-lookup"><span data-stu-id="105fb-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="105fb-127">Clique em **Importar**.</span><span class="sxs-lookup"><span data-stu-id="105fb-127">Click **Import**.</span></span>

    <span data-ttu-id="105fb-128">No Gerenciador de partições, observe a consulta Olá expressão agora tem uma cláusula filtrada linhas adicional.</span><span class="sxs-lookup"><span data-stu-id="105fb-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="105fb-130">Essa instrução Especifica que essa partição deve incluir somente os dados Olá dessas linhas onde Olá OrderDate está Olá ano 2010 conforme especificado na cláusula de linhas filtradas hello.</span><span class="sxs-lookup"><span data-stu-id="105fb-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="105fb-131">toocreate uma partição para Olá ano de 2011</span><span class="sxs-lookup"><span data-stu-id="105fb-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="105fb-132">Na lista de partições hello, clique em Olá **FactInternetSales2010** partição que você criou e, em seguida, clique em **cópia**.</span><span class="sxs-lookup"><span data-stu-id="105fb-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="105fb-133">Alterar o nome da partição Olá muito**FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="105fb-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="105fb-134">Não é necessário toouse toocreate do Editor de consultas uma nova cláusula de linhas filtradas.</span><span class="sxs-lookup"><span data-stu-id="105fb-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="105fb-135">Como você criou uma cópia da consulta Olá para 2010, você só precisa toodo é fazer uma pequena alteração na consulta de saudação de 2011.</span><span class="sxs-lookup"><span data-stu-id="105fb-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="105fb-136">Em **expressão de consulta**, em ordem para essa partição tooinclude somente as linhas de saudação ano de 2011, substituir anos Olá na cláusula de linhas filtradas Olá com **2011** e **2012**, respectivamente, como:</span><span class="sxs-lookup"><span data-stu-id="105fb-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="105fb-137">partições de toocreate de 2012, 2013 e 2014.</span><span class="sxs-lookup"><span data-stu-id="105fb-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="105fb-138">Execute as etapas anteriores de hello, criando partições para 2012 2013 e 2014, alterando anos Olá Olá linhas filtradas cláusula tooinclude somente as linhas daquele ano.</span><span class="sxs-lookup"><span data-stu-id="105fb-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="105fb-139">Excluir Olá FactInternetSales partição</span><span class="sxs-lookup"><span data-stu-id="105fb-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="105fb-140">Agora que você tiver partições para cada ano, você pode excluir a partição de FactInternetSales Olá; impedindo a sobreposição ao escolher o processo de todos os durante o processamento de partições.</span><span class="sxs-lookup"><span data-stu-id="105fb-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="105fb-141">Olá toodelete FactInternetSales partição</span><span class="sxs-lookup"><span data-stu-id="105fb-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="105fb-142">Clique em Olá FactInternetSales partição e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="105fb-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="105fb-143">Processar partições</span><span class="sxs-lookup"><span data-stu-id="105fb-143">Process partitions</span></span>  
<span data-ttu-id="105fb-144">No Gerenciador de partições, observe Olá **último processados** coluna para cada uma das novas partições de saudação criado mostra essas partições nunca tiveram sido processadas.</span><span class="sxs-lookup"><span data-stu-id="105fb-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="105fb-145">Quando você criar partições, você deve executar um processar partições ou processar tabela operação toorefresh Olá dados nessas partições.</span><span class="sxs-lookup"><span data-stu-id="105fb-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="105fb-146">tooprocess Olá FactInternetSales partições</span><span class="sxs-lookup"><span data-stu-id="105fb-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="105fb-147">Clique em **Okey** tooclose Gerenciador de partições.</span><span class="sxs-lookup"><span data-stu-id="105fb-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="105fb-148">Clique em Olá **FactInternetSales** de tabela, clique em Olá **modelo** menu > **processo** > **processar partições**.</span><span class="sxs-lookup"><span data-stu-id="105fb-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="105fb-149">Na caixa de diálogo processar partições hello, verifique se **modo** está definido muito**processar padrão**.</span><span class="sxs-lookup"><span data-stu-id="105fb-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="105fb-150">Marque a caixa de seleção de saudação em Olá **processo** coluna para cada Olá cinco partições criadas e depois clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="105fb-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="105fb-152">Se você for solicitado a fornecer credenciais de representação, insira o nome de usuário do Windows hello e a senha que você especificou na lição 2.</span><span class="sxs-lookup"><span data-stu-id="105fb-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="105fb-153">Olá **processamento de dados** caixa de diálogo aparece e exibe os detalhes do processo para cada partição.</span><span class="sxs-lookup"><span data-stu-id="105fb-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="105fb-154">Observe que um número diferente de linhas é transferido para cada partição.</span><span class="sxs-lookup"><span data-stu-id="105fb-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="105fb-155">Cada partição inclui somente as linhas para ano Olá especificado na cláusula WHERE na instrução SQL de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="105fb-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="105fb-156">Quando o processamento é concluído, vá em frente e fechar a caixa de diálogo de processamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="105fb-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="105fb-158">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="105fb-158">What's next?</span></span>
<span data-ttu-id="105fb-159">Vá toohello próxima lição: [lição 11: criar funções](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="105fb-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
