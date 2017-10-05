---
title: Use o Redgate para carregar dados para o Data Warehouse do Azure | Microsoft Docs
description: "Saiba como usar o Data Platform Studio da Redgate para cenários de data warehouse."
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
ms.openlocfilehash: a38b237d5bfc0450c1ca79b53a5784dbb9bf8602
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="c4c31-103">Carregar dados com o Data Platform Studio da Redgate</span><span class="sxs-lookup"><span data-stu-id="c4c31-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4c31-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="c4c31-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="c4c31-105">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="c4c31-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="c4c31-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="c4c31-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="c4c31-107">BCP</span><span class="sxs-lookup"><span data-stu-id="c4c31-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="c4c31-108">Este tutorial mostra como usar o [Data Platform Studio da Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) para mover dados de um SQL Server local para o SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4c31-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premises SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c4c31-109">O Data Platform Studio aplica-se as correções de compatibilidade e otimizações mais apropriada, portanto, é a maneira mais rápida de começar a usar o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c4c31-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="c4c31-110">[Redgate](http://www.red-gate.com) é um antigo parceiro da Microsoft que oferece várias ferramentas de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c4c31-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="c4c31-111">Esse recurso no Data Platform Studio ficou disponível gratuitamente para uso comercial e não comercial.</span><span class="sxs-lookup"><span data-stu-id="c4c31-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="c4c31-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c4c31-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="c4c31-113">Criar ou identificar recursos</span><span class="sxs-lookup"><span data-stu-id="c4c31-113">Create or identify resources</span></span>
<span data-ttu-id="c4c31-114">Antes de iniciar este tutorial, você precisa ter os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4c31-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="c4c31-115">**Banco de dados do SQL Server local**: os dados que você deseja importar para o SQL Data Warehouse precisam vir de um SQL Server local (versão 2008R2 ou superior).</span><span class="sxs-lookup"><span data-stu-id="c4c31-115">**on-premises SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="c4c31-116">Data Platform Studio não pode importar dados diretamente de um Banco de Dados SQL do Azure ou de arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="c4c31-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="c4c31-117">**Conta de Armazenamento do Azure**: o Data Platform Studio prepara os dados no Armazenamento de Blobs do Azure antes de carregá-los no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c4c31-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="c4c31-118">A conta de armazenamento deve estar usando o modelo de implantação "Gerenciador de recursos" (o padrão), em vez do modelo de implantação "Clássico".</span><span class="sxs-lookup"><span data-stu-id="c4c31-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="c4c31-119">Se você não tiver uma conta de armazenamento, aprenda como criar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4c31-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="c4c31-120">**SQL Data Warehouse**: este tutorial move os dados do SQL Server local para o SQL Data Warehouse, por isso você precisa ter um data warehouse online.</span><span class="sxs-lookup"><span data-stu-id="c4c31-120">**SQL Data Warehouse**: This tutorial moves the data from on-premises SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="c4c31-121">Se você ainda não tiver um data warehouse, saiba como criar um Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c4c31-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="c4c31-122">O desempenho é aprimorado se a conta de armazenamento e o data warehouse são criados na mesma região.</span><span class="sxs-lookup"><span data-stu-id="c4c31-122">Performance is improved if the storage account and the data warehouse are created in the same region.</span></span>
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="c4c31-123">Etapa 1: Entrar no Data Platform Studio com sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="c4c31-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="c4c31-124">Abra seu navegador da Web e navegue até o site do [Data Platform Studio](https://www.dataplatformstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c4c31-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="c4c31-125">Entrar com a mesma conta do Azure que você usou para criar o data warehouse a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4c31-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="c4c31-126">Se seu endereço de email está associado a uma conta corporativa ou de estudante e a uma conta da Microsoft, certifique-se de escolher a conta que tenha acesso aos seus recursos.</span><span class="sxs-lookup"><span data-stu-id="c4c31-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> <span data-ttu-id="c4c31-127">Se esta for sua primeira vez usando o Data Platform Studio, você precisará conceder a permissão de aplicativo para gerenciar os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4c31-127">If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="c4c31-128">Etapa 2: Iniciar o assistente de importação</span><span class="sxs-lookup"><span data-stu-id="c4c31-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="c4c31-129">Na tela principal do DPS, selecione o link Importar para Azure SQL Data Warehouse para iniciar o assistente de importação.</span><span class="sxs-lookup"><span data-stu-id="c4c31-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="c4c31-130">Etapa 3: Instalar o gateway do Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="c4c31-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="c4c31-131">Para se conectar ao banco de dados do SQL Server local, você precisa instalar o Gateway do DPS.</span><span class="sxs-lookup"><span data-stu-id="c4c31-131">To connect to your on-premises SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="c4c31-132">O gateway é um agente cliente que fornece acesso ao seu ambiente local, extrai os dados e carrega-os em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4c31-132">The gateway is a client agent that provides access to your on-premises environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="c4c31-133">Os dados nunca passam por servidores da Redgate.</span><span class="sxs-lookup"><span data-stu-id="c4c31-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="c4c31-134">Instalar o Gateway:</span><span class="sxs-lookup"><span data-stu-id="c4c31-134">To install the Gateway:</span></span>

1. <span data-ttu-id="c4c31-135">Clique no link **Criar Gateway**</span><span class="sxs-lookup"><span data-stu-id="c4c31-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="c4c31-136">Baixe e instale o Gateway usando o instalador fornecido</span><span class="sxs-lookup"><span data-stu-id="c4c31-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="c4c31-137">O Gateway pode ser instalado em qualquer computador com acesso à rede para o banco de dados do SQL Server de origem.</span><span class="sxs-lookup"><span data-stu-id="c4c31-137">The Gateway can be installed on any machine with network access to the source SQL Server database.</span></span> <span data-ttu-id="c4c31-138">Ele acessa o banco de dados do SQL Server usando a autenticação do Windows com as credenciais do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="c4c31-138">It accesses the SQL Server database using Windows authentication with the credentials of the current user.</span></span>
> 
> 

<span data-ttu-id="c4c31-139">Uma vez instalado, o status de Gateway é alterado para Conectado e você pode selecionar Avançar.</span><span class="sxs-lookup"><span data-stu-id="c4c31-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="c4c31-140">Etapa 4: Identificar o banco de dados de origem</span><span class="sxs-lookup"><span data-stu-id="c4c31-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="c4c31-141">Na caixa de texto *Insira o nome do servidor*, digite o nome do servidor que hospeda seu banco de dados e selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c4c31-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="c4c31-142">Em seguida, no menu suspenso, selecione o banco de dados do qual você deseja importar dados.</span><span class="sxs-lookup"><span data-stu-id="c4c31-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="c4c31-143">O DPS inspeciona o banco de dados para as tabelas a serem importadas.</span><span class="sxs-lookup"><span data-stu-id="c4c31-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="c4c31-144">Por padrão, o DPS importa todas as tabelas no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c4c31-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="c4c31-145">Você pode marcar ou desmarcar tabelas expandindo o link de todas as tabelas.</span><span class="sxs-lookup"><span data-stu-id="c4c31-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="c4c31-146">Selecione o botão Avançar para continuar.</span><span class="sxs-lookup"><span data-stu-id="c4c31-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="c4c31-147">Etapa 5: Escolha uma conta de armazenamento a fim de preparar os dados</span><span class="sxs-lookup"><span data-stu-id="c4c31-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="c4c31-148">O DPS solicitará um local para transferir os dados.</span><span class="sxs-lookup"><span data-stu-id="c4c31-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="c4c31-149">Escolha uma conta de armazenamento existente na sua assinatura e selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c4c31-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="c4c31-150">O DPS criará um novo contêiner blob na conta de armazenamento escolhida e use uma pasta distinta para cada importação.</span><span class="sxs-lookup"><span data-stu-id="c4c31-150">DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="c4c31-151">Etapa 6: Criar um data warehouse</span><span class="sxs-lookup"><span data-stu-id="c4c31-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="c4c31-152">Em seguida, selecione o banco de dados online [Azure SQL Data Warehouse](http://aka.ms/sqldw) para importar os dados.</span><span class="sxs-lookup"><span data-stu-id="c4c31-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="c4c31-153">Depois de selecionar o banco de dados, você precisa inserir as credenciais para se conectar ao banco de dados e selecionar **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c4c31-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="c4c31-154">O DPS mescla as tabelas de dados de origem no data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c4c31-154">DPS merges the source data tables into the data warehouse.</span></span> <span data-ttu-id="c4c31-155">O DPS avisa se o nome da tabela requer a substituição das tabelas existentes no data warehouse.</span><span class="sxs-lookup"><span data-stu-id="c4c31-155">DPS warns you if the table name requires it to overwrite existing tables in the data warehouse.</span></span> <span data-ttu-id="c4c31-156">Você, opcionalmente, poderá excluir quaisquer objetos existentes no data warehouse, clicando em excluir todos os objetos existentes antes da importação.</span><span class="sxs-lookup"><span data-stu-id="c4c31-156">You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="c4c31-157">Etapa 7: Importar dados</span><span class="sxs-lookup"><span data-stu-id="c4c31-157">Step 7: Import the data</span></span>
<span data-ttu-id="c4c31-158">O DPS confirma que você deseja importar os dados.</span><span class="sxs-lookup"><span data-stu-id="c4c31-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="c4c31-159">Basta clicar no botão de iniciar importação para iniciar a importação de dados.</span><span class="sxs-lookup"><span data-stu-id="c4c31-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="c4c31-160">O DPS exibe uma visualização que mostra o andamento da extração e carregamento de dados do SQL Server local e o andamento da importação no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c4c31-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premises SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="c4c31-161">Depois que a importação for concluída, o DPS exibe um resumo da importação de dados e um relatório de alteração das correções de compatibilidade que foram executadas.</span><span class="sxs-lookup"><span data-stu-id="c4c31-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="c4c31-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4c31-162">Next steps</span></span>
<span data-ttu-id="c4c31-163">Para explorar seus dados no SQL Data Warehouse, inicie por meio da exibição:</span><span class="sxs-lookup"><span data-stu-id="c4c31-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="c4c31-164">[Consultar o Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="c4c31-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="c4c31-165">[Visualizar os dados com o Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="c4c31-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="c4c31-166">Para saber mais sobre o Data Platform Studio da Redgate:</span><span class="sxs-lookup"><span data-stu-id="c4c31-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="c4c31-167">Visite a página inicial do DPS</span><span class="sxs-lookup"><span data-stu-id="c4c31-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="c4c31-168">Assista a uma demonstração do DPS no Channel9</span><span class="sxs-lookup"><span data-stu-id="c4c31-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="c4c31-169">Para obter uma visão geral de outras maneiras de migrar e carregar os dados no SQL Data Warehouse, consulte:</span><span class="sxs-lookup"><span data-stu-id="c4c31-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="c4c31-170">[Migrar sua solução para o SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="c4c31-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* [<span data-ttu-id="c4c31-171">Carregar dados no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="c4c31-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="c4c31-172">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="c4c31-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

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
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
