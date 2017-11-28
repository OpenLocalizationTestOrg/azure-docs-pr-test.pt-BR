---
title: Carregar dados do SQL Server no SQL Data Warehouse do Azure (SSIS) | Microsoft Docs
description: "Mostra a você como criar um pacote do SSIS (SQL Server Integration Services) para mover dados de uma ampla variedade de fontes de dados para o SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: 6c9cebdd715b6997d0633bc725a3945ba9e0c357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a><span data-ttu-id="f6ba5-103">Carregar dados do SQL Server no Azure SQL Data Warehouse (SSIS)</span><span class="sxs-lookup"><span data-stu-id="f6ba5-103">Load data from SQL Server into Azure SQL Data Warehouse (SSIS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6ba5-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="f6ba5-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="f6ba5-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="f6ba5-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="f6ba5-106">bcp</span><span class="sxs-lookup"><span data-stu-id="f6ba5-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="f6ba5-107">Crie um pacote SSIS (SQL Server Integration Services) para carregar dados do SQL Server no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-107">Create a SQL Server Integration Services (SSIS) package to load data from SQL Server into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f6ba5-108">Opcionalmente, você pode reestruturar, transformar e limpar os dados conforme eles passam pelo fluxo de dados do SSIS.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-108">You can optionally restructure, transform, and cleanse the data as it passes through the SSIS data flow.</span></span>

<span data-ttu-id="f6ba5-109">Neste tutorial, você irá:</span><span class="sxs-lookup"><span data-stu-id="f6ba5-109">In this tutorial, you will:</span></span>

* <span data-ttu-id="f6ba5-110">Criar um novo projeto do Integration Services no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-110">Create a new Integration Services project in Visual Studio.</span></span>
* <span data-ttu-id="f6ba5-111">Conectar-se a fontes de dados, incluindo SQL Server (como uma fonte) e o SQL Data Warehouse (como um destino).</span><span class="sxs-lookup"><span data-stu-id="f6ba5-111">Connect to data sources, including SQL Server (as a source) and SQL Data Warehouse (as a destination).</span></span>
* <span data-ttu-id="f6ba5-112">Criar um pacote do SSIS que carregue os dados da fonte para o destino.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-112">Design an SSIS package that loads data from the source into the destination.</span></span>
* <span data-ttu-id="f6ba5-113">Executar o pacote do SSIS para carregar os dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-113">Run the SSIS package to load the data.</span></span>

<span data-ttu-id="f6ba5-114">Este tutorial usa o SQL Server como a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-114">This tutorial uses SQL Server as the data source.</span></span> <span data-ttu-id="f6ba5-115">O SQL Server pode estar em execução local ou em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-115">SQL Server could be running on premises or in an Azure virtual machine.</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="f6ba5-116">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="f6ba5-116">Basic concepts</span></span>
<span data-ttu-id="f6ba5-117">O pacote é a unidade de trabalho no SSIS.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-117">The package is the unit of work in SSIS.</span></span> <span data-ttu-id="f6ba5-118">Os pacotes relacionados são agrupados em projetos.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-118">Related packages are grouped in projects.</span></span> <span data-ttu-id="f6ba5-119">Você cria projetos e pacotes de design no Visual Studio com o SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-119">You create projects and design packages in Visual Studio with SQL Server Data Tools.</span></span> <span data-ttu-id="f6ba5-120">O processo de design é um processo visual no qual você arrasta e solta componentes da Caixa de Ferramentas para a superfície de design, conecta-os e define suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-120">The design process is a visual process in which you drag and drop components from the Toolbox to the design surface, connect them, and set their properties.</span></span> <span data-ttu-id="f6ba5-121">Depois de concluir seu pacote, você pode, opcionalmente, implantá-lo no SQL Server para gerenciamento, monitoramento e segurança abrangentes.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-121">After you finish your package, you can optionally deploy it to SQL Server for comprehensive management, monitoring, and security.</span></span>

## <a name="options-for-loading-data-with-ssis"></a><span data-ttu-id="f6ba5-122">Opções de carregamento de dados com o SSIS</span><span class="sxs-lookup"><span data-stu-id="f6ba5-122">Options for loading data with SSIS</span></span>
<span data-ttu-id="f6ba5-123">O SSIS (SQL Server Integration Services) é um conjunto flexível de ferramentas que fornece uma variedade de opções para se conectar a e carregar dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-123">SQL Server Integration Services (SSIS) is a flexible set of tools that provides a variety of options for connecting to, and loading data into, SQL Data Warehouse.</span></span>

1. <span data-ttu-id="f6ba5-124">Use um destino do ADO NET para conectar-se ao SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-124">Use an ADO NET Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="f6ba5-125">Este tutorial usa um Destino do ADO NET porque ele é o que tem o menor número de opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-125">This tutorial uses an ADO NET Destination because it has the fewest configuration options.</span></span>
2. <span data-ttu-id="f6ba5-126">Use um Destino OLE DB para conectar-se ao SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-126">Use an OLE DB Destination to connect to SQL Data Warehouse.</span></span> <span data-ttu-id="f6ba5-127">Esta opção pode fornecer desempenho um pouco melhor do que o Destino ADO NET.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-127">This option may provide slightly better performance than the ADO NET Destination.</span></span>
3. <span data-ttu-id="f6ba5-128">Use a Tarefa de Upload de Blob do Azure para preparar os dados no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-128">Use the Azure Blob Upload Task to stage the data in Azure Blob Storage.</span></span> <span data-ttu-id="f6ba5-129">Em seguida, use a tarefa Executar SQL do SSIS para iniciar um script do Polybase que carrega os dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-129">Then use the SSIS Execute SQL task to launch a Polybase script that loads the data into SQL Data Warehouse.</span></span> <span data-ttu-id="f6ba5-130">Essa opção oferece o melhor desempenho das três opções listadas aqui.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-130">This option provides the best performance of the three options listed here.</span></span> <span data-ttu-id="f6ba5-131">Para obter a Tarefa de Upload de Blobs do Azure, baixe o [Feature Pack do Microsoft SQL Server 2016 Integration Services para o Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-131">To get the Azure Blob Upload task, download the [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure].</span></span> <span data-ttu-id="f6ba5-132">Para saber mais sobre o Polybase, consulte o [Guia do PolyBase][PolyBase Guide].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-132">To learn more about Polybase, see [PolyBase Guide][PolyBase Guide].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f6ba5-133">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f6ba5-133">Before you start</span></span>
<span data-ttu-id="f6ba5-134">Para acompanhar este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="f6ba5-134">To step through this tutorial, you need:</span></span>

1. <span data-ttu-id="f6ba5-135">**SSIS (SQL Server Integration Services)**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-135">**SQL Server Integration Services (SSIS)**.</span></span> <span data-ttu-id="f6ba5-136">O SSIS é um componente do SQL Server e requer uma versão de avaliação ou uma versão licenciada do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-136">SSIS is a component of SQL Server and requires an evaluation version or a licensed version of SQL Server.</span></span> <span data-ttu-id="f6ba5-137">Para obter uma versão de avaliação da Visualização do SQL Server 2016, consulte [Avaliações do SQL Server][SQL Server Evaluations].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-137">To get an evaluation version of SQL Server 2016 Preview, see [SQL Server Evaluations][SQL Server Evaluations].</span></span>
2. <span data-ttu-id="f6ba5-138">**Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-138">**Visual Studio**.</span></span> <span data-ttu-id="f6ba5-139">Para obter o Visual Studio Community Edition gratuito, consulte [Visual Studio Community][Visual Studio Community].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-139">To get the free Visual Studio Community Edition, see [Visual Studio Community][Visual Studio Community].</span></span>
3. <span data-ttu-id="f6ba5-140">**SSDT (SQL Server Data Tools) para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-140">**SQL Server Data Tools for Visual Studio (SSDT)**.</span></span> <span data-ttu-id="f6ba5-141">Para obter o SQL Server Data Tools para Visual Studio, consulte [Baixar o SSDT (SQL Server Data Tools)][Download SQL Server Data Tools (SSDT)].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-141">To get SQL Server Data Tools for Visual Studio, see [Download SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].</span></span>
4. <span data-ttu-id="f6ba5-142">**Dados de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-142">**Sample data**.</span></span> <span data-ttu-id="f6ba5-143">Este tutorial usa dados de exemplo armazenados no SQL Server no banco de dados de exemplo do AdventureWorks como os dados de origem a serem carregados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-143">This tutorial uses sample data stored in SQL Server in the AdventureWorks sample database as the source data to be loaded into SQL Data Warehouse.</span></span> <span data-ttu-id="f6ba5-144">Para obter o banco de dados de exemplo do AdventureWorks, consulte [Bancos de Dados de Exemplo do AdventureWorks 2014][AdventureWorks 2014 Sample Databases].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-144">To get the AdventureWorks sample database, see [AdventureWorks 2014 Sample Databases][AdventureWorks 2014 Sample Databases].</span></span>
5. <span data-ttu-id="f6ba5-145">**Um banco de dados e permissões do SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-145">**A SQL Data Warehouse database and permissions**.</span></span> <span data-ttu-id="f6ba5-146">Este tutorial conecta-se a uma instância do SQL Data Warehouse e carrega dados nela.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-146">This tutorial connects to a SQL Data Warehouse instance and loads data into it.</span></span> <span data-ttu-id="f6ba5-147">Você precisa ter permissões para criar uma tabela e para carregar dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-147">You have to have permissions to create a table and to load data.</span></span>
6. <span data-ttu-id="f6ba5-148">**Uma regra de firewall**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-148">**A firewall rule**.</span></span> <span data-ttu-id="f6ba5-149">Antes que você possa carregar dados no SQL Data Warehouse, você precisará criar uma regra de firewall no SQL Data Warehouse com o endereço IP do computador local.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-149">You have to create a firewall rule on SQL Data Warehouse with the IP address of your local computer before you can upload data to the SQL Data Warehouse.</span></span>

## <a name="step-1-create-a-new-integration-services-project"></a><span data-ttu-id="f6ba5-150">Etapa 1: Criar um novo projeto do Integration Services</span><span class="sxs-lookup"><span data-stu-id="f6ba5-150">Step 1: Create a new Integration Services project</span></span>
1. <span data-ttu-id="f6ba5-151">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-151">Launch Visual Studio.</span></span>
2. <span data-ttu-id="f6ba5-152">No menu **Arquivo**, selecione **Novo | Projeto**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-152">On the **File** menu, select **New | Project**.</span></span>
3. <span data-ttu-id="f6ba5-153">Navegue até os tipos de projeto **Instalado | Modelos | Business Intelligence | Integration Services** .</span><span class="sxs-lookup"><span data-stu-id="f6ba5-153">Navigate to the **Installed | Templates | Business Intelligence | Integration Services** project types.</span></span>
4. <span data-ttu-id="f6ba5-154">Selecione **Projeto do Integration Services**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-154">Select **Integration Services Project**.</span></span> <span data-ttu-id="f6ba5-155">Forneça valores para **Nome** e **Local** e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-155">Provide values for **Name** and **Location**, and then select **OK**.</span></span>

<span data-ttu-id="f6ba5-156">O Visual Studio abre e cria um novo projeto do SSIS (Integration Services).</span><span class="sxs-lookup"><span data-stu-id="f6ba5-156">Visual Studio opens and creates a new Integration Services (SSIS) project.</span></span> <span data-ttu-id="f6ba5-157">Em seguida, o Visual Studio abre o designer para o único novo pacote SSIS (Package.dtsx) no projeto.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-157">Then Visual Studio opens the designer for the single new SSIS package (Package.dtsx) in the project.</span></span> <span data-ttu-id="f6ba5-158">Você vê as seguintes áreas de tela:</span><span class="sxs-lookup"><span data-stu-id="f6ba5-158">You see the following screen areas:</span></span>

* <span data-ttu-id="f6ba5-159">À esquerda, a **Caixa de Ferramentas** dos componentes do SSIS.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-159">On the left, the **Toolbox** of SSIS components.</span></span>
* <span data-ttu-id="f6ba5-160">No meio, a superfície de design, com várias guias.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-160">In the middle, the design surface, with multiple tabs.</span></span> <span data-ttu-id="f6ba5-161">Normalmente, você usa pelo menos as guias **Fluxo de Controle** e **Fluxo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-161">You typically use at least the **Control Flow** and the **Data Flow** tabs.</span></span>
* <span data-ttu-id="f6ba5-162">À direita, os painéis **Gerenciador de Soluções** e **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-162">On the right, the **Solution Explorer** and the **Properties** panes.</span></span>
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a><span data-ttu-id="f6ba5-163">Etapa 2: Criar o fluxo de dados básico</span><span class="sxs-lookup"><span data-stu-id="f6ba5-163">Step 2: Create the basic data flow</span></span>
1. <span data-ttu-id="f6ba5-164">Arraste uma Tarefa de Fluxo de Dados da Caixa de Ferramentas para o centro da superfície de design (na guia **Fluxo de Controle** ).</span><span class="sxs-lookup"><span data-stu-id="f6ba5-164">Drag a Data Flow Task from the Toolbox to the center of the design surface (on the **Control Flow** tab).</span></span>
   
    ![][02]
2. <span data-ttu-id="f6ba5-165">Clique duas vezes na Tarefa de Fluxo de Dados para alternar para a guia Fluxo de Dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-165">Double-click the Data Flow Task to switch to the Data Flow tab.</span></span>
3. <span data-ttu-id="f6ba5-166">Na lista Outras Fontes na Caixa de Ferramentas, arraste uma Fonte do ADO.NET para a superfície de design.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-166">From the Other Sources list in the Toolbox, drag an ADO.NET Source to the design surface.</span></span> <span data-ttu-id="f6ba5-167">Com o adaptador de fonte ainda selecionado, altere seu nome para **Fonte do SQL Server** no painel **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-167">With the source adapter still selected, change its name to **SQL Server source** in the **Properties** pane.</span></span>
4. <span data-ttu-id="f6ba5-168">Na lista Outros Destinos na caixa de ferramentas, arraste um Destino ADO.NET para a superfície de design na Fonte do ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-168">From the Other Destinations list in the Toolbox, drag an ADO.NET Destination to the design surface under the ADO.NET Source.</span></span> <span data-ttu-id="f6ba5-169">Com o adaptador de destino ainda selecionado, altere seu nome para **Destino do SQL DW** no painel **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-169">With the destination adapter still selected, change its name to **SQL DW destination** in the **Properties** pane.</span></span>
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a><span data-ttu-id="f6ba5-170">Etapa 3: Configurar o adaptador de fonte</span><span class="sxs-lookup"><span data-stu-id="f6ba5-170">Step 3: Configure the source adapter</span></span>
1. <span data-ttu-id="f6ba5-171">Clique duas vezes no adaptador de fonte para abrir o **Editor de Fonte do ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-171">Double-click the source adapter to open the **ADO.NET Source Editor**.</span></span>
   
    ![][03]
2. <span data-ttu-id="f6ba5-172">Na guia **Gerenciador de Conexões** do **Editor de Fonte do ADO.NET**, clique no botão **Novo** ao lado da lista **Gerenciador de conexões ADO.NET** para abrir a caixa de diálogo **Configurar Gerenciador de Conexões do ADO.NET** e crie as configurações de conexão para o banco de dados do SQL Server do qual este tutorial carrega os dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-172">On the **Connection Manager** tab of the **ADO.NET Source Editor**, click the **New** button next to the **ADO.NET connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the SQL Server database from which this tutorial loads data.</span></span>
   
    ![][04]
3. <span data-ttu-id="f6ba5-173">Na caixa de diálogo **Configurar Gerenciador de Conexões do ADO.NET**, clique no botão **Novo** para abrir a caixa de diálogo **Gerenciador de Conexões** e criar uma nova conexão de dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-173">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
   
    ![][05]
4. <span data-ttu-id="f6ba5-174">Na caixa de diálogo **Gerenciador de Conexões** , realize as ações descritas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-174">In the **Connection Manager** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="f6ba5-175">Para **Provedor**, selecione o Provedor de Dados SqlClient.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-175">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="f6ba5-176">Para **Nome do servidor**, insira o nome do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-176">For **Server name**, enter the SQL Server name.</span></span>
   3. <span data-ttu-id="f6ba5-177">Na seção **Fazer logon no servidor** , selecione ou insira as informações de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-177">In the **Log on to the server** section, select or enter authentication information.</span></span>
   4. <span data-ttu-id="f6ba5-178">Na seção **Conectar-se a um banco de dados** , selecione o banco de dados de exemplo AdventureWorks.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-178">In the **Connect to a database** section, select the AdventureWorks sample database.</span></span>
   5. <span data-ttu-id="f6ba5-179">Clique em **Testar conexão**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-179">Click **Test Connection**.</span></span>
      
       ![][06]
   6. <span data-ttu-id="f6ba5-180">Na caixa de diálogo que relata os resultados do teste de conexão, clique em **OK** para retornar à caixa de diálogo **Gerenciador de Conexões**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-180">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="f6ba5-181">Na caixa de diálogo **Gerenciador de Conexões**, clique em **OK** para retornar à caixa de diálogo **Configurar Gerenciador de Conexões do ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-181">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="f6ba5-182">Na caixa de diálogo **Configurar Gerenciador de Conexões do ADO.NET**, clique em **OK** para retornar ao **Editor de Fonte do ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-182">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Source Editor**.</span></span>
6. <span data-ttu-id="f6ba5-183">No **Editor de Fonte do ADO.NET**, na lista **Nome da tabela ou exibição**, selecione a tabela **Sales.SalesOrderDetail**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-183">In the **ADO.NET Source Editor**, in the **Name of the table or the view** list, select the **Sales.SalesOrderDetail** table.</span></span>
   
    ![][07]
7. <span data-ttu-id="f6ba5-184">Clique em **Visualização** para ver as primeiras 200 linhas de dados na tabela de origem na caixa de diálogo **Visualizar Resultados da Consulta**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-184">Click **Preview** to see the first 200 rows of data in the source table in the **Preview Query Results** dialog box.</span></span>
   
    ![][08]
8. <span data-ttu-id="f6ba5-185">Na caixa de diálogo **Visualizar Resultados da Consulta**, clique em **Fechar** para retornar para o **Editor de Fonte do ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-185">In the **Preview Query Results** dialog box, click **Close** to return to the **ADO.NET Source Editor**.</span></span>
9. <span data-ttu-id="f6ba5-186">No **Editor de Fonte do ADO.NET**, clique em **OK** para concluir a configuração da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-186">In the **ADO.NET Source Editor**, click **OK** to finish configuring the data source.</span></span>

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a><span data-ttu-id="f6ba5-187">Etapa 4: Conectar o adaptador de fonte ao adaptador de destino</span><span class="sxs-lookup"><span data-stu-id="f6ba5-187">Step 4: Connect the source adapter to the destination adapter</span></span>
1. <span data-ttu-id="f6ba5-188">Selecione o adaptador de fonte na superfície de design.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-188">Select the source adapter on the design surface.</span></span>
2. <span data-ttu-id="f6ba5-189">Selecione a seta azul que se estende do adaptador de fonte e arraste-a para o editor de destino até que ela se encaixe.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-189">Select the blue arrow that extends from the source adapter and drag it to the destination editor until it snaps into place.</span></span>
   
    ![][10]
   
    <span data-ttu-id="f6ba5-190">Em um pacote SSIS típico, você pode usar um número de outros componentes da Caixa de Ferramentas do SSIS entre a fonte e o destino para reestruturar, transformar e limpar seus dados conforme eles passam pelo fluxo de dados do SSIS.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-190">In a typical SSIS package, you use a number of other components from the SSIS Toolbox in between the source and the destination to restructure, transform, and cleanse your data as it passes through the SSIS data flow.</span></span> <span data-ttu-id="f6ba5-191">Para manter esse exemplo o mais simples possível, estamos conectando a fonte diretamente ao destino.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-191">To keep this example as simple as possible, we’re connecting the source directly to the destination.</span></span>

## <a name="step-5-configure-the-destination-adapter"></a><span data-ttu-id="f6ba5-192">Etapa 5: Configurar o adaptador de destino</span><span class="sxs-lookup"><span data-stu-id="f6ba5-192">Step 5: Configure the destination adapter</span></span>
1. <span data-ttu-id="f6ba5-193">Clique duas vezes no adaptador de destino para abrir o **Editor de Destino do ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-193">Double-click the destination adapter to open the **ADO.NET Destination Editor**.</span></span>
   
    ![][11]
2. <span data-ttu-id="f6ba5-194">Na guia **Gerenciador de Conexões** do **Editor de Destino do ADO.NET**, clique no botão **Novo** ao lado da lista **Gerenciador de conexões** para abrir a caixa de diálogo **Configurar Gerenciador de Conexões do ADO.NET** e crie as configurações de conexão para o banco de dados do SQL Data Warehouse no qual este tutorial carrega os dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-194">On the **Connection Manager** tab of the **ADO.NET Destination Editor**, click the **New** button next to the **Connection manager** list to open the **Configure ADO.NET Connection Manager** dialog box and create connection settings for the Azure SQL Data Warehouse database into which this tutorial loads data.</span></span>
3. <span data-ttu-id="f6ba5-195">Na caixa de diálogo **Configurar Gerenciador de Conexões do ADO.NET**, clique no botão **Novo** para abrir a caixa de diálogo **Gerenciador de Conexões** e criar uma nova conexão de dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-195">In the **Configure ADO.NET Connection Manager** dialog box, click the **New** button to open the **Connection Manager** dialog box and create a new data connection.</span></span>
4. <span data-ttu-id="f6ba5-196">Na caixa de diálogo **Gerenciador de Conexões** , realize as ações descritas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-196">In the **Connection Manager** dialog box, do the following things.</span></span>
   1. <span data-ttu-id="f6ba5-197">Para **Provedor**, selecione o Provedor de Dados SqlClient.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-197">For **Provider**, select the SqlClient Data Provider.</span></span>
   2. <span data-ttu-id="f6ba5-198">Para **Nome do servidor**, digite o nome do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-198">For **Server name**, enter the SQL Data Warehouse name.</span></span>
   3. <span data-ttu-id="f6ba5-199">Na seção **Fazer logon no servidor**, selecione **Usar autenticação do SQL Server** e insira as informações de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-199">In the **Log on to the server** section, select **Use SQL Server authentication** and enter authentication information.</span></span>
   4. <span data-ttu-id="f6ba5-200">Na seção **Conectar-se a um banco de dados** , selecione um banco de dados do SQL Data Warehouse existente.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-200">In the **Connect to a database** section, select an existing SQL Data Warehouse database.</span></span>
   5. <span data-ttu-id="f6ba5-201">Clique em **Testar conexão**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-201">Click **Test Connection**.</span></span>
   6. <span data-ttu-id="f6ba5-202">Na caixa de diálogo que relata os resultados do teste de conexão, clique em **OK** para retornar à caixa de diálogo **Gerenciador de Conexões**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-202">In the dialog box that reports the results of the connection test, click **OK** to return to the **Connection Manager** dialog box.</span></span>
   7. <span data-ttu-id="f6ba5-203">Na caixa de diálogo **Gerenciador de Conexões**, clique em **OK** para retornar à caixa de diálogo **Configurar Gerenciador de Conexões do ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-203">In the **Connection Manager** dialog box, click **OK** to return to the **Configure ADO.NET Connection Manager** dialog box.</span></span>
5. <span data-ttu-id="f6ba5-204">Na caixa de diálogo **Configurar Gerenciador de Conexões do ADO.NET**, clique em **OK** para retornar ao **Editor de Destino do ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-204">In the **Configure ADO.NET Connection Manager** dialog box, click **OK** to return to the **ADO.NET Destination Editor**.</span></span>
6. <span data-ttu-id="f6ba5-205">No **Editor de Destino do ADO.NET**, clique em **Novo** ao lado da lista **Usar uma tabela ou exibição** para abrir a caixa de diálogo **Criar Tabela** para criar uma nova tabela de destino com uma lista de colunas que corresponde à tabela de origem.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-205">In the **ADO.NET Destination Editor**, click **New** next to the **Use a table or view** list to open the **Create Table** dialog box to create a new destination table with a column list that matches the source table.</span></span>
   
    ![][12a]
7. <span data-ttu-id="f6ba5-206">Na caixa de diálogo **Criar Tabela** , realize as ações a seguir.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-206">In the **Create Table** dialog box, do the following things.</span></span>
   
   1. <span data-ttu-id="f6ba5-207">Altere o nome da tabela de destino para **SalesOrderDetail**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-207">Change the name of the destination table to **SalesOrderDetail**.</span></span>
   2. <span data-ttu-id="f6ba5-208">Remova a coluna **rowguid** .</span><span class="sxs-lookup"><span data-stu-id="f6ba5-208">Remove the **rowguid** column.</span></span> <span data-ttu-id="f6ba5-209">Não há suporte para o tipo de dados **uniqueidentifier** no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-209">The **uniqueidentifier** data type is not supported in SQL Data Warehouse.</span></span>
   3. <span data-ttu-id="f6ba5-210">Altere o tipo de dados da coluna **LineTotal** para **money**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-210">Change the data type of the **LineTotal** column to **money**.</span></span> <span data-ttu-id="f6ba5-211">Não há suporte para o tipo de dados **decimal** no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-211">The **decimal** data type is not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="f6ba5-212">Para obter informações sobre tipos de dados com suporte, consulte [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-212">For info about supported data types, see [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].</span></span>
      
       ![][12b]
   4. <span data-ttu-id="f6ba5-213">Clique em **OK** para criar a tabela e retornar para o **Editor de Destino do ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-213">Click **OK** to create the table and return to the **ADO.NET Destination Editor**.</span></span>
8. <span data-ttu-id="f6ba5-214">No **Editor de Destino do ADO.NET**, selecione a guia **Mapeamentos** para ver como as colunas na origem são mapeadas para as colunas no destino.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-214">In the **ADO.NET Destination Editor**, select the **Mappings** tab to see how columns in the source are mapped to columns in the destination.</span></span>
   
    ![][13]
9. <span data-ttu-id="f6ba5-215">Clique em **OK** para concluir a configuração da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-215">Click **OK** to finish configuring the data source.</span></span>

## <a name="step-6-run-the-package-to-load-the-data"></a><span data-ttu-id="f6ba5-216">Etapa 6: Executar o pacote para carregar os dados</span><span class="sxs-lookup"><span data-stu-id="f6ba5-216">Step 6: Run the package to load the data</span></span>
<span data-ttu-id="f6ba5-217">Execute o pacote clicando no botão **Iniciar** na barra de ferramentas ou selecionando uma das opções **Executar** no menu **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-217">Run the package by clicking the **Start** button on the toolbar or by selecting one of the **Run** options on the **Debug** menu.</span></span>

<span data-ttu-id="f6ba5-218">O pacote começa a executar e você vê rodas amarelas girando para indicar atividade, bem como o número de linhas processadas até o momento.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-218">As the package begins to run, you see yellow spinning wheels to indicate activity as well as the number of rows processed so far.</span></span>

![][14]

<span data-ttu-id="f6ba5-219">Quando a execução do pacote for concluída, você verá marcas de seleção verdes para indicar êxito, bem como o número total de linhas de dados carregados da fonte para o destino.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-219">When the package has finished running, you see green check marks to indicate success as well as the total number of rows of data loaded from the source to the destination.</span></span>

![][15]

<span data-ttu-id="f6ba5-220">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="f6ba5-220">Congratulations!</span></span> <span data-ttu-id="f6ba5-221">Você usou com êxito o SQL Server Integration Services para carregar dados no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-221">You’ve successfully used SQL Server Integration Services to load data into Azure SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6ba5-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f6ba5-222">Next steps</span></span>
* <span data-ttu-id="f6ba5-223">Saiba mais sobre o fluxo de dados do SSIS.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-223">Learn more about the SSIS data flow.</span></span> <span data-ttu-id="f6ba5-224">Comece por aqui: [Fluxo de Dados][Data Flow].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-224">Start here: [Data Flow][Data Flow].</span></span>
* <span data-ttu-id="f6ba5-225">Saiba como depurar e solucionar problemas de seus pacotes direto do ambiente de design.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-225">Learn how to debug and troubleshoot your packages right in the design environment.</span></span> <span data-ttu-id="f6ba5-226">Comece por aqui: [Solução de problemas de ferramentas para o desenvolvimento de pacotes][Troubleshooting Tools for Package Development].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-226">Start here: [Troubleshooting Tools for Package Development][Troubleshooting Tools for Package Development].</span></span>
* <span data-ttu-id="f6ba5-227">Saiba como implantar seus pacotes e projetos do SSIS no servidor do Integration Services ou em outro local de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-227">Learn how to deploy your SSIS projects and packages to Integration Services Server or to another storage location.</span></span> <span data-ttu-id="f6ba5-228">Comece por aqui: [Implantação de projetos e pacotes][Deployment of Projects and Packages].</span><span class="sxs-lookup"><span data-stu-id="f6ba5-228">Start here: [Deployment of Projects and Packages][Deployment of Projects and Packages].</span></span>

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
