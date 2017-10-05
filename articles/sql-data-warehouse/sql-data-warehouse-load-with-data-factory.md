---
title: "Carregar dados no SQL Data Warehouse do Azure – Data Factory | Microsoft Docs"
description: Este tutorial carrega dados no SQL Data Warehouse do Azure usando o Azure Data Factory e usa um banco de dados SQL Server como a fonte de dados.
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
ms.openlocfilehash: 12a35213e07ff16bdc1c27be106792bcc032ac80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="96f7d-103">Carregar dados no SQL Data Warehouse com o Data Factory</span><span class="sxs-lookup"><span data-stu-id="96f7d-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="96f7d-104">Você pode usar o Azure Data Factory para carregar dados no SQL Data Warehouse do Azure de qualquer um dos [repositórios de dados de origem com suporte](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="96f7d-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="96f7d-105">Por exemplo, é possível carregar dados de um Banco de Dados SQL do Azure ou um Banco de Dados Oracle em um SQL Data Warehouse usando o Data Factory.</span><span class="sxs-lookup"><span data-stu-id="96f7d-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="96f7d-106">O tutorial neste artigo mostra como carregar dados de um banco de dados local do SQL Server em um SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="96f7d-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="96f7d-107">**Tempo estimado**: este tutorial levará cerca de 10 a 15 minutos para ser concluído depois que os pré-requisitos forem atendidos.</span><span class="sxs-lookup"><span data-stu-id="96f7d-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96f7d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="96f7d-108">Prerequisites</span></span>

- <span data-ttu-id="96f7d-109">Você precisa de um **Banco de Dados do SQL Server** com tabelas que contêm os dados a serem copiados para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="96f7d-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span></span>  

- <span data-ttu-id="96f7d-110">Você precisa de um **SQL Data Warehouse** online.</span><span class="sxs-lookup"><span data-stu-id="96f7d-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="96f7d-111">Se você ainda não tiver um data warehouse, saiba como [Criar um SQL Data Warehouse do Azure](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="96f7d-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="96f7d-112">Você precisa de uma **Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="96f7d-113">Se você ainda não tem uma conta de armazenamento, aprenda como [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="96f7d-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="96f7d-114">Para melhor desempenho, localize a conta de armazenamento e o data warehouse na mesma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="96f7d-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="96f7d-115">Configurar uma fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="96f7d-115">Configure a data factory</span></span>
1. <span data-ttu-id="96f7d-116">Faça logon no [Portal do Azure][].</span><span class="sxs-lookup"><span data-stu-id="96f7d-116">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="96f7d-117">Localize seu data warehouse e clique para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="96f7d-117">Locate your data warehouse and click to open it.</span></span>
3. <span data-ttu-id="96f7d-118">Na folha principal, clique em **Carregar Dados** > **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Iniciar o assistente para Carregar Dados](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="96f7d-120">Se você não tem uma fábrica de dados na sua assinatura do Azure, você verá uma caixa de diálogo **Nova fábrica de dados** em uma guia separada do navegador.</span><span class="sxs-lookup"><span data-stu-id="96f7d-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span></span> <span data-ttu-id="96f7d-121">Preencha as informações solicitadas e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-121">Fill in the requested information, and click **Create**.</span></span> <span data-ttu-id="96f7d-122">Depois que a fábrica de dados for criada, a caixa de diálogo **Nova fábrica de dados** será fechada e você verá a caixa de diálogo **Selecionar fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="96f7d-123">Se você já tem uma ou mais fábricas de dados na assinatura do Azure, você verá a caixa de diálogo **Selecionar fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span></span> <span data-ttu-id="96f7d-124">Nessa caixa de diálogo é possível selecionar uma fábrica de dados existente ou clicar em **Criar nova fábrica de dados** para criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="96f7d-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span></span>

    ![Configurar o Data Factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="96f7d-126">Na caixa de diálogo **Selecionar Data Factory**, a opção **Carregar dados** é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="96f7d-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span></span> <span data-ttu-id="96f7d-127">Clique em **Avançar** para começar a criar uma tarefa de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-127">Click **Next** to start creating a data loading task.</span></span>

## <a name="configure-the-data-factory-properties"></a><span data-ttu-id="96f7d-128">Configurar as propriedades do data factory</span><span class="sxs-lookup"><span data-stu-id="96f7d-128">Configure the data factory properties</span></span>
<span data-ttu-id="96f7d-129">Agora que você criou um data factory, a próxima etapa é configurar o agendamento de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span></span>

1. <span data-ttu-id="96f7d-130">Em **Nome da tarefa**, digite **DWLoadData-fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="96f7d-131">Use a opção padrão **Executar uma vez agora** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-131">Use the default **Run once now** option, click **Next**.</span></span>

    ![Configurar o agendamento de carregamento](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-the-source-data-store-and-gateway"></a><span data-ttu-id="96f7d-133">Configurar o gateway e o repositório de dados de origem</span><span class="sxs-lookup"><span data-stu-id="96f7d-133">Configure the source data store and gateway</span></span>
<span data-ttu-id="96f7d-134">Agora você informa o Data Factory sobre o banco de dados SQL Server local do qual você deseja carregar os dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span></span>

1. <span data-ttu-id="96f7d-135">Escolha **SQL Server** no catálogo de armazenamento de dados de origem com suporte e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span></span>

    ![Escolher a fonte do SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="96f7d-137">Uma caixa de diálogo **Especificar o banco de dados SQL Server local** será exibida.</span><span class="sxs-lookup"><span data-stu-id="96f7d-137">A **Specify the on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="96f7d-138">O primeiro campo **Nome da conexão** é preenchido automaticamente.</span><span class="sxs-lookup"><span data-stu-id="96f7d-138">The first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="96f7d-139">O segundo campo solicita o nome do **Gateway**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-139">The second field asks for the name of the **Gateway**.</span></span> <span data-ttu-id="96f7d-140">Se estiver usando uma fábrica de dados existente que já tenha um gateway, você poderá reutilizar o gateway, selecionando-o na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="96f7d-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span></span> <span data-ttu-id="96f7d-141">Clique no link **Criar Gateway** para criar um Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-141">Click the **Create Gateway** link to create a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="96f7d-142">Se o armazenamento de dados de origem for local ou estiver em uma máquina virtual do Azure IaaS, será necessário usar um gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="96f7d-143">Um gateway tem uma relação de 1-1 com uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="96f7d-144">Ele não pode ser usado de outra data factory, mas pode ser usado por várias tarefas de carregamento de dados na mesma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span></span> <span data-ttu-id="96f7d-145">Um gateway pode ser usado para se conectar a vários repositórios de dados durante a execução de tarefas de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="96f7d-146">Para obter informações detalhadas sobre o gateway, consulte o artigo [Gateway de Gerenciamento de Dados](../data-factory/data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="96f7d-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="96f7d-147">Uma caixa de diálogo **Criar Gateway** será exibida.</span><span class="sxs-lookup"><span data-stu-id="96f7d-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="96f7d-148">Em Nome, insira **GatewayForDWLoading** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="96f7d-149">Uma caixa de diálogo **Configurar Gateway** será exibida.</span><span class="sxs-lookup"><span data-stu-id="96f7d-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="96f7d-150">Clique em **Iniciar a instalação expressa neste computador** para baixar, instalar e registrar automaticamente o Gateway de Gerenciamento de Dados no computador atual.</span><span class="sxs-lookup"><span data-stu-id="96f7d-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="96f7d-151">O progresso é mostrado em uma janela pop-up.</span><span class="sxs-lookup"><span data-stu-id="96f7d-151">The progress is shown in a pop-up window.</span></span> <span data-ttu-id="96f7d-152">Se o computador não puder se conectar ao armazenamento de dados, você poderá [baixar e instalar o gateway](https://www.microsoft.com/download/details.aspx?id=39717) manualmente em um computador que possa se conectar ao armazenamento de dados e, em seguida, usar a chave para registrar.</span><span class="sxs-lookup"><span data-stu-id="96f7d-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span></span>
    > [!NOTE]
    > <span data-ttu-id="96f7d-153">A instalação expressa funciona nativamente com o Microsoft Edge e o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="96f7d-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="96f7d-154">Se você estiver usando o Google Chrome, primeiro instale a extensão ClickOnce na loja na Web do Chrome.</span><span class="sxs-lookup"><span data-stu-id="96f7d-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span></span>

    ![Iniciar a instalação Expressa](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="96f7d-156">Aguarde a conclusão da instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="96f7d-156">Wait for the gateway setup to complete.</span></span> <span data-ttu-id="96f7d-157">Depois que o gateway for registrado com êxito e estiver online, a janela pop-up será fechada e o novo gateway será exibido no campo do gateway.</span><span class="sxs-lookup"><span data-stu-id="96f7d-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span></span> <span data-ttu-id="96f7d-158">Em seguida, preencha o restante dos campos obrigatórios como se segue e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-158">Then fill in the rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="96f7d-159">**Nome do servidor**: nome do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="96f7d-159">**Server name**: Name of the on-premises SQL Server.</span></span>
    - <span data-ttu-id="96f7d-160">**Nome do banco de dados**: banco de dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96f7d-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="96f7d-161">**Criptografia de credencial**: use o padrão "Pelo navegador da Web".</span><span class="sxs-lookup"><span data-stu-id="96f7d-161">**Credential encryption**: Use the default "By web browser".</span></span>
    - <span data-ttu-id="96f7d-162">**Tipo de autenticação**: escolha o tipo de autenticação que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="96f7d-162">**Authentication type**: Choose the type of authentication you are using.</span></span>
    - <span data-ttu-id="96f7d-163">**Nome de usuário** e **senha**: insira o nome de usuário e a senha de um usuário que tem permissão para copiar os dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span></span>

    ![Iniciar a instalação Expressa](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="96f7d-165">A próxima etapa é escolher as tabelas das quais os dados serão copiados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-165">The next step is to choose the tables from which to copy the data.</span></span> <span data-ttu-id="96f7d-166">Filtre as tabelas usando palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="96f7d-166">You can filter the tables by using keywords.</span></span> <span data-ttu-id="96f7d-167">Além disso, você pode visualizar o esquema de dados e tabela no painel inferior.</span><span class="sxs-lookup"><span data-stu-id="96f7d-167">And you can preview the data and table schema in the bottom panel.</span></span> <span data-ttu-id="96f7d-168">Depois de concluir a seleção, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-168">After you finish your selection, click **Next**.</span></span>

    ![Selecionar tabelas](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-the-destination-your-sql-data-warehouse"></a><span data-ttu-id="96f7d-170">Configurar o destino, o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="96f7d-170">Configure the destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="96f7d-171">Agora você informa ao Data Factory sobre as informações de destino.</span><span class="sxs-lookup"><span data-stu-id="96f7d-171">Now you tell Data Factory about the destination information.</span></span>

1. <span data-ttu-id="96f7d-172">As informações de conexão do SQL Data Warehouse são preenchidas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="96f7d-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="96f7d-173">Insira a senha para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="96f7d-173">Enter the password for the user name.</span></span> <span data-ttu-id="96f7d-174">e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-174">and click **Next**.</span></span>

    ![Configurar o destino](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="96f7d-176">É exibido um mapeamento de tabela inteligente, que mapeia tabelas de origem para tabelas de destino com base em nomes de tabelas.</span><span class="sxs-lookup"><span data-stu-id="96f7d-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span></span> <span data-ttu-id="96f7d-177">Se a tabela não existir no destino, o ADF criará uma por padrão com o mesmo nome (isso se aplica ao SQL Server ou ao Banco de Dados SQL do Azure como fonte).</span><span class="sxs-lookup"><span data-stu-id="96f7d-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="96f7d-178">Também é possível mapear para uma tabela existente.</span><span class="sxs-lookup"><span data-stu-id="96f7d-178">You can also choose to map to an existing table.</span></span> <span data-ttu-id="96f7d-179">Examine e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-179">Review and click **Next**.</span></span>

    ![Mapear tabelas](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="96f7d-181">Examine o mapeamento de esquema e procure mensagens de erro ou de aviso.</span><span class="sxs-lookup"><span data-stu-id="96f7d-181">Review the schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="96f7d-182">O mapeamento inteligente é baseado no nome da coluna.</span><span class="sxs-lookup"><span data-stu-id="96f7d-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="96f7d-183">Se houver uma conversão de tipo de dados sem suporte entre a coluna de origem e de destino, você verá uma mensagem de erro juntamente com a tabela correspondente.</span><span class="sxs-lookup"><span data-stu-id="96f7d-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span></span> <span data-ttu-id="96f7d-184">Se você escolher permitir que o Data Factory crie automaticamente as tabelas, a conversão apropriada de tipo de dados poderá ocorrer se for necessário corrigir a incompatibilidade entre os repositórios de origem e destino.</span><span class="sxs-lookup"><span data-stu-id="96f7d-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span></span>

    ![Mapear esquema](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="96f7d-186">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-186">Click **Next**.</span></span>

## <a name="configure-the-performance-settings"></a><span data-ttu-id="96f7d-187">Definir as configurações de desempenho</span><span class="sxs-lookup"><span data-stu-id="96f7d-187">Configure the performance settings</span></span>
<span data-ttu-id="96f7d-188">Nas configurações de Desempenho, configure uma conta de armazenamento do Azure usada para preparar os dados antes de carregá-los no de forma definitiva no SQL Data Warehouse usando o [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="96f7d-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="96f7d-189">Depois que a cópia for concluída, os dados provisórios no armazenamento serão limpos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="96f7d-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="96f7d-190">Selecione uma conta de armazenamento do Azure existente e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configurar um blob de preparo](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-the-pipeline"></a><span data-ttu-id="96f7d-192">Examinar as informações de resumo e implantar o pipeline</span><span class="sxs-lookup"><span data-stu-id="96f7d-192">Review summary information and deploy the pipeline</span></span>

<span data-ttu-id="96f7d-193">Examine a configuração e clique no botão **Concluir** para implantar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="96f7d-193">Review the configuration and click **Finish** button to deploy the pipeline.</span></span>

![Implantar o data factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="96f7d-195">Monitorar o progresso do carregamento de dados</span><span class="sxs-lookup"><span data-stu-id="96f7d-195">Monitor data loading progress</span></span>

<span data-ttu-id="96f7d-196">Você pode ver o progresso e os resultados da implantação na página **Implantação**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-196">You can see the deployment progress and results in the **Deployment** page.</span></span>

1. <span data-ttu-id="96f7d-197">Quando a implantação estiver concluída, clique no link **Clique aqui para monitorar o pipeline de cópia** para monitorar o progresso do carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="96f7d-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span></span>

    ![Monitorar o pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="96f7d-199">O pipeline de carregamento de dados recém-criado **DWLoadData-fromSQLServer** é automaticamente selecionado no **Gerenciador de Recursos** à esquerda.</span><span class="sxs-lookup"><span data-stu-id="96f7d-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span></span>

    ![Exibir o pipeline](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="96f7d-201">Clique no pipeline, no painel do meio, para ver o status detalhado de cada tabela mapeada para uma Atividade.</span><span class="sxs-lookup"><span data-stu-id="96f7d-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span></span>

    ![Exibir a atividade da tabela](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="96f7d-203">Continue clicando em uma atividade e você verá os detalhes do carregamento de dados no painel direito, incluindo tamanho dos dados, linhas, taxa de transferência, etc.</span><span class="sxs-lookup"><span data-stu-id="96f7d-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span></span>

    ![Exibir os detalhes da atividade da tabela](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="96f7d-205">Para iniciar esta exibição de monitoramento mais tarde, vá para o SQL Data Warehouse, clique em **Carregar Dados > Azure Data Factory**, selecione seu factory e escolha **Monitorar as tarefas de carregamento existentes**.</span><span class="sxs-lookup"><span data-stu-id="96f7d-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96f7d-206">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96f7d-206">Next steps</span></span>

<span data-ttu-id="96f7d-207">Para migrar seu banco de dados para o SQL Data Warehouse, consulte [Visão geral da migração](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="96f7d-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="96f7d-208">Para saber mais sobre o Azure Data Factory e seus recursos de movimentação de dados, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="96f7d-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span></span>

- [<span data-ttu-id="96f7d-209">Introdução ao Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="96f7d-209">Introduction to Azure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="96f7d-210">Mover dados usando a Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="96f7d-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="96f7d-211">Mover dados para e do SQL Data Warehouse do Azure usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="96f7d-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="96f7d-212">Para explorar seus dados no SQL Data Warehouse, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="96f7d-212">To explore your data in SQL Data Warehouse, see the following articles:</span></span>

- [<span data-ttu-id="96f7d-213">Conectar-se ao SQL Data Warehouse com o Visual Studio e o SSDT</span><span class="sxs-lookup"><span data-stu-id="96f7d-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="96f7d-214">[Dados visuais com o Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="96f7d-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Portal do Azure]: https://portal.azure.com
