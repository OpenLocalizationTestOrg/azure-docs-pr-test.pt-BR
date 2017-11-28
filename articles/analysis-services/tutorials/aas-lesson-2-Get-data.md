---
<span data-ttu-id="99958-101">título: aaa "lição do tutorial do Azure Analysis Services 2: obter dados | Descrição de Microsoft Docs": descreve como tooget e importar dados em Olá projeto do tutorial do Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="99958-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="99958-102">serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '</span><span class="sxs-lookup"><span data-stu-id="99958-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="99958-103">MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 01/06/2017 Author: owend</span><span class="sxs-lookup"><span data-stu-id="99958-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="99958-104">Lição 2: obter dados</span><span class="sxs-lookup"><span data-stu-id="99958-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="99958-105">Nesta lição, você usa obter dados no banco de dados de exemplo do tooconnect toohello AdventureWorksDW2014 SSDT, selecione os dados, visualizar e filtrar e, em seguida, importa para seu espaço de trabalho do modelo.</span><span class="sxs-lookup"><span data-stu-id="99958-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="99958-106">Pelo uso do Obter Dados, você pode importar dados de uma ampla variedade de fontes: Banco de Dados SQL do Azure, Oracle, Sybase, OData Feed, Teradata, arquivos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="99958-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="99958-107">Os dados também podem ser consultados usando uma expressão de fórmula Power Query M.</span><span class="sxs-lookup"><span data-stu-id="99958-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="99958-108">Estimado tempo toocomplete nesta lição: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="99958-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="99958-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="99958-109">Prerequisites</span></span>  
<span data-ttu-id="99958-110">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="99958-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="99958-111">Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 1: criar um novo projeto de modelo de tabela](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="99958-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="99958-112">Criar uma conexão</span><span class="sxs-lookup"><span data-stu-id="99958-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="99958-113">toocreate um banco de dados de toohello AdventureWorksDW2014 de conexão</span><span class="sxs-lookup"><span data-stu-id="99958-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="99958-114">No Gerenciador de Modelos tabulares, clique com o botão direito do mouse em **Fontes de Dados** > **Importar de Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="99958-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="99958-115">Obter dados, que guiará você por meio da fonte de dados tooa conexão é iniciado.</span><span class="sxs-lookup"><span data-stu-id="99958-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="99958-116">Se você não vir o Gerenciador de modelos de tabela, em **Solution Explorer**, clique duas vezes em **Model.bim** tooopen modelo de saudação no designer de saudação.</span><span class="sxs-lookup"><span data-stu-id="99958-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="99958-118">Em Obter Dados, clique em **Banco de Dados** > **Banco de Dados do SQL Server** > **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="99958-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="99958-119">Em Olá **o banco de dados do SQL Server** caixa de diálogo, na **servidor**, digite o nome de saudação do servidor de saudação onde você instalou o banco de dados de saudação AdventureWorksDW2014 e, em seguida, clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="99958-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="99958-120">Quando solicitado tooenter credenciais, você precisa ter credenciais de saudação toospecify tooconnect toohello fonte de dados ao importar e processar dados do Analysis Services usa.</span><span class="sxs-lookup"><span data-stu-id="99958-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="99958-121">Em **Modo de Representação**, selecione **Representar Conta** e, em seguida, insira as credenciais e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="99958-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="99958-122">É recomendável que usar uma conta em que as senhas de saudação não expiram.</span><span class="sxs-lookup"><span data-stu-id="99958-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="99958-124">Usar uma conta de usuário do Windows e senha fornece o método mais seguro hello conexão tooa da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="99958-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="99958-125">No navegador, selecione Olá **AdventureWorksDW2014** banco de dados e, em seguida, clique em **Okey**. Isso cria o banco de dados do hello conexão toohello.</span><span class="sxs-lookup"><span data-stu-id="99958-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="99958-126">No navegador, selecione Olá a caixa de seleção para Olá tabelas a seguir: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="99958-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="99958-128">Depois que você clicar em OK, o Editor de Consultas será aberto.</span><span class="sxs-lookup"><span data-stu-id="99958-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="99958-129">Na próxima seção, Olá, você seleciona somente os dados de saudação tooimport desejado.</span><span class="sxs-lookup"><span data-stu-id="99958-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="99958-130">Filtrar dados da tabela Olá</span><span class="sxs-lookup"><span data-stu-id="99958-130">Filter hello table data</span></span>  
<span data-ttu-id="99958-131">Tabelas no banco de dados do exemplo hello AdventureWorksDW2014 tem dados que não seja necessário tooinclude em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="99958-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="99958-132">Quando possível, você deseja toofilter espaço de na memória toosave desnecessária de dados usado pelo modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="99958-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="99958-133">Você filtrará algumas das Olá colunas de tabelas para não importação para o banco de dados de espaço de trabalho de saudação ou banco de dados de modelo Olá após ele ter sido implantado.</span><span class="sxs-lookup"><span data-stu-id="99958-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="99958-134">dados da tabela toofilter Olá antes de importar</span><span class="sxs-lookup"><span data-stu-id="99958-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="99958-135">No Editor de consultas, selecione Olá **DimCustomer** tabela.</span><span class="sxs-lookup"><span data-stu-id="99958-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="99958-136">Uma exibição de tabela DimCustomer Olá Olá datasource (seus dados de exemplo AdventureWorksDWQ2014) é exibida.</span><span class="sxs-lookup"><span data-stu-id="99958-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="99958-137">Faça uma seleção múltipla (Ctrl + clique) de **SpanishEducation**, **FrenchEducation**, **SpanishOccupation** e **FrenchOccupation** e, em seguida, clique com o botão direito do mouse e clique em **Remover Colunas**.</span><span class="sxs-lookup"><span data-stu-id="99958-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="99958-139">Como valores de saudação para essas colunas não são relevantes tooInternet análise de vendas, há tooimport sem necessidade dessas colunas.</span><span class="sxs-lookup"><span data-stu-id="99958-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="99958-140">A eliminação das colunas desnecessárias torna seu modelo menor e mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="99958-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="99958-141">Filtre Olá restantes tabelas removendo Olá colunas em cada tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="99958-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="99958-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="99958-142">**DimDate**</span></span>
    
      |<span data-ttu-id="99958-143">Coluna</span><span class="sxs-lookup"><span data-stu-id="99958-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="99958-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="99958-144">DateKey</span></span>|  
      |<span data-ttu-id="99958-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="99958-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="99958-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="99958-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="99958-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="99958-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="99958-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="99958-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="99958-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="99958-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="99958-150">Coluna</span><span class="sxs-lookup"><span data-stu-id="99958-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="99958-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="99958-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="99958-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="99958-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="99958-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="99958-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="99958-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="99958-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="99958-155">Coluna</span><span class="sxs-lookup"><span data-stu-id="99958-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="99958-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="99958-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="99958-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="99958-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="99958-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="99958-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="99958-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="99958-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="99958-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="99958-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="99958-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="99958-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="99958-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="99958-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="99958-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="99958-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="99958-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="99958-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="99958-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="99958-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="99958-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="99958-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="99958-167">Coluna</span><span class="sxs-lookup"><span data-stu-id="99958-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="99958-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="99958-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="99958-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="99958-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="99958-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="99958-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="99958-171">Coluna</span><span class="sxs-lookup"><span data-stu-id="99958-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="99958-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="99958-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="99958-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="99958-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="99958-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="99958-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="99958-175">Coluna</span><span class="sxs-lookup"><span data-stu-id="99958-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="99958-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="99958-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="99958-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="99958-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="99958-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="99958-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="99958-179"><a name="Import"></a>Saudação de importação selecionar tabelas e os dados da coluna</span><span class="sxs-lookup"><span data-stu-id="99958-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="99958-180">Agora que você visualizou e filtrou os dados desnecessários, você pode importar restante Olá Olá dados.</span><span class="sxs-lookup"><span data-stu-id="99958-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="99958-181">Assistente de saudação importa dados da tabela Olá junto com as relações entre tabelas.</span><span class="sxs-lookup"><span data-stu-id="99958-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="99958-182">Novas tabelas e colunas são criadas no modelo de saudação e não é possível importar dados que você filtrou.</span><span class="sxs-lookup"><span data-stu-id="99958-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="99958-183">Olá tooimport selecionar tabelas e os dados da coluna</span><span class="sxs-lookup"><span data-stu-id="99958-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="99958-184">Examine suas seleções.</span><span class="sxs-lookup"><span data-stu-id="99958-184">Review your selections.</span></span> <span data-ttu-id="99958-185">Se tudo estiver ok, clique em **Importar**.</span><span class="sxs-lookup"><span data-stu-id="99958-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="99958-186">caixa de diálogo de processamento de dados Olá mostra o status de saudação de dados sendo importados de sua fonte de dados para seu banco de dados do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="99958-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="99958-188">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="99958-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="99958-189">Salvar o projeto de modelo</span><span class="sxs-lookup"><span data-stu-id="99958-189">Save your model project</span></span>  
<span data-ttu-id="99958-190">É importante toofrequently salvar seu projeto de modelo.</span><span class="sxs-lookup"><span data-stu-id="99958-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="99958-191">projeto de modelo de saudação toosave</span><span class="sxs-lookup"><span data-stu-id="99958-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="99958-192">Clique em **Arquivo** > **Salvar Tudo**.</span><span class="sxs-lookup"><span data-stu-id="99958-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="99958-193">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="99958-193">What's next?</span></span>
<span data-ttu-id="99958-194">[Lição 3: marcar como tabela de data](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="99958-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
