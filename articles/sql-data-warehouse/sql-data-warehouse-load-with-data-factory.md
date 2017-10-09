---
title: "dados de aaaLoad no Azure SQL Data Warehouse – Data Factory | Microsoft Docs"
description: "Este tutorial carrega dados no Azure SQL Data Warehouse com o uso do Azure Data Factory e usa um banco de dados do SQL Server como fonte de dados de saudação."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="42646-103">Carregar dados no SQL Data Warehouse com o Data Factory</span><span class="sxs-lookup"><span data-stu-id="42646-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="42646-104">Você pode usar dados do Azure Data Factory tooload no Azure SQL Data Warehouse de qualquer Olá [suporte para armazenamentos de dados de origem](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="42646-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="42646-105">Por exemplo, é possível carregar dados de um Banco de Dados SQL do Azure ou um Banco de Dados Oracle em um SQL Data Warehouse usando o Data Factory.</span><span class="sxs-lookup"><span data-stu-id="42646-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="42646-106">Tutorial neste artigo mostra como tooload dados do servidor SQL local banco de dados em um data warehouse do SQL.</span><span class="sxs-lookup"><span data-stu-id="42646-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="42646-107">**Tempo estimado**: neste tutorial leva cerca de toocomplete de 10 a 15 minutos depois de saudação pré-requisitos foram atendidos.</span><span class="sxs-lookup"><span data-stu-id="42646-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42646-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42646-108">Prerequisites</span></span>

- <span data-ttu-id="42646-109">É necessário um **banco de dados do SQL Server** com tabelas que contêm dados saudação toobe copiou toohello do SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="42646-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="42646-110">Você precisa de um **SQL Data Warehouse** online.</span><span class="sxs-lookup"><span data-stu-id="42646-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="42646-111">Se você ainda não tiver um data warehouse, saiba como muito[criar um Data Warehouse do Azure SQL](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="42646-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="42646-112">Você precisa de uma **Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="42646-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="42646-113">Se você não tiver uma conta de armazenamento, saiba como muito[criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="42646-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="42646-114">Para melhor desempenho, localize a conta de armazenamento hello e saudação do data warehouse em hello mesma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="42646-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="42646-115">Configurar uma fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="42646-115">Configure a data factory</span></span>
1. <span data-ttu-id="42646-116">Faça logon no toohello [portal do Azure][].</span><span class="sxs-lookup"><span data-stu-id="42646-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="42646-117">Localize o data warehouse e clique em tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="42646-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="42646-118">Na folha principal de saudação, clique em **carregar dados** > **do Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="42646-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Iniciar o assistente para Carregar Dados](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="42646-120">Se você não tem uma fábrica de dados em sua assinatura do Azure, você verá um **nova fábrica de dados** caixa de diálogo em uma guia separada do navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="42646-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="42646-121">Preencha Olá informações solicitadas e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="42646-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="42646-122">Após Olá fábrica de dados é criada, Olá **nova fábrica de dados** caixa de diálogo é fechada, e você vê Olá **selecionar Data Factory** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42646-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="42646-123">Se você tiver um ou mais fábricas de dados já está em Olá assinatura do Azure, você verá Olá **selecionar Data Factory** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42646-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="42646-124">Na caixa de diálogo, você pode selecionar uma fábrica de dados existente ou clique em **criar nova fábrica de dados** toocreate um novo.</span><span class="sxs-lookup"><span data-stu-id="42646-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Configurar o Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="42646-126">Em Olá **selecionar Data Factory** caixa de diálogo, Olá **carregar dados** opção é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="42646-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="42646-127">Clique em **próximo** toostart criando um tarefa de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="42646-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="42646-128">Configurar propriedades de fábrica de dados Olá</span><span class="sxs-lookup"><span data-stu-id="42646-128">Configure hello data factory properties</span></span>
<span data-ttu-id="42646-129">Agora que você criou uma fábrica de dados, Olá próxima etapa é agenda de carregamento de dados de saudação de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="42646-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="42646-130">Em **Nome da tarefa**, digite **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="42646-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="42646-131">Usar saudação padrão **executar uma vez agora** opção, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="42646-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Configurar o agendamento de carregamento](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="42646-133">Configurar armazenamento de dados de origem hello e gateway</span><span class="sxs-lookup"><span data-stu-id="42646-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="42646-134">Agora você informar a fábrica de dados sobre Olá local do SQL Server banco de dados do qual você deseja que os dados tooload.</span><span class="sxs-lookup"><span data-stu-id="42646-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="42646-135">Escolha **do SQL Server** dos dados de origem Olá suporte para armazenar o catálogo e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="42646-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![Escolher a fonte do SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="42646-137">Um **banco de dados de SQL Server local especificar Olá** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="42646-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="42646-138">Olá primeiro **nome de Conexão** campo é automaticamente preenchido.</span><span class="sxs-lookup"><span data-stu-id="42646-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="42646-139">segundo campo de saudação solicita nome de saudação do hello **Gateway**.</span><span class="sxs-lookup"><span data-stu-id="42646-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="42646-140">Se você estiver usando uma fábrica de dados existente que já tem um gateway, você pode reutilizar o gateway Olá selecionando-o na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="42646-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="42646-141">Clique em Olá **criar Gateway** link toocreate um Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="42646-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="42646-142">Se o repositório de dados de origem de saudação é local ou em uma máquina virtual IaaS do Azure, é necessário um Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="42646-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="42646-143">Um gateway tem uma relação de 1-1 com uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="42646-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="42646-144">Ele não pode ser usado em outro fábrica de dados, mas ele pode ser usado por vários dados carregando tarefas com hello mesma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="42646-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="42646-145">Um gateway pode ser usado tooconnect toomultiple os armazenamentos de dados ao executar tarefas de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="42646-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="42646-146">Para obter informações detalhadas sobre o gateway hello, consulte [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="42646-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="42646-147">Uma caixa de diálogo **Criar Gateway** será exibida.</span><span class="sxs-lookup"><span data-stu-id="42646-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="42646-148">Em Nome, insira **GatewayForDWLoading** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="42646-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="42646-149">Uma caixa de diálogo **Configurar Gateway** será exibida.</span><span class="sxs-lookup"><span data-stu-id="42646-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="42646-150">Clique em **iniciar a instalação do express no computador** tooautomatically download, instalar e registrar o Gateway de gerenciamento de dados no computador atual.</span><span class="sxs-lookup"><span data-stu-id="42646-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="42646-151">Olá progresso é mostrado em uma janela pop-up.</span><span class="sxs-lookup"><span data-stu-id="42646-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="42646-152">Se a máquina de saudação não pode se conectar a toohello repositório de dados, você pode manualmente [baixar e instalar gateway Olá](https://www.microsoft.com/download/details.aspx?id=39717) em um computador que possa se conectar a dados toohello armazenar e usar tooregister chave hello.</span><span class="sxs-lookup"><span data-stu-id="42646-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="42646-153">a configuração expressa Olá nativamente funciona com o Microsoft Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="42646-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="42646-154">Se você estiver usando o Google Chrome, primeiro instale extensão do ClickOnce de saudação do repositório do cromo da web.</span><span class="sxs-lookup"><span data-stu-id="42646-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Iniciar a instalação Expressa](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="42646-156">Aguarde Olá toocomplete de configuração de gateway.</span><span class="sxs-lookup"><span data-stu-id="42646-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="42646-157">Depois que o gateway de saudação for registrado com êxito e está online, janela pop-up Olá fecha e novo gateway de saudação aparece no campo gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="42646-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="42646-158">Em seguida, preencha o restante da saudação campos obrigatórios da seguinte maneira, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="42646-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="42646-159">**Nome do servidor**: nome de saudação do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="42646-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="42646-160">**Nome do banco de dados**: banco de dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="42646-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="42646-161">**Criptografia de credencial**: usar o padrão de hello "pelo navegador da web".</span><span class="sxs-lookup"><span data-stu-id="42646-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="42646-162">**Tipo de autenticação**: escolha o tipo de saudação de autenticação você está usando.</span><span class="sxs-lookup"><span data-stu-id="42646-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="42646-163">**Nome de usuário** e **senha**: insira Olá nome de usuário e senha para um usuário que tem permissão toocopy Olá dados.</span><span class="sxs-lookup"><span data-stu-id="42646-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Iniciar a instalação Expressa](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="42646-165">Olá próxima etapa é toochoose tabelas de saudação de quais dados de saudação toocopy.</span><span class="sxs-lookup"><span data-stu-id="42646-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="42646-166">Você pode filtrar tabelas hello usando palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="42646-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="42646-167">E você pode visualizar o esquema de dados e tabela de saudação no painel inferior de saudação.</span><span class="sxs-lookup"><span data-stu-id="42646-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="42646-168">Depois de concluir a seleção, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="42646-168">After you finish your selection, click **Next**.</span></span>

    ![Selecionar tabelas](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="42646-170">Configurar destino hello, o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="42646-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="42646-171">Agora você informar a fábrica de dados sobre informações de destino hello.</span><span class="sxs-lookup"><span data-stu-id="42646-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="42646-172">As informações de conexão do SQL Data Warehouse são preenchidas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42646-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="42646-173">Digite a senha de Olá Olá nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="42646-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="42646-174">e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="42646-174">and click **Next**.</span></span>

    ![Configurar o destino](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="42646-176">Um mapeamento de tabela inteligente aparece que mapeia as tabelas de toodestination de origem com base em nomes de tabela.</span><span class="sxs-lookup"><span data-stu-id="42646-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="42646-177">Se a tabela de saudação não existe no destino hello, por padrão ADF criará um com hello mesmo nome (isso se aplica tooSQL servidor ou banco de dados SQL Azure como origem).</span><span class="sxs-lookup"><span data-stu-id="42646-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="42646-178">Você também pode escolher tabela existente de tooan toomap.</span><span class="sxs-lookup"><span data-stu-id="42646-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="42646-179">Examine e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="42646-179">Review and click **Next**.</span></span>

    ![Mapear tabelas](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="42646-181">Examine o mapeamento de esquema Olá e procure por mensagens de erro ou aviso.</span><span class="sxs-lookup"><span data-stu-id="42646-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="42646-182">O mapeamento inteligente é baseado no nome da coluna.</span><span class="sxs-lookup"><span data-stu-id="42646-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="42646-183">Se há uma conversão de tipo de dados sem suporte entre a coluna de origem e destino hello, você verá uma mensagem de erro ao lado da tabela correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="42646-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="42646-184">Se você escolher automática de fábrica de dados toolet criar tabelas hello, conversão de tipo de dados adequado pode acontecer se necessário toofix incompatibilidade de saudação entre repositórios de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="42646-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Mapear esquema](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="42646-186">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="42646-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="42646-187">Definir configurações de desempenho de saudação</span><span class="sxs-lookup"><span data-stu-id="42646-187">Configure hello performance settings</span></span>
<span data-ttu-id="42646-188">Olá configurações de desempenho, você configurar uma conta de armazenamento do Azure usada para teste antes de ele carrega no SQL Data Warehouse performantly usando Olá [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="42646-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="42646-189">Após copiar hello, dados intermediários saudação no armazenamento serão limpas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42646-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="42646-190">Selecione uma conta de armazenamento do Azure existente e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="42646-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configurar um blob de preparo](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="42646-192">Revisar informações de resumo e implantar o pipeline de saudação</span><span class="sxs-lookup"><span data-stu-id="42646-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="42646-193">Examine a configuração de saudação e clique em **concluir** pipeline de saudação do botão toodeploy.</span><span class="sxs-lookup"><span data-stu-id="42646-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Implantar o data factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="42646-195">Monitorar o progresso do carregamento de dados</span><span class="sxs-lookup"><span data-stu-id="42646-195">Monitor data loading progress</span></span>

<span data-ttu-id="42646-196">Você pode ver o progresso da implantação hello e resulta em Olá **implantação** página.</span><span class="sxs-lookup"><span data-stu-id="42646-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="42646-197">Depois de implantação hello, clique o link de saudação que diz **clique aqui pipeline de cópia toomonitor** toomonitor dados progresso do carregamento.</span><span class="sxs-lookup"><span data-stu-id="42646-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![Monitorar o pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="42646-199">Olá recém-criado **DWLoadData fromSQLServer** pipeline de carregamento de dados é automaticamente selecionado do hello esquerdo **Gerenciador de recursos**.</span><span class="sxs-lookup"><span data-stu-id="42646-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Exibir o pipeline](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="42646-201">Clique no pipeline de saudação no meio Olá Olá do painel toosee status detalhado para cada tabela que mapeia tooan atividade.</span><span class="sxs-lookup"><span data-stu-id="42646-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Exibir a atividade da tabela](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="42646-203">Ainda mais, clique em uma atividade e você vê dados Olá Carregando detalhes no painel direito hello, incluindo o tamanho dos dados, linhas, taxa de transferência, etc.</span><span class="sxs-lookup"><span data-stu-id="42646-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Exibir os detalhes da atividade da tabela](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="42646-205">toolaunch esse monitoramento exibição posterior, vá tooyour SQL Data Warehouse, clique **carregar dados > Azure Data Factory**, selecione sua fábrica e escolha **monitorar existentes ao carregar tarefas**.</span><span class="sxs-lookup"><span data-stu-id="42646-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42646-206">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42646-206">Next steps</span></span>

<span data-ttu-id="42646-207">toomigrate tooSQL o banco de dados do Data Warehouse, consulte [visão geral da migração](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="42646-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="42646-208">toolearn mais sobre Azure Data Factory e seus recursos de movimentação de dados, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="42646-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="42646-209">Introdução tooAzure fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="42646-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="42646-210">Mover dados usando a Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="42646-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="42646-211">Mover tooand de dados de uso do Azure Data Factory do Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="42646-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="42646-212">tooexplore seus dados no Data Warehouse do SQL, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="42646-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="42646-213">Conecte-se tooSQL Data Warehouse com o Visual Studio e SSDT</span><span class="sxs-lookup"><span data-stu-id="42646-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="42646-214">[Dados visuais com o Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="42646-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[portal do Azure]: https://portal.azure.com
