---
title: aaaSQL atividade de procedimento armazenado do servidor
description: "Saiba como você pode usar o hello atividade de procedimento armazenado do SQL Server tooinvoke um procedimento armazenado em um banco de dados do SQL Azure ou Azure SQL Data Warehouse de um pipeline da fábrica de dados."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="e96d1-103">Atividade de procedimento armazenado do SQL Server</span><span class="sxs-lookup"><span data-stu-id="e96d1-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="e96d1-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="e96d1-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="e96d1-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="e96d1-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="e96d1-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="e96d1-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="e96d1-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="e96d1-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="e96d1-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="e96d1-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="e96d1-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e96d1-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="e96d1-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e96d1-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="e96d1-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="e96d1-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="e96d1-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e96d1-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="e96d1-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="e96d1-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="e96d1-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e96d1-114">Overview</span></span>
<span data-ttu-id="e96d1-115">Use atividades de transformação de dados em uma fábrica de dados [pipeline](data-factory-create-pipelines.md) tootransform e processar dados brutos em previsões e ideias.</span><span class="sxs-lookup"><span data-stu-id="e96d1-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="e96d1-116">Hello atividade de procedimento armazenado é uma das atividades de transformação de saudação que dá suporte a fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="e96d1-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="e96d1-117">Este artigo aproveita Olá [atividades de transformação de dados](data-factory-data-transformation-activities.md) artigo, que apresenta uma visão geral de transformação de dados e atividades de transformação de saudação tem suportada na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="e96d1-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="e96d1-118">Você pode usar o hello atividade de procedimento armazenado tooinvoke um procedimento armazenado em um dos seguintes dados de saudação armazena em sua empresa ou em uma máquina virtual do Azure (VM):</span><span class="sxs-lookup"><span data-stu-id="e96d1-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="e96d1-119">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="e96d1-119">Azure SQL Database</span></span>
- <span data-ttu-id="e96d1-120">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="e96d1-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="e96d1-121">Banco de Dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e96d1-121">SQL Server Database.</span></span>  <span data-ttu-id="e96d1-122">Se você estiver usando o SQL Server, instale o Gateway de gerenciamento de dados no mesmo computador que hospeda Olá banco de dados ou em um computador separado que tem o banco de dados do access toohello de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="e96d1-123">O Gateway de Gerenciamento de Dados é um componente que conecta fontes de dados locais ou em uma VM do Azure a serviços de nuvem de maneira segura e gerenciada.</span><span class="sxs-lookup"><span data-stu-id="e96d1-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="e96d1-124">Consulte o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="e96d1-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e96d1-125">Ao copiar dados em um banco de dados do SQL Azure ou o SQL Server, você pode configurar Olá **SqlSink** na atividade de cópia tooinvoke um procedimento armazenado usando Olá **sqlWriterStoredProcedureName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="e96d1-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="e96d1-126">Para obter mais informações, consulte [Invocar um procedimento armazenado por meio da atividade de cópia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="e96d1-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="e96d1-127">Para obter detalhes sobre a propriedade hello, veja a seguir os artigos de conector: [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [do SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e96d1-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="e96d1-128">Não há suporte para invocar um procedimento armazenado ao copiar dados em um SQL Data Warehouse do Azure usando uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="e96d1-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="e96d1-129">Porém, você pode usar tooinvoke atividade de procedimento armazenada de saudação um procedimento armazenado em um SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e96d1-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="e96d1-130">Ao copiar dados de banco de dados do SQL Azure ou o SQL Server ou o Azure SQL Data Warehouse, você pode configurar **SqlSource** na atividade de cópia tooinvoke um procedimento armazenado tooread os dados de banco de dados de origem de saudação usando Olá  **sqlReaderStoredProcedureName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="e96d1-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="e96d1-131">Para obter mais informações, consulte Olá seguintes artigos de conector: [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [do SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="e96d1-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="e96d1-132">Olá, seguindo as instruções passo a passo usa hello atividade de procedimento armazenado em um pipeline tooinvoke um procedimento armazenado em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e96d1-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="e96d1-133">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="e96d1-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="e96d1-134">Tabela de exemplo e procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="e96d1-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="e96d1-135">Crie seguinte Olá **tabela** em seu banco de dados SQL usando o SQL Server Management Studio ou qualquer outra ferramenta que você estiver familiarizado com o.</span><span class="sxs-lookup"><span data-stu-id="e96d1-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="e96d1-136">coluna de datetimestamp Olá é date de hello e hora em que a ID correspondente Olá é gerado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="e96d1-137">ID exclusivo Olá identificado de Olá datetimestamp está date de hello e hora em que a ID correspondente Olá é gerado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![Dados de amostra](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="e96d1-139">Neste exemplo, procedimento armazenado de saudação está em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e96d1-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="e96d1-140">Se hello procedimento armazenado está em um Data warehouse do SQL Azure e o banco de dados do SQL Server, a abordagem de saudação é semelhante.</span><span class="sxs-lookup"><span data-stu-id="e96d1-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="e96d1-141">Para um Banco de Dados do SQL Server, você deve instalar um [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="e96d1-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="e96d1-142">Crie seguinte Olá **procedimento armazenado** que insere dados na toohello **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="e96d1-143">**Nome** e **maiusculas e minúsculas** de saudação (DateTime neste exemplo) do parâmetro deve corresponder de parâmetro especificado em Olá pipeline/atividade JSON.</span><span class="sxs-lookup"><span data-stu-id="e96d1-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="e96d1-144">Olá a definição do procedimento armazenado no, certifique-se de que  **@**  é usado como um prefixo para o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="e96d1-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="e96d1-145">Criar uma data factory</span><span class="sxs-lookup"><span data-stu-id="e96d1-145">Create a data factory</span></span>
1. <span data-ttu-id="e96d1-146">Faça logon no muito[portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e96d1-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e96d1-147">Clique em **novo** no menu esquerdo Olá **Intelligence + análise**e clique em **fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Novo data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="e96d1-149">Em Olá **nova fábrica de dados** folha, digite **SProcDF** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="e96d1-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="e96d1-150">Os nomes do Azure Data Factory são **globalmente exclusivos**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="e96d1-151">Você precisará tooprefix nome de Olá Olá da fábrica de dados com seu nome, tooenable Olá êxito na criação da fábrica de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![Novo data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="e96d1-153">Selecione sua **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="e96d1-154">Para **grupo de recursos**, siga um destes Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e96d1-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="e96d1-155">Clique em **criar novo** e insira um nome para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="e96d1-156">Clique em **Usar existente** e selecione um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="e96d1-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="e96d1-157">Selecione Olá **local** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="e96d1-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="e96d1-158">Selecione **toodashboard Pin** para que possa ver fábrica de dados de saudação no painel de saudação próxima vez que você efetuar logon.</span><span class="sxs-lookup"><span data-stu-id="e96d1-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="e96d1-159">Clique em **criar** em Olá **nova fábrica de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="e96d1-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="e96d1-160">Você verá a fábrica de dados hello está sendo criada no hello **painel** de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e96d1-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="e96d1-161">Depois de fábrica de dados Olá tiver sido criada com êxito, você ver a página de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="e96d1-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Home page do Data Factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="e96d1-163">Criar um serviço vinculado do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="e96d1-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="e96d1-164">Depois de criar a fábrica de dados hello, crie um serviço vinculado do SQL Azure que vincula o banco de dados do SQL Azure, que contém a tabela de sampletable hello e procedimento armazenado de sp_sample, tooyour fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="e96d1-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="e96d1-165">Clique em **autor e implantar** em Olá **Data Factory** folha para **SProcDF** toolaunch Olá Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="e96d1-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="e96d1-166">Clique em **novo repositório de dados** Olá barra de comandos e escolha **banco de dados do SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="e96d1-167">Você deve ver Olá script JSON para a criação de um SQL do Azure vinculada serviço no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![Novo armazenamento de dados](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="e96d1-169">No hello script JSON, faça as seguintes alterações de saudação:</span><span class="sxs-lookup"><span data-stu-id="e96d1-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="e96d1-170">Substituir `<servername>` com nome de saudação do seu servidor de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e96d1-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="e96d1-171">Substituir `<databasename>` com banco de dados de saudação em que você criou tabela hello e hello procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="e96d1-172">Substituir `<username@servername>` com conta de usuário de saudação que tem o banco de dados do access toohello.</span><span class="sxs-lookup"><span data-stu-id="e96d1-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="e96d1-173">Substituir `<password>` com senha Olá Olá conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="e96d1-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![Novo armazenamento de dados](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="e96d1-175">toodeploy Olá serviço vinculado, clique em **implantar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="e96d1-176">Confirme que você vê Olá AzureSqlLinkedService na árvore de saudação exibir hello esquerda.</span><span class="sxs-lookup"><span data-stu-id="e96d1-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![modo de exibição de árvore com serviço vinculado](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="e96d1-178">Criar um conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="e96d1-178">Create an output dataset</span></span>
<span data-ttu-id="e96d1-179">Você deve especificar um conjunto de dados de saída para uma atividade de procedimento armazenado mesmo que o procedimento armazenado de saudação não produz nenhum dado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="e96d1-180">Isso ocorre porque Olá seu conjunto de dados que orienta a agenda de saudação da atividade de saudação (frequência hello atividade é executada - hora, diariamente, etc.) de saída.</span><span class="sxs-lookup"><span data-stu-id="e96d1-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="e96d1-181">Olá conjunto de dados de saída deve usar um **serviço vinculado** que se refere a tooan banco de dados do SQL Azure ou um Azure SQL Data Warehouse ou um banco de dados do SQL Server no qual você deseja Olá toorun do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="e96d1-182">Olá conjunto de dados de saída pode servir como um resultado do modo toopass Olá do procedimento armazenado de saudação para processamento subsequente por outra atividade ([encadeamento atividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="e96d1-183">No entanto, fábrica de dados não gravará automaticamente saída Olá de um conjunto de dados do procedimento armazenado toothis.</span><span class="sxs-lookup"><span data-stu-id="e96d1-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="e96d1-184">É Olá tabela gravações tooa SQL que Olá pontos do conjunto de dados de saída de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="e96d1-185">Em alguns casos, o conjunto de dados de saída de hello pode ser um **conjunto de dados fictício** (um conjunto de dados que aponta tooa tabela que não tem saída de hello procedimento armazenado).</span><span class="sxs-lookup"><span data-stu-id="e96d1-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="e96d1-186">Este conjunto de dados fictício é usado somente para atividade de procedimento armazenado de agendamento de saudação toospecify para executar a saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="e96d1-187">Clique em **... Mais** na barra de ferramentas hello, clique em **novo conjunto de dados**e clique em **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="e96d1-188">**Novo conjunto de dados** no comando Olá barra e selecione **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![modo de exibição de árvore com serviço vinculado](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="e96d1-190">Saudação de copiar/colar o script JSON no editor de JSON toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="e96d1-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="e96d1-191">toodeploy Olá conjunto de dados, clique em **implantar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="e96d1-192">Confirme que você vê Olá conjunto de dados na exibição de árvore de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![modo de exibição de árvore com serviços vinculados](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="e96d1-194">Criar um pipeline com atividade de SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="e96d1-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="e96d1-195">Agora, vamos criar um pipeline com uma atividade de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="e96d1-196">Observe Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="e96d1-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="e96d1-197">Olá **tipo** propriedade for definida muito**SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="e96d1-198">Olá **storedProcedureName** no tipo de propriedades está definido muito**sp_sample** (nome da saudação procedimento armazenado).</span><span class="sxs-lookup"><span data-stu-id="e96d1-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="e96d1-199">Olá **storedProcedureParameters** seção contém um parâmetro denominado **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="e96d1-200">Nome e o uso de maiusculas e minúsculas do parâmetro hello em JSON devem corresponder Olá nome e o uso de maiusculas e minúsculas do parâmetro hello na definição do procedimento armazenada de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="e96d1-201">Se você precisar passar null para um parâmetro, use a sintaxe de saudação: `"param1": null` (todas as minúsculas).</span><span class="sxs-lookup"><span data-stu-id="e96d1-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="e96d1-202">Clique em **... Mais** Olá barra de comandos e clique em **novo pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="e96d1-203">Saudação de copiar/colar trecho JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="e96d1-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="e96d1-204">pipeline de saudação toodeploy, clique em **implantar** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="e96d1-205">Pipeline de saudação do monitor</span><span class="sxs-lookup"><span data-stu-id="e96d1-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="e96d1-206">Clique em **X** tooclose Editor da fábrica de dados folhas toonavigate fazer toohello folha de fábrica de dados e clique em **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="e96d1-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![bloco do diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="e96d1-208">Em Olá **exibição de diagrama**, consulte uma visão geral dos pipelines hello e conjuntos de dados usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e96d1-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![bloco do diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="e96d1-210">Na exibição de diagrama de Olá, clique duas vezes em dataset Olá `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="e96d1-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="e96d1-211">Você verá fatias Olá no estado pronto.</span><span class="sxs-lookup"><span data-stu-id="e96d1-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="e96d1-212">Deve haver cinco fatias porque uma fatia é produzida para cada hora entre a hora de início de saudação e a hora de término da saudação JSON.</span><span class="sxs-lookup"><span data-stu-id="e96d1-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![bloco do diagrama](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="e96d1-214">Quando uma fatia está em **pronto** estado, execute uma `select * from sampletable` consulta Olá tooverify de banco de dados de SQL do Azure que Olá dados foi inserida na tabela de toohello pelo procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![Dados de saída](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="e96d1-216">Consulte [pipeline de saudação do Monitor](data-factory-monitor-manage-pipelines.md) para obter informações detalhadas sobre o monitoramento do Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="e96d1-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="e96d1-217">Especificar um conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="e96d1-217">Specify an input dataset</span></span>
<span data-ttu-id="e96d1-218">Passo a passo hello, atividade de procedimento armazenado não tem quaisquer conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="e96d1-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="e96d1-219">Se você especificar um conjunto de dados de entrada, hello atividade de procedimento armazenado não será executado até que a fatia de saudação do conjunto de dados de entrada está disponível (no estado pronto).</span><span class="sxs-lookup"><span data-stu-id="e96d1-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="e96d1-220">saudação de conjunto de dados pode ser um conjunto de dados externo (que não é produzido por outra atividade no hello mesmo pipeline) ou um conjunto de dados interno que é produzido por uma atividade de upstream (atividade de saudação executada antes que essa atividade).</span><span class="sxs-lookup"><span data-stu-id="e96d1-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="e96d1-221">Você pode especificar vários conjuntos de dados de entrada para a atividade de procedimento armazenada de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="e96d1-222">Se você fizer isso, hello atividade de procedimento armazenado é executado somente quando todas as fatias de conjunto de dados de entrada hello estão disponíveis (no estado pronto).</span><span class="sxs-lookup"><span data-stu-id="e96d1-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="e96d1-223">Olá conjunto de dados de entrada não pode ser consumido no procedimento Olá armazenado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e96d1-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="e96d1-224">É apenas dependência de saudação toocheck usado antes de atividade de procedimento armazenado de saudação inicial.</span><span class="sxs-lookup"><span data-stu-id="e96d1-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="e96d1-225">Encadeando com outras atividades</span><span class="sxs-lookup"><span data-stu-id="e96d1-225">Chaining with other activities</span></span>
<span data-ttu-id="e96d1-226">Se você quiser toochain uma atividade de upstream com essa atividade, Especifica saída de saudação da atividade de upstream hello como uma entrada dessa atividade.</span><span class="sxs-lookup"><span data-stu-id="e96d1-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="e96d1-227">Quando você fizer isso, hello atividade de procedimento armazenado não executado até a conclusão da atividade de upstream hello e Olá o conjunto de dados de saída da atividade de upstream hello está disponível (em status Pronto).</span><span class="sxs-lookup"><span data-stu-id="e96d1-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="e96d1-228">Você pode especificar conjuntos de dados de saída de várias atividades de upstream como conjuntos de dados de entrada da atividade de procedimento armazenada de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="e96d1-229">Ao fazer isso, a atividade de procedimento armazenado de saudação é executado somente quando todas as fatias de conjunto de dados de entrada hello estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e96d1-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="e96d1-230">No hello exemplo a seguir, a saída de saudação da atividade de cópia de saudação é: atividade de procedimento armazenado de OutputDataset, que é uma entrada de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="e96d1-231">Portanto, hello atividade de procedimento armazenado não será executado até hello atividade de cópia é concluída e a fatia de OutputDataset hello está disponível (no estado pronto).</span><span class="sxs-lookup"><span data-stu-id="e96d1-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="e96d1-232">Se você especificar vários conjuntos de dados de entrada, hello atividade de procedimento armazenado não será executado até que todas as fatias de conjunto de dados de entrada hello estão disponíveis (no estado pronto).</span><span class="sxs-lookup"><span data-stu-id="e96d1-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="e96d1-233">Olá conjuntos de dados de entrada não podem ser usados diretamente como atividade de procedimento armazenado de toohello de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e96d1-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="e96d1-234">Para obter mais informações sobre atividades de encadeamento, consulte [várias atividades em um pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="e96d1-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="e96d1-235">Da mesma forma, toolink Olá repositório de atividade de procedimento com **atividades downstream** (Olá as atividades que executam após hello atividade de procedimento armazenado), especifique Olá o conjunto de dados de saída da atividade de procedimento Olá armazenado como um entrada de atividade de downstream Olá no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e96d1-236">Ao copiar dados em um banco de dados do SQL Azure ou o SQL Server, você pode configurar Olá **SqlSink** na atividade de cópia tooinvoke um procedimento armazenado usando Olá **sqlWriterStoredProcedureName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="e96d1-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="e96d1-237">Para obter mais informações, consulte [Invocar um procedimento armazenado por meio da atividade de cópia](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="e96d1-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="e96d1-238">Para obter detalhes sobre a propriedade hello, consulte Olá seguintes artigos de conector: [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [do SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e96d1-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="e96d1-239">Ao copiar dados de banco de dados do SQL Azure ou o SQL Server ou o Azure SQL Data Warehouse, você pode configurar **SqlSource** na atividade de cópia tooinvoke um procedimento armazenado tooread os dados de banco de dados de origem de saudação usando Olá  **sqlReaderStoredProcedureName** propriedade.</span><span class="sxs-lookup"><span data-stu-id="e96d1-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="e96d1-240">Para obter mais informações, consulte Olá seguintes artigos de conector: [banco de dados do SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [do SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="e96d1-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="e96d1-241">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="e96d1-241">JSON format</span></span>
<span data-ttu-id="e96d1-242">Este é o formato JSON de saudação para definir uma atividade de procedimento armazenado:</span><span class="sxs-lookup"><span data-stu-id="e96d1-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="e96d1-243">Olá, a tabela a seguir descreve as propriedades JSON:</span><span class="sxs-lookup"><span data-stu-id="e96d1-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="e96d1-244">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e96d1-244">Property</span></span> | <span data-ttu-id="e96d1-245">Descrição</span><span class="sxs-lookup"><span data-stu-id="e96d1-245">Description</span></span> | <span data-ttu-id="e96d1-246">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e96d1-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e96d1-247">name</span><span class="sxs-lookup"><span data-stu-id="e96d1-247">name</span></span> | <span data-ttu-id="e96d1-248">Nome da atividade de saudação</span><span class="sxs-lookup"><span data-stu-id="e96d1-248">Name of hello activity</span></span> |<span data-ttu-id="e96d1-249">Sim</span><span class="sxs-lookup"><span data-stu-id="e96d1-249">Yes</span></span> |
| <span data-ttu-id="e96d1-250">description</span><span class="sxs-lookup"><span data-stu-id="e96d1-250">description</span></span> |<span data-ttu-id="e96d1-251">Texto que descreve quais atividade Olá é usada para</span><span class="sxs-lookup"><span data-stu-id="e96d1-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="e96d1-252">Não</span><span class="sxs-lookup"><span data-stu-id="e96d1-252">No</span></span> |
| <span data-ttu-id="e96d1-253">type</span><span class="sxs-lookup"><span data-stu-id="e96d1-253">type</span></span> | <span data-ttu-id="e96d1-254">Deve ser definido como: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="e96d1-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="e96d1-255">Sim</span><span class="sxs-lookup"><span data-stu-id="e96d1-255">Yes</span></span> |
| <span data-ttu-id="e96d1-256">inputs</span><span class="sxs-lookup"><span data-stu-id="e96d1-256">inputs</span></span> | <span data-ttu-id="e96d1-257">Opcional.</span><span class="sxs-lookup"><span data-stu-id="e96d1-257">Optional.</span></span> <span data-ttu-id="e96d1-258">Se você especificar um conjunto de dados de entrada, ele deve estar disponível (em status 'Pronto') para Olá armazenados toorun de atividade de procedimento.</span><span class="sxs-lookup"><span data-stu-id="e96d1-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="e96d1-259">Olá conjunto de dados de entrada não pode ser consumido no procedimento Olá armazenado como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e96d1-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="e96d1-260">É apenas dependência de saudação toocheck usado antes de atividade de procedimento armazenado de saudação inicial.</span><span class="sxs-lookup"><span data-stu-id="e96d1-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="e96d1-261">Não</span><span class="sxs-lookup"><span data-stu-id="e96d1-261">No</span></span> |
| <span data-ttu-id="e96d1-262">outputs</span><span class="sxs-lookup"><span data-stu-id="e96d1-262">outputs</span></span> | <span data-ttu-id="e96d1-263">Você deve especificar um conjunto de dados de saída para uma atividade de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="e96d1-264">Conjunto de dados de saída especifica Olá **agenda** para Olá armazenados atividade de procedimento (por hora, semanalmente, mensalmente, etc.).</span><span class="sxs-lookup"><span data-stu-id="e96d1-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="e96d1-265">Olá conjunto de dados de saída deve usar um **serviço vinculado** que se refere a tooan banco de dados do SQL Azure ou um Azure SQL Data Warehouse ou um banco de dados do SQL Server no qual você deseja Olá toorun do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="e96d1-266">Olá conjunto de dados de saída pode servir como um resultado do modo toopass Olá do procedimento armazenado de saudação para processamento subsequente por outra atividade ([encadeamento atividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="e96d1-267">No entanto, fábrica de dados não gravará automaticamente saída Olá de um conjunto de dados do procedimento armazenado toothis.</span><span class="sxs-lookup"><span data-stu-id="e96d1-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="e96d1-268">É Olá tabela gravações tooa SQL que Olá pontos do conjunto de dados de saída de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="e96d1-269">Em alguns casos, o conjunto de dados de saída de hello pode ser um **conjunto de dados fictício**, que é usado somente para atividade de procedimento armazenado de agendamento de saudação toospecify para executar a saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="e96d1-270">Sim</span><span class="sxs-lookup"><span data-stu-id="e96d1-270">Yes</span></span> |
| <span data-ttu-id="e96d1-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="e96d1-271">storedProcedureName</span></span> |<span data-ttu-id="e96d1-272">Especifique o nome de saudação do procedimento de saudação armazenado no banco de dados do SQL Azure hello ou banco de dados Azure SQL Data Warehouse ou o SQL Server que é representado pelo serviço Olá vinculado que Olá usos da tabela de saída.</span><span class="sxs-lookup"><span data-stu-id="e96d1-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="e96d1-273">Sim</span><span class="sxs-lookup"><span data-stu-id="e96d1-273">Yes</span></span> |
| <span data-ttu-id="e96d1-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e96d1-274">storedProcedureParameters</span></span> |<span data-ttu-id="e96d1-275">Especifique valores para parâmetros de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="e96d1-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="e96d1-276">Se você precisar toopass nulo para um parâmetro, use a sintaxe de saudação: "param1": null (todas as letras minúsculas).</span><span class="sxs-lookup"><span data-stu-id="e96d1-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="e96d1-277">Consulte Olá toolearn de exemplo sobre como usar essa propriedade a seguir.</span><span class="sxs-lookup"><span data-stu-id="e96d1-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="e96d1-278">Não</span><span class="sxs-lookup"><span data-stu-id="e96d1-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="e96d1-279">Passando um valor estático</span><span class="sxs-lookup"><span data-stu-id="e96d1-279">Passing a static value</span></span>
<span data-ttu-id="e96d1-280">Agora, vamos considerar adicionar outra coluna denominada 'Cenário' na tabela de saudação que contém um valor estático chamado 'Exemplo de documento'.</span><span class="sxs-lookup"><span data-stu-id="e96d1-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![Dados de exemplo 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="e96d1-282">**Tabela:**</span><span class="sxs-lookup"><span data-stu-id="e96d1-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="e96d1-283">**Procedimento armazenado:**</span><span class="sxs-lookup"><span data-stu-id="e96d1-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="e96d1-284">Agora, passar Olá **cenário** atividade de procedimento armazenado do valor de parâmetro e hello da saudação.</span><span class="sxs-lookup"><span data-stu-id="e96d1-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="e96d1-285">Olá **typeProperties** seção Olá anterior exemplo parece Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e96d1-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="e96d1-286">**Conjunto de dados do Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="e96d1-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="e96d1-287">**Pipeline do Data Factory**</span><span class="sxs-lookup"><span data-stu-id="e96d1-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```