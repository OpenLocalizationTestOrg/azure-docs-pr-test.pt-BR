---
title: dados de aaaCopy do armazenamento de Blob tooSQL banco de dados - Azure | Microsoft Docs
description: "Este tutorial mostra como toouse atividade de cópia em uma fábrica de dados do Azure pipeline toocopy dados do banco de dados de tooSQL de armazenamento de Blob."
keywords: "sql para blob, armazenamento de blobs, cópia de dados"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="afc01-104">Tutorial: Copiar dados de armazenamento de Blob tooSQL banco de dados usando a fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="afc01-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afc01-105">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="afc01-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="afc01-106">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="afc01-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="afc01-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="afc01-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="afc01-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afc01-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="afc01-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afc01-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="afc01-110">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="afc01-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="afc01-111">API REST</span><span class="sxs-lookup"><span data-stu-id="afc01-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="afc01-112">API do .NET</span><span class="sxs-lookup"><span data-stu-id="afc01-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="afc01-113">Neste tutorial, você pode criar uma fábrica de dados com um pipeline toocopy do banco de dados Blob armazenamento tooSQL.</span><span class="sxs-lookup"><span data-stu-id="afc01-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="afc01-114">Hello atividade de cópia realiza a movimentação de dados Olá na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="afc01-115">Ela é habilitada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="afc01-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="afc01-116">Consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre hello atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="afc01-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="afc01-117">Para obter uma visão geral detalhada da saudação serviço da fábrica de dados, consulte Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="afc01-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="afc01-118">Pré-requisitos para o tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="afc01-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="afc01-119">Antes de começar este tutorial, você deve ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="afc01-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="afc01-120">**Assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="afc01-120">**Azure subscription**.</span></span>  <span data-ttu-id="afc01-121">Se você não tiver uma assinatura, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="afc01-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="afc01-122">Consulte Olá [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="afc01-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="afc01-123">**Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="afc01-123">**Azure Storage Account**.</span></span> <span data-ttu-id="afc01-124">Use o armazenamento de blob hello como um **fonte** repositório de dados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="afc01-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="afc01-125">Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo para toocreate etapas um.</span><span class="sxs-lookup"><span data-stu-id="afc01-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="afc01-126">**Banco de dados SQL do Azure**.</span><span class="sxs-lookup"><span data-stu-id="afc01-126">**Azure SQL Database**.</span></span> <span data-ttu-id="afc01-127">Você usa um banco de dados SQL do Azure como um armazenamento de dados de **destino** neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="afc01-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="afc01-128">Se você não tiver um banco de dados SQL do Azure que você pode usar o tutorial hello, consulte [como toocreate e configurar um banco de dados do SQL Azure](../sql-database/sql-database-get-started.md) toocreate um.</span><span class="sxs-lookup"><span data-stu-id="afc01-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="afc01-129">**SQL Server 2012/2014 ou Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="afc01-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="afc01-130">Use o SQL Server Management Studio ou Visual Studio toocreate um banco de dados de exemplo e os dados de resultado de saudação tooview no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="afc01-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="afc01-131">Coletar o nome e a chave da conta de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="afc01-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="afc01-132">Você precisa conta Olá chave de nome e a conta do armazenamento do Azure conta toodo neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="afc01-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="afc01-133">Anote o **nome da conta** e a **chave de conta** da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="afc01-134">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="afc01-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="afc01-135">Clique em **mais serviços** em Olá deixado menu e selecione **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="afc01-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    ![Procurar - Contas de armazenamento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="afc01-137">Em Olá **contas de armazenamento** folha, selecione Olá **conta de armazenamento do Azure** que você deseja toouse neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="afc01-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="afc01-138">Selecione o link **Chaves de acesso** em **CONFIGURAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="afc01-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="afc01-139">Clique em **cópia** (imagem) botão Avançar muito**nome da conta de armazenamento** texto caixa e salvar/colá-lo em algum lugar (por exemplo: em um arquivo de texto).</span><span class="sxs-lookup"><span data-stu-id="afc01-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="afc01-140">Repetir Olá toocopy de etapa anterior ou anote Olá **key1**.</span><span class="sxs-lookup"><span data-stu-id="afc01-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![Chave de acesso de armazenamento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="afc01-142">Feche todas as folhas de saudação clicando **X**.</span><span class="sxs-lookup"><span data-stu-id="afc01-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="afc01-143">Coletar o servidor SQL, o banco de dados, os nomes de usuário</span><span class="sxs-lookup"><span data-stu-id="afc01-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="afc01-144">Neste tutorial você precisa de nomes de saudação do servidor, banco de dados e toodo de usuário do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="afc01-145">Anote os nomes do **servidor**, **banco de dados** e **usuário** para seu banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="afc01-146">Em Olá **portal do Azure**, clique em **mais serviços** em Olá esquerdo e selecione **bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="afc01-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="afc01-147">Em Olá **folha de bancos de dados SQL**, selecione Olá **banco de dados** que você deseja toouse neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="afc01-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="afc01-148">Anote Olá **nome do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="afc01-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="afc01-149">Em Olá **banco de dados SQL** folha, clique em **propriedades** em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="afc01-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="afc01-150">Anote os valores hello para **nome do servidor** e **logon de administrador de servidor**.</span><span class="sxs-lookup"><span data-stu-id="afc01-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="afc01-151">Feche todas as folhas de saudação clicando **X**.</span><span class="sxs-lookup"><span data-stu-id="afc01-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="afc01-152">Permitir que os serviços do Azure tooaccess SQL server</span><span class="sxs-lookup"><span data-stu-id="afc01-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="afc01-153">Certifique-se de que **permitir acesso a serviços tooAzure** configuração desativado **ON** para o servidor do SQL Azure para esse serviço da fábrica de dados Olá possa acessar seu servidor do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="afc01-154">tooverify e ativar essa configuração, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="afc01-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="afc01-155">Clique em **mais serviços** hub no hello esquerda e clique em **servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="afc01-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="afc01-156">Selecione seu servidor e clique em **Firewall** em **CONFIGURAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="afc01-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="afc01-157">Em Olá **configurações de Firewall** folha, clique em **ON** para **permitir acesso a serviços tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="afc01-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="afc01-158">Feche todas as folhas de saudação clicando **X**.</span><span class="sxs-lookup"><span data-stu-id="afc01-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="afc01-159">Preparar o Armazenamento de Blobs e o banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="afc01-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="afc01-160">Agora, prepare o armazenamento de BLOBs do Azure e o banco de dados SQL do Azure para tutorial Olá executando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="afc01-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="afc01-161">Inicie o Bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="afc01-161">Launch Notepad.</span></span> <span data-ttu-id="afc01-162">Copie Olá texto a seguir e salve-o como **emp.txt** muito**C:\ADFGetStarted** pasta no disco rígido.</span><span class="sxs-lookup"><span data-stu-id="afc01-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="afc01-163">Use ferramentas como [Azure Storage Explorer](http://storageexplorer.com/) toocreate Olá **adftutorial** Olá contêiner e tooupload **emp.txt** arquivo toohello recipiente.</span><span class="sxs-lookup"><span data-stu-id="afc01-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Gerenciador de Armazenamento do Azure.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="afc01-166">Olá Use Olá de toocreate de script SQL a seguir **emp** tabela no banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="afc01-167">**Se você tiver instalado no computador do SQL Server 2012/2014:** siga as instruções de [gerenciamento de banco de dados SQL usando o SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour script SQL de saudação de servidor e execução de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="afc01-168">Este artigo usa Olá [portal clássico do Azure](http://manage.windowsazure.com), Olá não [novo portal do Azure](https://portal.azure.com), tooconfigure firewall para um servidor do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="afc01-169">Se o cliente não é permitido tooaccess hello Azure do SQL server, será necessário tooconfigure firewall para o acesso ao SQL Azure server tooallow em seu computador (endereço IP).</span><span class="sxs-lookup"><span data-stu-id="afc01-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="afc01-170">Consulte [neste artigo](../sql-database/sql-database-configure-firewall-settings.md) firewall de saudação tooconfigure etapas para o servidor do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="afc01-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="afc01-171">Criar uma data factory</span><span class="sxs-lookup"><span data-stu-id="afc01-171">Create a data factory</span></span>
<span data-ttu-id="afc01-172">Você concluiu os pré-requisitos de saudação.</span><span class="sxs-lookup"><span data-stu-id="afc01-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="afc01-173">Você pode criar uma fábrica de dados usando uma das maneiras a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="afc01-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="afc01-174">Clique em uma das opções de saudação na lista suspensa de saudação na superior de saudação ou Olá seguir links tooperform Olá tutorial.</span><span class="sxs-lookup"><span data-stu-id="afc01-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="afc01-175">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="afc01-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="afc01-176">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="afc01-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="afc01-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afc01-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="afc01-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afc01-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="afc01-179">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="afc01-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="afc01-180">API REST</span><span class="sxs-lookup"><span data-stu-id="afc01-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="afc01-181">API do .NET</span><span class="sxs-lookup"><span data-stu-id="afc01-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="afc01-182">pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="afc01-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="afc01-183">Ela não transforma dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="afc01-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="afc01-184">Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie sua primeira pipeline tootransform de dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="afc01-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="afc01-185">É possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="afc01-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="afc01-186">Veja [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="afc01-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
