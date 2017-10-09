---
title: "depósito de dados do Azure aaaUse Redgate tooload dados tooyour | Microsoft Docs"
description: "Saiba como Studio do toouse Redgate de plataforma de dados para cenários de data warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="f28e4-103">Carregar dados com o Data Platform Studio da Redgate</span><span class="sxs-lookup"><span data-stu-id="f28e4-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f28e4-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="f28e4-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="f28e4-105">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="f28e4-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="f28e4-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="f28e4-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="f28e4-107">BCP</span><span class="sxs-lookup"><span data-stu-id="f28e4-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="f28e4-108">Este tutorial mostra como toouse [Studio de plataforma de dados do Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) dados de toomove (DPS) de um tooAzure do SQL Server local SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f28e4-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="f28e4-109">Studio da plataforma de dados aplica correções de compatibilidade mais apropriadas hello e otimizações, portanto, não tem mais rápido possível Olá maneira tooget iniciado com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f28e4-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="f28e4-110">[Redgate](http://www.red-gate.com) é um antigo parceiro da Microsoft que oferece várias ferramentas de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f28e4-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="f28e4-111">Esse recurso no Data Platform Studio ficou disponível gratuitamente para uso comercial e não comercial.</span><span class="sxs-lookup"><span data-stu-id="f28e4-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="f28e4-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f28e4-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="f28e4-113">Criar ou identificar recursos</span><span class="sxs-lookup"><span data-stu-id="f28e4-113">Create or identify resources</span></span>
<span data-ttu-id="f28e4-114">Antes de iniciar este tutorial, você precisará toohave:</span><span class="sxs-lookup"><span data-stu-id="f28e4-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="f28e4-115">**o banco de dados do SQL Server local**: Olá dados que você deseja tooimport tooSQL Data Warehouse precisa toocome de um SQL Server no local (versão 2008R2 ou superior).</span><span class="sxs-lookup"><span data-stu-id="f28e4-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="f28e4-116">Data Platform Studio não pode importar dados diretamente de um Banco de Dados SQL do Azure ou de arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="f28e4-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="f28e4-117">**Conta de armazenamento do Azure**: Studio da plataforma de dados prepara os dados de saudação no armazenamento de BLOBs do Azure antes de carregá-lo no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f28e4-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="f28e4-118">conta de armazenamento Olá deve estar usando o modelo de implantação do "Gerenciador de recursos" saudação (padrão de saudação) em vez do modelo de implantação "Clássico" hello.</span><span class="sxs-lookup"><span data-stu-id="f28e4-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="f28e4-119">Se você não tiver uma conta de armazenamento, saiba como tooCreate uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f28e4-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="f28e4-120">**SQL Data Warehouse**: neste tutorial move Olá dados do local do SQL Server tooSQL Data Warehouse, para que seja necessário toohave um data warehouse on-line.</span><span class="sxs-lookup"><span data-stu-id="f28e4-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="f28e4-121">Se você ainda não tiver um data warehouse, saiba como tooCreate um Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f28e4-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="f28e4-122">Desempenho é aprimorado se a conta de armazenamento hello e Olá data warehouse são criados no hello mesmo região.</span><span class="sxs-lookup"><span data-stu-id="f28e4-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="f28e4-123">Etapa 1: Inscrever-se em tooData Studio plataforma com sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="f28e4-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="f28e4-124">Abra seu navegador da web e navegue toohello [Studio da plataforma de dados](https://www.dataplatformstudio.com/) site.</span><span class="sxs-lookup"><span data-stu-id="f28e4-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="f28e4-125">Entrar com hello a mesma conta do Azure que você toocreate usado Olá armazenamento conta e do data warehouse.</span><span class="sxs-lookup"><span data-stu-id="f28e4-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="f28e4-126">Se seu endereço de email for associado a um trabalho ou conta de escola e uma conta da Microsoft, conta de Olá toochoose-se de que tem acesso tooyour recursos.</span><span class="sxs-lookup"><span data-stu-id="f28e4-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="f28e4-127">Se essa é a primeira vez usando o Studio de plataforma de dados, você será solicitado toogrant Olá aplicativo permissão toomanage seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28e4-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="f28e4-128">Etapa 2: Inicie o Assistente de importação de saudação</span><span class="sxs-lookup"><span data-stu-id="f28e4-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="f28e4-129">Na tela principal de DPS hello, selecione Olá tooAzure SQL Data Warehouse link toostart Olá Importar Assistente de importação.</span><span class="sxs-lookup"><span data-stu-id="f28e4-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="f28e4-130">Etapa 3: Instalar Olá dados plataforma Studio Gateway</span><span class="sxs-lookup"><span data-stu-id="f28e4-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="f28e4-131">tooconnect tooyour no SQL Server banco de dados local, você precisa tooinstall Olá DPS Gateway.</span><span class="sxs-lookup"><span data-stu-id="f28e4-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="f28e4-132">gateway de saudação é um agente de cliente que fornece acesso tooyour ambiente local, extrai dados de saudação e carrega-tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f28e4-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="f28e4-133">Os dados nunca passam por servidores da Redgate.</span><span class="sxs-lookup"><span data-stu-id="f28e4-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="f28e4-134">Olá tooinstall Gateway:</span><span class="sxs-lookup"><span data-stu-id="f28e4-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="f28e4-135">Clique em Olá **criar Gateway** link</span><span class="sxs-lookup"><span data-stu-id="f28e4-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="f28e4-136">Baixar e instalar usando o Gateway Olá Olá instalador fornecido</span><span class="sxs-lookup"><span data-stu-id="f28e4-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="f28e4-137">Olá Gateway pode ser instalado em qualquer computador com o banco de dados do network access toohello origem do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f28e4-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="f28e4-138">Ele acessa o banco de dados do SQL Server hello usando a autenticação do Windows com credenciais de saudação do usuário atual do hello.</span><span class="sxs-lookup"><span data-stu-id="f28e4-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="f28e4-139">Uma vez instalado, Olá tooConnected de alterações de status do Gateway e você pode selecionar o próximo.</span><span class="sxs-lookup"><span data-stu-id="f28e4-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="f28e4-140">Etapa 4: Identificar o banco de dados de origem de saudação</span><span class="sxs-lookup"><span data-stu-id="f28e4-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="f28e4-141">Em Olá *insira o nome do servidor* caixa de texto, insira o nome de saudação do servidor de saudação que hospeda seu banco de dados e selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f28e4-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="f28e4-142">Do menu suspenso de Olá, selecione Olá banco de dados que você deseja tooimport dados.</span><span class="sxs-lookup"><span data-stu-id="f28e4-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="f28e4-143">DPS inspeciona o banco de dados selecionados para tabelas tooimport hello.</span><span class="sxs-lookup"><span data-stu-id="f28e4-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="f28e4-144">Por padrão, o DPS importa todas as tabelas de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28e4-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="f28e4-145">Você pode selecionar ou desmarcar tabelas expandindo Olá vincular todas as tabelas.</span><span class="sxs-lookup"><span data-stu-id="f28e4-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="f28e4-146">Selecione Olá próximo botão toomove para frente.</span><span class="sxs-lookup"><span data-stu-id="f28e4-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="f28e4-147">Etapa 5: Escolha um armazenamento conta toostage Olá de dados</span><span class="sxs-lookup"><span data-stu-id="f28e4-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="f28e4-148">DPS solicita um local toostage Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="f28e4-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="f28e4-149">Escolha uma conta de armazenamento existente na sua assinatura e selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f28e4-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="f28e4-150">DPS criará um novo contêiner de blob no hello escolhido conta de armazenamento e usar uma pasta distinta para cada importação.</span><span class="sxs-lookup"><span data-stu-id="f28e4-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="f28e4-151">Etapa 6: Criar um data warehouse</span><span class="sxs-lookup"><span data-stu-id="f28e4-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="f28e4-152">Em seguida, selecione um online [Azure SQL Data Warehouse](http://aka.ms/sqldw) dados Olá tooimport de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f28e4-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="f28e4-153">Depois de selecionar o banco de dados, você precisa tooenter Olá credenciais tooconnect toohello banco de dados e selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f28e4-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="f28e4-154">DPS mescla tabelas de dados de origem de saudação do data warehouse de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28e4-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="f28e4-155">DPS avisa se o nome de tabela Olá exige toooverwrite as tabelas existentes no data warehouse de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28e4-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="f28e4-156">Você pode, opcionalmente, excluir quaisquer objetos existentes no data warehouse de saudação acionamento excluir todos os objetos existentes antes da importação.</span><span class="sxs-lookup"><span data-stu-id="f28e4-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="f28e4-157">Etapa 7: Importar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="f28e4-157">Step 7: Import hello data</span></span>
<span data-ttu-id="f28e4-158">DPS confirma que você gostaria que dados de saudação tooimport.</span><span class="sxs-lookup"><span data-stu-id="f28e4-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="f28e4-159">Basta clicar em Olá Iniciar importação botão toobegin Olá a importação de dados.</span><span class="sxs-lookup"><span data-stu-id="f28e4-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="f28e4-160">DPS exibe uma visualização que mostra o andamento da saudação de extração e carregamento de dados de saudação do progresso de SQL Server e Olá de local de Olá da importação de saudação no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f28e4-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="f28e4-161">Após a conclusão da importação de hello, DPS exibe um resumo da importação de dados hello e um relatório de alteração de correções de compatibilidade de saudação que foram executadas.</span><span class="sxs-lookup"><span data-stu-id="f28e4-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="f28e4-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f28e4-162">Next steps</span></span>
<span data-ttu-id="f28e4-163">tooexplore seus dados no SQL Data Warehouse, inicie por meio da exibição:</span><span class="sxs-lookup"><span data-stu-id="f28e4-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="f28e4-164">[Consultar o Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="f28e4-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="f28e4-165">[Visualizar os dados com o Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="f28e4-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="f28e4-166">toolearn mais sobre o Studio de plataforma de dados do Redgate:</span><span class="sxs-lookup"><span data-stu-id="f28e4-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="f28e4-167">Visite a home page DPS Olá</span><span class="sxs-lookup"><span data-stu-id="f28e4-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="f28e4-168">Assista a uma demonstração do DPS no Channel9</span><span class="sxs-lookup"><span data-stu-id="f28e4-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="f28e4-169">Para obter uma visão geral de outras maneiras toomigrate e carregar os dados no Data Warehouse SQL consulte:</span><span class="sxs-lookup"><span data-stu-id="f28e4-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="f28e4-170">[Migrar tooSQL sua solução do Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="f28e4-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="f28e4-171">Carregar dados no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="f28e4-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="f28e4-172">Para obter mais dicas de desenvolvimento, consulte Olá [visão geral do desenvolvimento de SQL Data Warehouse](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="f28e4-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
