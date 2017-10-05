---
title: Copiar dados do Armazenamento de Blobs para o Banco de Dados SQL - Azure | Microsoft Docs
description: "Este tutorial mostra como usar a Atividade de Cópia em um pipeline do Azure Data Factory para copiar dados do Armazenamento de Blobs para um banco de dados SQL."
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
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="0ef8f-104">Tutorial: copiar dados do Armazenamento de Blobs para o Banco de Dados SQL usando o Data Factory</span><span class="sxs-lookup"><span data-stu-id="0ef8f-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ef8f-105">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0ef8f-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="0ef8f-106">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="0ef8f-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="0ef8f-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0ef8f-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="0ef8f-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ef8f-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="0ef8f-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ef8f-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="0ef8f-110">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0ef8f-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="0ef8f-111">API REST</span><span class="sxs-lookup"><span data-stu-id="0ef8f-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="0ef8f-112">API do .NET</span><span class="sxs-lookup"><span data-stu-id="0ef8f-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="0ef8f-113">Neste tutorial, você cria um data factory com um pipeline para copiar dados do Armazenamento de Blobs para o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="0ef8f-114">A atividade de cópia realiza a movimentação de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="0ef8f-115">Ela é habilitada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="0ef8f-116">Veja o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) para obter detalhes sobre a Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="0ef8f-117">Para obter uma visão geral detalhada do serviço Data Factory, veja o artigo [Introdução à Azure Data Factory](data-factory-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="0ef8f-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="0ef8f-118">Pré-requisitos para o tutorial</span><span class="sxs-lookup"><span data-stu-id="0ef8f-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="0ef8f-119">Antes de iniciar este tutorial, você deverá ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="0ef8f-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="0ef8f-120">**Assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-120">**Azure subscription**.</span></span>  <span data-ttu-id="0ef8f-121">Se você não tiver uma assinatura, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0ef8f-122">Consulte o artigo [Avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="0ef8f-123">**Conta de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-123">**Azure Storage Account**.</span></span> <span data-ttu-id="0ef8f-124">Você usa o armazenamento de blobs como um armazenamento de dados de **origem** dados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="0ef8f-125">Se você não tiver uma conta de armazenamento do Azure, veja o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para conhecer as etapas para criar um.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="0ef8f-126">**Banco de dados SQL do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-126">**Azure SQL Database**.</span></span> <span data-ttu-id="0ef8f-127">Você usa um banco de dados SQL do Azure como um armazenamento de dados de **destino** neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="0ef8f-128">Se você não tiver um banco de dados do SQL Azure que você possa usar no tutorial, consulte [Como criar e configurar um banco de dados SQL do Azure](../sql-database/sql-database-get-started.md) para criar um.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="0ef8f-129">**SQL Server 2012/2014 ou Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="0ef8f-130">Você usa SQL Server Management Studio ou Visual Studio para criar um banco de dados de exemplo e exibir os dados de resultado no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="0ef8f-131">Coletar o nome e a chave da conta de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="0ef8f-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="0ef8f-132">Você precisa do nome da conta e chave de conta da sua conta de armazenamento do Azure para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="0ef8f-133">Anote o **nome da conta** e a **chave de conta** da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="0ef8f-134">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0ef8f-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0ef8f-135">Clique em **Mais serviços** no menu à esquerda e selecione **Contas de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![Procurar - Contas de armazenamento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="0ef8f-137">Na folha **Contas de armazenamento**, selecione a **Conta de armazenamento do Azure** que você deseja usar neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="0ef8f-138">Selecione o link **Chaves de acesso** em **CONFIGURAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="0ef8f-139">Clique no botão **copiar** (imagem) ao lado da caixa de texto **Nome da conta de armazenamento** e salve-a/cole-a em algum lugar (por exemplo, em um arquivo de texto).</span><span class="sxs-lookup"><span data-stu-id="0ef8f-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="0ef8f-140">Repita a etapa anterior para copiar ou anote a **chave1**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Chave de acesso de armazenamento](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="0ef8f-142">Feche todas as folhas, clicando em **X**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="0ef8f-143">Coletar o servidor SQL, o banco de dados, os nomes de usuário</span><span class="sxs-lookup"><span data-stu-id="0ef8f-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="0ef8f-144">Você precisa dos nomes do servidor, banco de dados e usuário SQL do Azure para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="0ef8f-145">Anote os nomes do **servidor**, **banco de dados** e **usuário** para seu banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="0ef8f-146">No **Portal do Azure**, clique em **Mais serviços** à esquerda e selecione **Bancos de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="0ef8f-147">Na **folha Bancos de dados SQL**, clique no **banco de dados** que você deseja utilizar neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="0ef8f-148">Anote o **nome do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="0ef8f-149">Em seguida, na folha **Banco de dados SQL**, clique em **Propriedades** em **CONFIGURAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="0ef8f-150">Anote os valores para **NOME DO SERVIDOR** e **LOGON DE ADMINISTRADOR DO SERVIDOR**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="0ef8f-151">Feche todas as folhas, clicando em **X**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="0ef8f-152">Permitir que os serviços do Azure acessem o servidor</span><span class="sxs-lookup"><span data-stu-id="0ef8f-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="0ef8f-153">Certifique-se de a configuração **Permitir acesso aos serviços do Azure** esteja definida como **ATIVADA** para o servidor do SQL Azure, para que o serviço Data Factory possa acessar seu SQL Server do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="0ef8f-154">Para verificar e ativar essa configuração, faça as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0ef8f-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="0ef8f-155">Clique no hub **Mais serviços** à esquerda e clique em **Servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="0ef8f-156">Selecione seu servidor e clique em **Firewall** em **CONFIGURAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="0ef8f-157">Na folha **Configurações de Firewall**, clique em **ATIVADO** para **Permitir acesso aos serviços do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="0ef8f-158">Feche todas as folhas, clicando em **X**.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="0ef8f-159">Preparar o Armazenamento de Blobs e o banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="0ef8f-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="0ef8f-160">Agora, prepare seu armazenamento de blob do Azure e o banco de dados SQL do Azure para o tutorial, executando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0ef8f-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="0ef8f-161">Inicie o Bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-161">Launch Notepad.</span></span> <span data-ttu-id="0ef8f-162">Copie o texto a seguir e salve-o como **emp.txt** na pasta **C:\ADFGetStarted** em seu disco rígido.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="0ef8f-163">Use ferramentas como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/) para criar o contêiner **adftutorial** e carregar o arquivo **emp.txt** no contêiner.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Gerenciador de Armazenamento do Azure.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="0ef8f-166">Use o script SQL a seguir para criar a tabela **emp** no seu Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="0ef8f-167">**Se você tiver o SQL Server 2012/2014 instalado no computador:** siga as instruções em [Gerenciando o Banco de Dados SQL do Azure usando o SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) para se conectar ao servidor SQL do Azure e executar o script SQL.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="0ef8f-168">Este artigo usa o [portal clássico do Azure](http://manage.windowsazure.com), não o [novo portal do Azure](https://portal.azure.com), para configurar um firewall para um SQL Server do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="0ef8f-169">Se o cliente não tiver permissão para acessar o servidor SQL do Azure, você precisará configurar o firewall para o servidor SQL do Azure permitir o acesso no seu computador (endereço IP).</span><span class="sxs-lookup"><span data-stu-id="0ef8f-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="0ef8f-170">Veja [este artigo](../sql-database/sql-database-configure-firewall-settings.md) para obter as etapas para configurar o firewall para o SQL Server do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="0ef8f-171">Criar uma data factory</span><span class="sxs-lookup"><span data-stu-id="0ef8f-171">Create a data factory</span></span>
<span data-ttu-id="0ef8f-172">Você concluiu os pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-172">You have completed the prerequisites.</span></span> <span data-ttu-id="0ef8f-173">Você pode criar um data factory usando um dos caminhos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="0ef8f-174">Clique em uma das opções na lista suspensa na parte superior ou nos links a seguir para executar o tutorial.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="0ef8f-175">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="0ef8f-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="0ef8f-176">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0ef8f-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="0ef8f-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ef8f-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="0ef8f-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ef8f-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="0ef8f-179">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0ef8f-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="0ef8f-180">API REST</span><span class="sxs-lookup"><span data-stu-id="0ef8f-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="0ef8f-181">API do .NET</span><span class="sxs-lookup"><span data-stu-id="0ef8f-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="0ef8f-182">O pipeline de dados neste tutorial copia os dados de um armazenamento de dados de origem para um armazenamento de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="0ef8f-183">Ele não transforma dados de entrada para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="0ef8f-184">Para obter um tutorial sobre como transformar dados usando o Azure Data Factory, confira [Tutorial: criar seu primeiro pipeline para transformar dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="0ef8f-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="0ef8f-185">É possível encadear duas atividades (executar uma atividade após a outra) definindo o conjunto de dados de saída de uma atividade como o conjunto de dados de entrada da outra atividade.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="0ef8f-186">Confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="0ef8f-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
