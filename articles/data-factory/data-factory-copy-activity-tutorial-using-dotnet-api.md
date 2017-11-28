---
title: "Tutorial: criar um pipeline com Atividade de Cópia usando a API .NET | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline do Azure Data Factory com uma Atividade de Cópia usando a REST .NET."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="b8ea5-103">Tutorial: criar um pipeline com Atividade de Cópia usando a API .NET</span><span class="sxs-lookup"><span data-stu-id="b8ea5-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8ea5-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b8ea5-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="b8ea5-105">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="b8ea5-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="b8ea5-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b8ea5-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="b8ea5-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8ea5-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="b8ea5-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8ea5-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="b8ea5-109">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b8ea5-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="b8ea5-110">API REST</span><span class="sxs-lookup"><span data-stu-id="b8ea5-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="b8ea5-111">API do .NET</span><span class="sxs-lookup"><span data-stu-id="b8ea5-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="b8ea5-112">Neste artigo, você aprenderá como toouse [API .NET](https://portal.azure.com) toocreate uma fábrica de dados com um pipeline que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="b8ea5-113">Se você estiver tooAzure nova fábrica de dados, leia Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo antes de fazer este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="b8ea5-114">Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="b8ea5-115">Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="b8ea5-116">Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b8ea5-117">atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="b8ea5-118">Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="b8ea5-119">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="b8ea5-120">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="b8ea5-121">Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="b8ea5-122">Confira [Referência da API do .NET do Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) para obter uma documentação abrangente sobre a API do .NET do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="b8ea5-123">pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="b8ea5-124">Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8ea5-125">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b8ea5-125">Prerequisites</span></span>
* <span data-ttu-id="b8ea5-126">Passar [Tutorial visão geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget uma visão geral do tutorial hello e hello completa **pré-requisito** etapas.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="b8ea5-127">Visual Studio 2012 ou 2013 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="b8ea5-128">Baixar e instalar o [SDK .NET do Azure](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b8ea5-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="b8ea5-129">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-129">Azure PowerShell.</span></span> <span data-ttu-id="b8ea5-130">Siga as instruções em [como tooinstall e configurar o Azure PowerShell](../powershell-install-configure.md) artigo tooinstall PowerShell do Azure no seu computador.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="b8ea5-131">Use o Azure PowerShell toocreate um aplicativo do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="b8ea5-132">Criar um aplicativo no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8ea5-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="b8ea5-133">Criar um aplicativo do Active Directory do Azure, criar uma entidade de serviço para o aplicativo hello e atribuí-la toohello **colaborador da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="b8ea5-134">Inicie o **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="b8ea5-135">Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="b8ea5-136">Execute Olá tooview de comando a seguir todas as assinaturas de saudação para esta conta.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="b8ea5-137">Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="b8ea5-138">Substituir  **&lt;NameOfAzureSubscription** &gt; com o nome da saudação de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="b8ea5-139">Anote **SubscriptionId** e **TenantId** da saída de hello desse comando.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="b8ea5-140">Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando de saudação do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="b8ea5-141">Se o grupo de recursos Olá já existe, especifique se tooupdate-lo (Y) ou mantê-lo como (N).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="b8ea5-142">Se você usar um grupo de recursos diferentes, você precisa toouse nome de saudação do seu grupo de recursos no lugar de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="b8ea5-143">Criar um aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="b8ea5-144">Se você obtiver Olá erro a seguir, especifique uma URL diferente e execute o comando Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="b8ea5-145">Crie hello entidade de serviço do AD.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="b8ea5-146">Adicionar toohello principal do serviço **colaborador da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="b8ea5-147">Obter a ID do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="b8ea5-148">Anote a ID do aplicativo hello (applicationID) de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="b8ea5-149">Você deve ter quatro valores após estas etapas:</span><span class="sxs-lookup"><span data-stu-id="b8ea5-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="b8ea5-150">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="b8ea5-150">Tenant ID</span></span>
* <span data-ttu-id="b8ea5-151">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="b8ea5-151">Subscription ID</span></span>
* <span data-ttu-id="b8ea5-152">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b8ea5-152">Application ID</span></span>
* <span data-ttu-id="b8ea5-153">Senha (especificada no comando primeiro Olá)</span><span class="sxs-lookup"><span data-stu-id="b8ea5-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="b8ea5-154">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="b8ea5-154">Walkthrough</span></span>
1. <span data-ttu-id="b8ea5-155">Usando o Visual Studio 2012/2013/2015, crie um aplicativo de console C# .NET.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="b8ea5-156">Inicie o **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="b8ea5-157">Clique em **arquivo**, ponto muito**novo**e clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="b8ea5-158">Expanda **Modelos** e selecione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="b8ea5-159">Neste passo a passo, você usa C#, mas você pode usar qualquer linguagem .NET.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="b8ea5-160">Selecione **aplicativo de Console** da lista de saudação de tipos de projeto em saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="b8ea5-161">Digite **DataFactoryAPITestApp** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="b8ea5-162">Selecione **C:\ADFGetStarted** para Olá local.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="b8ea5-163">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="b8ea5-164">Clique em **ferramentas**, ponto muito**NuGet Package Manager**e clique em **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="b8ea5-165">Em Olá **Package Manager Console**, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b8ea5-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="b8ea5-166">Execute Olá pacote do comando tooinstall fábrica de dados a seguir:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="b8ea5-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="b8ea5-167">Execute Olá pacote de Active Directory do Azure tooinstall de comando (use a API do Active Directory em código Olá) a seguir:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="b8ea5-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="b8ea5-168">Adicione o seguinte Olá **appSetttings** seção toohello **App. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="b8ea5-169">Essas configurações são usadas pelo método auxiliar de saudação: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="b8ea5-170">Substitua os valores de **&lt;ID do aplicativo&gt;**, **&lt;Senha&gt;**, **&lt;ID da assinatura&gt;** e **&lt;ID do locatário&gt;** pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```

5. <span data-ttu-id="b8ea5-171">Adicione o seguinte Olá **usando** arquivo de origem toohello instruções (Program.cs) no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```

6. <span data-ttu-id="b8ea5-172">Adicionar Olá seguindo o código que cria uma instância de **DataPipelineManagementClient** classe toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="b8ea5-173">Você usar esse objeto toocreate uma fábrica de dados, um serviço vinculado, conjuntos de dados de entrada e saídos e um pipeline.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="b8ea5-174">Você também pode usar este fatias de toomonitor de objeto de um conjunto de dados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="b8ea5-175">Substituir valor de saudação do **resourceGroupName** com nome de saudação do seu grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="b8ea5-176">Atualize o nome da saudação dados fábrica (dataFactoryName) toobe exclusivo.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="b8ea5-177">Nome da fábrica de dados Olá deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="b8ea5-178">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="b8ea5-179">Adicionar Olá seguindo o código que cria um **fábrica de dados** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```

    <span data-ttu-id="b8ea5-180">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="b8ea5-181">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="b8ea5-182">Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de saída de tooproduct dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="b8ea5-183">Vamos começar com a criação de fábrica de dados Olá nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="b8ea5-184">Adicionar Olá seguindo o código que cria um **serviço vinculado do armazenamento do Azure** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b8ea5-185">Substitua **storageaccountname** e **accountkey** pelo nome e pela chave da sua conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```

    <span data-ttu-id="b8ea5-186">Você pode criar serviços vinculados em um toolink de fábrica de dados seus dados, armazena e fábrica de dados toohello de serviços de computação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="b8ea5-187">Neste tutorial, você não usa serviços de computação, como o Azure HDInsight ou o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="b8ea5-188">Você usa dois armazenamentos de dados do tipo Armazenamento do Azure (origem) e o banco de dados SQL (destino).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="b8ea5-189">Portanto, você pode criar dois serviços vinculados, chamados AzureStorageLinkedService e AzureSqlLinkedService, dos tipos: AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="b8ea5-190">Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="b8ea5-191">Esta conta de armazenamento é hello um no qual você criou um contêiner e carregou dados de saudação como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="b8ea5-192">Adicionar Olá seguindo o código que cria um **serviço vinculado do SQL Azure** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b8ea5-193">Substitua **servername**, **databasename**, **username** e **password** pelos nomes de seu servidor SQL do Azure, banco de dados, usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="b8ea5-194">AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="b8ea5-195">Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="b8ea5-196">Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="b8ea5-197">Adicionar Olá código que cria a seguir **conjuntos de dados de entrada e saídos** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },

                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
                    },
                    Availability = new Availability()
                    {
                        Frequency = SchedulePeriod.Hour,
                        Interval = 1,
                    },
                }
            }
        });
    ```
    
    <span data-ttu-id="b8ea5-198">Na etapa anterior de saudação, você criou serviços vinculados toolink sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="b8ea5-199">Nesta etapa, você definirá dois conjuntos de dados denominados InputDataset OutputDataset que representam a entrada e saída dados e que são armazenados em repositórios de dados Olá referenciados por AzureStorageLinkedService e AzureSqlLinkedService, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="b8ea5-200">serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="b8ea5-201">E, Olá o conjunto de dados de blob de entrada (InputDataset) Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="b8ea5-202">Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="b8ea5-203">E, Olá saída SQL o conjunto de dados de tabela (OututDataset) Especifica a tabela de saudação em Olá Olá de toowhich de banco de dados dados saudação do armazenamento de blob são copiados.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="b8ea5-204">Nesta etapa, você criar um conjunto de dados chamado InputDataset que aponta o arquivo de blob tooa (emp.txt) na pasta raiz de saudação de um contêiner de blob (adftutorial) no hello representado por Olá AzureStorageLinkedService vinculado de serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="b8ea5-205">Se você não especificar um valor para o nome de arquivo hello (ou ignorá-lo), dados de todos os blobs na pasta de entrada hello são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="b8ea5-206">Neste tutorial, você deve especificar um valor para o nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="b8ea5-207">Nesta etapa, você cria um conjunto de dados de saída denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="b8ea5-208">Este conjunto de dados aponta tooa SQL tabela no banco de dados do SQL Azure Olá representado por **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="b8ea5-209">Adicione o código a seguir de saudação que **cria e ativa um pipeline** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="b8ea5-210">Nesta etapa, você cria um pipeline com uma **atividade de cópia** que usa **InputDataset** como entrada e **OutputDataset** como saída.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new PipelineCreateOrUpdateParameters()
        {
            Pipeline = new Pipeline()
            {
                Name = PipelineName,
                Properties = new PipelineProperties()
                {
                    Description = "Demo Pipeline for data transfer between blobs",

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
                    Start = PipelineActivePeriodStartTime,
                    End = PipelineActivePeriodEndTime,

                    Activities = new List<Activity>()
                    {
                        new Activity()
                        {
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
                                    Name = Dataset_Source
                                }
                            },
                            Outputs = new List<ActivityOutput>()
                            {
                                new ActivityOutput()
                                {
                                    Name = Dataset_Destination
                                }
                            },
                            TypeProperties = new CopyActivity()
                            {
                                Source = new BlobSource(),
                                Sink = new BlobSink()
                                {
                                    WriteBatchSize = 10000,
                                    WriteBatchTimeout = TimeSpan.FromMinutes(10)
                                }
                            }
                        }
                    }
                }
            }
        });
    ```

    <span data-ttu-id="b8ea5-211">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8ea5-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="b8ea5-212">Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="b8ea5-213">Para obter mais informações sobre a atividade de cópia hello, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="b8ea5-214">Nas soluções de Data Factory, você também pode usar [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="b8ea5-215">Entrada para atividade de saudação é definida muito**InputDataset** e de saída para o conjunto de hello atividade é muito**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="b8ea5-216">Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="b8ea5-217">Para obter uma lista completa de armazenamentos de dados de atividade de cópia hello como origens e coletores com suporte, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b8ea5-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b8ea5-218">toolearn como toouse dados específicos com suporte são armazenados como um fonte/coletor, clique o link de saudação na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="b8ea5-219">Atualmente, o conjunto de dados de saída é quais unidades Olá agenda.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="b8ea5-220">Neste tutorial, o conjunto de dados de saída é configurado tooproduce uma fatia de uma vez por hora.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="b8ea5-221">pipeline de saudação tem uma hora de início e a hora de término que são um dia de distância, que é de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="b8ea5-222">Portanto, 24 fatias de conjunto de dados de saída são produzidas pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="b8ea5-223">Adicionar Olá toohello de código a seguir **principal** conjunto de dados de saída do status de saudação do método tooget de uma fatia de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="b8ea5-224">Há apenas uma fatia esperada neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-224">There is only slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;

    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");        
        // wait before hello next status check
        Thread.Sleep(1000 * 12);

        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });

        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```

13. <span data-ttu-id="b8ea5-225">Adicionar Olá código tooget executar detalhes para um toohello da fatia de dados a seguir **principal** método.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");

    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();

    var datasliceRunListResponse = client.DataSliceRuns.List(
            resourceGroupName,
            dataFactoryName,
            Dataset_Destination,
            new DataSliceRunListParameters()
            {
                DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
            }
        );

    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="b8ea5-226">Adicionar Olá após o método auxiliar usado pelo Olá **principal** método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b8ea5-227">Quando você copia e cola Olá código a seguir, certifique-se de que Olá copiado código estiver em uma saudação de mesmo nível como Olá método Main.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="b8ea5-228">No Olá Gerenciador de soluções, expanda o projeto hello (DataFactoryAPITestApp), clique com botão direito **referências**e clique em **adicionar referência**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="b8ea5-229">Marque a caixa de seleção do assembly **System. Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="b8ea5-230">E clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-230">and click **OK**.</span></span>
16. <span data-ttu-id="b8ea5-231">Crie um aplicativo de console hello.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-231">Build hello console application.</span></span> <span data-ttu-id="b8ea5-232">Clique em **criar** no menu de saudação e clique em **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="b8ea5-233">Confirme se há pelo menos um arquivo hello **adftutorial** contêiner no seu armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="b8ea5-234">Caso contrário, crie **Emp.txt** arquivo no bloco de notas com hello após conteúdo e carregá-lo toohello adftutorial contêiner.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="b8ea5-235">Execute o exemplo hello clicando **depurar** -> **iniciar depuração** no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="b8ea5-236">Quando você vir Olá **obtendo detalhes de uma fatia de dados da execução**, aguarde alguns minutos e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="b8ea5-237">Use Olá tooverify portal do Azure essa fábrica de dados Olá **APITutorialFactory** é criada com hello artefatos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8ea5-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="b8ea5-238">Serviço vinculado: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="b8ea5-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="b8ea5-239">Conjunto de dados: **InputDataset** e **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="b8ea5-240">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="b8ea5-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="b8ea5-241">Verifique se que os registros dos funcionários Olá dois são criados no hello **emp** tabela Olá especificado banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8ea5-242">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8ea5-242">Next steps</span></span>
<span data-ttu-id="b8ea5-243">Confira [Referência da API do .NET do Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) para obter uma documentação abrangente sobre a API do .NET do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="b8ea5-244">Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="b8ea5-245">Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação:</span><span class="sxs-lookup"><span data-stu-id="b8ea5-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="b8ea5-246">toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8ea5-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

