---
title: "Lição 2 do tutorial do Azure Analysis Services: obter dados | Microsoft Docs"
description: Descreve como obter e importar dados no projeto de tutorial do Azure Analysis Services.
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
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: e77de4b9a74b528fa8a7ce86424fc14628b2cacc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-2-get-data"></a><span data-ttu-id="a5b17-103">Lição 2: obter dados</span><span class="sxs-lookup"><span data-stu-id="a5b17-103">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="a5b17-104">Nesta lição, você usa Obter Dados no SSDT para se conectar ao banco de dados de exemplo AdventureWorksDW2014, selecionar dados, visualizar e filtrar e, em seguida, importar para o seu espaço de trabalho de modelo.</span><span class="sxs-lookup"><span data-stu-id="a5b17-104">In this lesson, you use Get Data in SSDT to connect to the AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="a5b17-105">Pelo uso do Obter Dados, você pode importar dados de uma ampla variedade de fontes: Banco de Dados SQL do Azure, Oracle, Sybase, OData Feed, Teradata, arquivos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="a5b17-105">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="a5b17-106">Os dados também podem ser consultados usando uma expressão de fórmula Power Query M.</span><span class="sxs-lookup"><span data-stu-id="a5b17-106">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="a5b17-107">Tempo estimado para conclusão desta lição: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="a5b17-107">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="a5b17-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a5b17-108">Prerequisites</span></span>  
<span data-ttu-id="a5b17-109">Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem.</span><span class="sxs-lookup"><span data-stu-id="a5b17-109">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="a5b17-110">Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 1: criar um novo projeto de modelo tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="a5b17-110">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="a5b17-111">Criar uma conexão</span><span class="sxs-lookup"><span data-stu-id="a5b17-111">Create a connection</span></span>  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw2014-database"></a><span data-ttu-id="a5b17-112">Para criar uma conexão ao banco de dados AdventureWorksDW2014</span><span class="sxs-lookup"><span data-stu-id="a5b17-112">To create a connection to the AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="a5b17-113">No Gerenciador de Modelos tabulares, clique com o botão direito do mouse em **Fontes de Dados** > **Importar de Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-113">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="a5b17-114">Isso inicializa o Obter Dados, que orienta você pela conexão a uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="a5b17-114">This launches Get Data, which guides you through connecting to a data source.</span></span> <span data-ttu-id="a5b17-115">Se você não vir o Gerenciador de Modelos tabulares, no **Gerenciador de Soluções**, clique duas vezes em **Model.bim** para abrir o modelo no designer.</span><span class="sxs-lookup"><span data-stu-id="a5b17-115">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** to open the model in the designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="a5b17-117">Em Obter Dados, clique em **Banco de Dados** > **Banco de Dados do SQL Server** > **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-117">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="a5b17-118">Na caixa de diálogo **Banco de Dados do SQL Server**, em **Servidor**, digite o nome do servidor em que você instalou o banco de dados AdventureWorksDW2014 e, em seguida, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-118">In the **SQL Server Database** dialog, in **Server**, type the name of the server where you installed the AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="a5b17-119">Quando for solicitado que você insira as credenciais, você precisará especificar as credenciais que o Analysis Services usa para se conectar à fonte de dados ao importar e processar dados.</span><span class="sxs-lookup"><span data-stu-id="a5b17-119">When prompted to enter credentials, you need to specify the credentials Analysis Services uses to connect to the data source when importing and processing data.</span></span> <span data-ttu-id="a5b17-120">Em **Modo de Representação**, selecione **Representar Conta** e, em seguida, insira as credenciais e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-120">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="a5b17-121">É recomendável que você use uma conta em que a senha não expira.</span><span class="sxs-lookup"><span data-stu-id="a5b17-121">It's recommended you use an account where the password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="a5b17-123">Usar uma conta de usuário e senha do Windows fornece o método mais seguro de se conectar a uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="a5b17-123">Using a Windows user account and password provides the most secure method of connecting to a data source.</span></span>
  
5.  <span data-ttu-id="a5b17-124">No navegador, selecione o banco de dados **AdventureWorksDW2014** e, em seguida, clique em **OK**. Isso cria a conexão ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a5b17-124">In Navigator, select the **AdventureWorksDW2014** database, and then click **OK**.This creates the connection to the database.</span></span> 
  
6.  <span data-ttu-id="a5b17-125">No navegador, marque a caixa de seleção para as tabelas a seguir: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** e **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-125">In Navigator, select the check box for the following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="a5b17-127">Depois que você clicar em OK, o Editor de Consultas será aberto.</span><span class="sxs-lookup"><span data-stu-id="a5b17-127">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="a5b17-128">Na próxima seção, você selecionará somente os dados que deseja importar.</span><span class="sxs-lookup"><span data-stu-id="a5b17-128">In the next section, you select only the data you want to import.</span></span>

  
## <a name="filter-the-table-data"></a><span data-ttu-id="a5b17-129">Filtrar os dados da tabela</span><span class="sxs-lookup"><span data-stu-id="a5b17-129">Filter the table data</span></span>  
<span data-ttu-id="a5b17-130">As tabelas no banco de dados de exemplo AdventureWorksDW2014 têm dados que não precisam ser incluídos em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="a5b17-130">Tables in the AdventureWorksDW2014 sample database have data that isn't necessary to include in your model.</span></span> <span data-ttu-id="a5b17-131">Quando possível, é recomendável filtrar os dados desnecessários para economizar espaço na memória usado pelo modelo.</span><span class="sxs-lookup"><span data-stu-id="a5b17-131">When possible, you want to filter out unnecessary data to save in-memory space used by the model.</span></span> <span data-ttu-id="a5b17-132">Você filtrará algumas das colunas de tabelas para que elas não sejam importadas para o banco de dados do espaço de trabalho ou então para o modelo de banco de dados após ele ter sido implantado.</span><span class="sxs-lookup"><span data-stu-id="a5b17-132">You filter out some of the columns from tables so they're not imported into the workspace database, or the model database after it has been deployed.</span></span> 
  
#### <a name="to-filter-the-table-data-before-importing"></a><span data-ttu-id="a5b17-133">Para filtrar os dados da tabela antes de importar</span><span class="sxs-lookup"><span data-stu-id="a5b17-133">To filter the table data before importing</span></span>  
  
1.  <span data-ttu-id="a5b17-134">No Editor de Consultas, selecione a tabela **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-134">In Query Editor, select the **DimCustomer** table.</span></span> <span data-ttu-id="a5b17-135">Uma exibição da tabela DimCustomer na fonte de dados (seu banco de dados de exemplo AdventureWorksDWQ2014) é exibida.</span><span class="sxs-lookup"><span data-stu-id="a5b17-135">A view of the DimCustomer table at the datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="a5b17-136">Faça uma seleção múltipla (Ctrl + clique) de **SpanishEducation**, **FrenchEducation**, **SpanishOccupation** e **FrenchOccupation** e, em seguida, clique com o botão direito do mouse e clique em **Remover Colunas**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-136">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="a5b17-138">Como os valores dessas colunas não são pertinentes à análise de vendas pela Internet, não é necessário importá-las.</span><span class="sxs-lookup"><span data-stu-id="a5b17-138">Since the values for these columns are not relevant to Internet sales analysis, there is no need to import these columns.</span></span> <span data-ttu-id="a5b17-139">A eliminação das colunas desnecessárias torna seu modelo menor e mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="a5b17-139">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="a5b17-140">Filtre as tabelas restantes, removendo as seguintes colunas em cada tabela:</span><span class="sxs-lookup"><span data-stu-id="a5b17-140">Filter the remaining tables by removing the following columns in each table:</span></span>  
    
    <span data-ttu-id="a5b17-141">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="a5b17-141">**DimDate**</span></span>
    
      |<span data-ttu-id="a5b17-142">Coluna</span><span class="sxs-lookup"><span data-stu-id="a5b17-142">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="a5b17-143">DateKey</span><span class="sxs-lookup"><span data-stu-id="a5b17-143">DateKey</span></span>|  
      |<span data-ttu-id="a5b17-144">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a5b17-144">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="a5b17-145">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a5b17-145">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="a5b17-146">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-146">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="a5b17-147">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-147">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="a5b17-148">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="a5b17-148">**DimGeography**</span></span>
  
      |<span data-ttu-id="a5b17-149">Coluna</span><span class="sxs-lookup"><span data-stu-id="a5b17-149">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="a5b17-150">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-150">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="a5b17-151">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-151">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="a5b17-152">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="a5b17-152">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="a5b17-153">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="a5b17-153">**DimProduct**</span></span>
  
      |<span data-ttu-id="a5b17-154">Coluna</span><span class="sxs-lookup"><span data-stu-id="a5b17-154">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="a5b17-155">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-155">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="a5b17-156">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-156">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="a5b17-157">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="a5b17-157">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="a5b17-158">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="a5b17-158">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="a5b17-159">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="a5b17-159">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="a5b17-160">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="a5b17-160">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="a5b17-161">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="a5b17-161">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="a5b17-162">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="a5b17-162">**GermanDescription**</span></span>|  
      |<span data-ttu-id="a5b17-163">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="a5b17-163">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="a5b17-164">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="a5b17-164">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="a5b17-165">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="a5b17-165">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="a5b17-166">Coluna</span><span class="sxs-lookup"><span data-stu-id="a5b17-166">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="a5b17-167">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-167">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="a5b17-168">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-168">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="a5b17-169">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="a5b17-169">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="a5b17-170">Coluna</span><span class="sxs-lookup"><span data-stu-id="a5b17-170">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="a5b17-171">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-171">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="a5b17-172">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="a5b17-172">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="a5b17-173">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="a5b17-173">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="a5b17-174">Coluna</span><span class="sxs-lookup"><span data-stu-id="a5b17-174">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="a5b17-175">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="a5b17-175">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="a5b17-176">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="a5b17-176">**DueDateKey**</span></span>|  
      |<span data-ttu-id="a5b17-177">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="a5b17-177">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="a5b17-178"><a name="Import"></a>Importar os dados de colunas e tabelas selecionadas</span><span class="sxs-lookup"><span data-stu-id="a5b17-178"><a name="Import"></a>Import the selected tables and column data</span></span>  
<span data-ttu-id="a5b17-179">Agora que você visualizou e filtrou os dados desnecessários, você pode importar o restante dos dados que você deseja.</span><span class="sxs-lookup"><span data-stu-id="a5b17-179">Now that you've previewed and filtered out unnecessary data, you can import the rest of the data you do want.</span></span> <span data-ttu-id="a5b17-180">O assistente importa os dados da tabela juntamente com quaisquer relacionamentos entre tabelas.</span><span class="sxs-lookup"><span data-stu-id="a5b17-180">The wizard imports the table data along with any relationships between tables.</span></span> <span data-ttu-id="a5b17-181">As novas tabelas e colunas são criadas no modelo e dados que você filtrou não serão importados.</span><span class="sxs-lookup"><span data-stu-id="a5b17-181">New tables and columns are created in the model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a><span data-ttu-id="a5b17-182">Para importar os dados de colunas e tabelas selecionadas</span><span class="sxs-lookup"><span data-stu-id="a5b17-182">To import the selected tables and column data</span></span>  
  
1.  <span data-ttu-id="a5b17-183">Examine suas seleções.</span><span class="sxs-lookup"><span data-stu-id="a5b17-183">Review your selections.</span></span> <span data-ttu-id="a5b17-184">Se tudo estiver ok, clique em **Importar**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-184">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="a5b17-185">A caixa de diálogo Processamento de Dados mostra o status dos dados que estão sendo importados de sua fonte de dados para seu banco de dados do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a5b17-185">The Data Processing dialog shows the status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="a5b17-187">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="a5b17-187">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="a5b17-188">Salvar o projeto de modelo</span><span class="sxs-lookup"><span data-stu-id="a5b17-188">Save your model project</span></span>  
<span data-ttu-id="a5b17-189">É importante salvar frequentemente o projeto de modelo.</span><span class="sxs-lookup"><span data-stu-id="a5b17-189">It's important to frequently save your model project.</span></span>  
  
#### <a name="to-save-the-model-project"></a><span data-ttu-id="a5b17-190">Para salvar o projeto de modelo</span><span class="sxs-lookup"><span data-stu-id="a5b17-190">To save the model project</span></span>  
  
-   <span data-ttu-id="a5b17-191">Clique em **Arquivo** > **Salvar Tudo**.</span><span class="sxs-lookup"><span data-stu-id="a5b17-191">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="a5b17-192">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="a5b17-192">What's next?</span></span>
<span data-ttu-id="a5b17-193">[Lição 3: marcar como tabela de data](../tutorials/aas-lesson-3-mark-as-date-table.md).</span><span class="sxs-lookup"><span data-stu-id="a5b17-193">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
