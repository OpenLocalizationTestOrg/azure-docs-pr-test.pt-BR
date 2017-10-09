---
title: aaaCreate pipelines de dados usando o SDK .NET do Azure | Microsoft Docs
description: "Saiba como tooprogrammatically criar, monitorar e gerenciar as fábricas de dados do Azure usando o SDK de fábrica de dados."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="a0e75-103">Criar, monitorar e gerenciar data factories do Azure usando o SDK do .NET do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a0e75-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="a0e75-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a0e75-104">Overview</span></span>
<span data-ttu-id="a0e75-105">Você pode criar, monitorar e gerenciar as Data Factory do Azure programaticamente usando o SDK do .NET da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a0e75-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="a0e75-106">Este artigo contém uma explicação passo a passo que você pode seguir toocreate um aplicativo de console .NET de exemplo que cria e monitora uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="a0e75-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="a0e75-107">Este artigo não aborda Olá todos os dados de fábrica .NET API.</span><span class="sxs-lookup"><span data-stu-id="a0e75-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="a0e75-108">Consulte [Referência da API do .NET do Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) para obter uma documentação abrangente sobre a API do .NET do de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a0e75-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a0e75-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a0e75-109">Prerequisites</span></span>
* <span data-ttu-id="a0e75-110">Visual Studio 2012 ou 2013 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="a0e75-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="a0e75-111">Baixe e instale o [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a0e75-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="a0e75-112">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-112">Azure PowerShell.</span></span> <span data-ttu-id="a0e75-113">Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall PowerShell do Azure no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a0e75-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="a0e75-114">Use o Azure PowerShell toocreate um aplicativo do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="a0e75-115">Criar um aplicativo no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0e75-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="a0e75-116">Criar um aplicativo do Active Directory do Azure, criar uma entidade de serviço para o aplicativo hello e atribuí-la toohello **colaborador da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="a0e75-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="a0e75-117">Inicie o **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="a0e75-118">Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="a0e75-119">Execute Olá tooview de comando a seguir todas as assinaturas de saudação para esta conta.</span><span class="sxs-lookup"><span data-stu-id="a0e75-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="a0e75-120">Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir.</span><span class="sxs-lookup"><span data-stu-id="a0e75-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="a0e75-121">Substituir  **&lt;NameOfAzureSubscription** &gt; com o nome da saudação de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a0e75-122">Anote **SubscriptionId** e **TenantId** da saída de hello desse comando.</span><span class="sxs-lookup"><span data-stu-id="a0e75-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="a0e75-123">Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando de saudação do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="a0e75-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="a0e75-124">Se o grupo de recursos Olá já existe, especifique se tooupdate-lo (Y) ou mantê-lo como (N).</span><span class="sxs-lookup"><span data-stu-id="a0e75-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="a0e75-125">Se você usar um grupo de recursos diferentes, você precisa toouse nome de saudação do seu grupo de recursos no lugar de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a0e75-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="a0e75-126">Criar um aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a0e75-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="a0e75-127">Se você obtiver Olá erro a seguir, especifique uma URL diferente e execute o comando Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="a0e75-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="a0e75-128">Crie hello entidade de serviço do AD.</span><span class="sxs-lookup"><span data-stu-id="a0e75-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="a0e75-129">Adicionar toohello principal do serviço **colaborador da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="a0e75-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="a0e75-130">Obter a ID do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a0e75-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="a0e75-131">Anote a ID do aplicativo hello (applicationID) de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="a0e75-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="a0e75-132">Você deve ter quatro valores após estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a0e75-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="a0e75-133">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="a0e75-133">Tenant ID</span></span>
* <span data-ttu-id="a0e75-134">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="a0e75-134">Subscription ID</span></span>
* <span data-ttu-id="a0e75-135">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="a0e75-135">Application ID</span></span>
* <span data-ttu-id="a0e75-136">Senha (especificada no comando primeiro Olá)</span><span class="sxs-lookup"><span data-stu-id="a0e75-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="a0e75-137">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="a0e75-137">Walkthrough</span></span>
<span data-ttu-id="a0e75-138">Olá instruções passo a passo, você criará uma fábrica de dados com um pipeline que contém uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="a0e75-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="a0e75-139">Olá, atividade de cópia copia dados de uma pasta na sua pasta de tooanother do armazenamento de BLOBs do Azure no hello mesmo armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="a0e75-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="a0e75-140">Hello atividade de cópia realiza a movimentação de dados Olá na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="a0e75-141">atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="a0e75-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="a0e75-142">Consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre hello atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="a0e75-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="a0e75-143">Usando o Visual Studio 2012/2013/2015, crie um aplicativo de console C# .NET.</span><span class="sxs-lookup"><span data-stu-id="a0e75-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="a0e75-144">Inicie o **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="a0e75-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="a0e75-145">Clique em **arquivo**, ponto muito**novo**e clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="a0e75-146">Expanda **Modelos** e selecione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="a0e75-147">Neste passo a passo, você usa C#, mas você pode usar qualquer linguagem .NET.</span><span class="sxs-lookup"><span data-stu-id="a0e75-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="a0e75-148">Selecione **aplicativo de Console** da lista de saudação de tipos de projeto em saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="a0e75-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="a0e75-149">Digite **DataFactoryAPITestApp** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="a0e75-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="a0e75-150">Selecione **C:\ADFGetStarted** para Olá local.</span><span class="sxs-lookup"><span data-stu-id="a0e75-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="a0e75-151">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0e75-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="a0e75-152">Clique em **ferramentas**, ponto muito**NuGet Package Manager**e clique em **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="a0e75-153">Em Olá **Package Manager Console**, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a0e75-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="a0e75-154">Execute Olá pacote do comando tooinstall fábrica de dados a seguir:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="a0e75-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="a0e75-155">Execute Olá pacote de Active Directory do Azure tooinstall de comando (use a API do Active Directory em código Olá) a seguir:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="a0e75-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="a0e75-156">Substitua o conteúdo de saudação do **App. config** arquivo no projeto de saudação com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0e75-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
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
5. <span data-ttu-id="a0e75-157">No arquivo App. config de hello, atualizar os valores de  **&lt;ID do aplicativo&gt;**,  **&lt;senha&gt;**,  **&lt; ID da assinatura&gt;**, e  **&lt;ID do locatário&gt;**  com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="a0e75-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="a0e75-158">Adicione o seguinte Olá **usando** instruções toohello **Program.cs** arquivo no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0e75-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

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
6. <span data-ttu-id="a0e75-159">Adicionar Olá seguindo o código que cria uma instância de **DataPipelineManagementClient** classe toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="a0e75-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="a0e75-160">Você usar esse objeto toocreate uma fábrica de dados, um serviço vinculado, conjuntos de dados de entrada e saídos e um pipeline.</span><span class="sxs-lookup"><span data-stu-id="a0e75-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="a0e75-161">Você também pode usar este fatias de toomonitor de objeto de um conjunto de dados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="a0e75-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a0e75-162">Substituir valor de saudação do **resourceGroupName** com nome de saudação do seu grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="a0e75-163">Você pode criar um grupo de recursos usando Olá [AzureResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0e75-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="a0e75-164">Atualize o nome da saudação dados fábrica (dataFactoryName) toobe exclusivo.</span><span class="sxs-lookup"><span data-stu-id="a0e75-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="a0e75-165">Nome da fábrica de dados Olá deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="a0e75-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="a0e75-166">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a0e75-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="a0e75-167">Adicionar Olá seguindo o código que cria um **fábrica de dados** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="a0e75-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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
8. <span data-ttu-id="a0e75-168">Adicionar Olá seguindo o código que cria um **serviço vinculado do armazenamento do Azure** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="a0e75-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a0e75-169">Substitua **storageaccountname** e **accountkey** pelo nome e pela chave da sua conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="a0e75-170">Adicionar Olá código que cria a seguir **conjuntos de dados de entrada e saídos** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="a0e75-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="a0e75-171">Olá **FolderPath** para o blob de entrada hello está definido muito**adftutorial /** onde **adftutorial** é Olá nome do contêiner de saudação em seu armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="a0e75-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="a0e75-172">Se este contêiner não existe em seu armazenamento de BLOBs do Azure, crie um contêiner com este nome: **adftutorial** e carregar um contêiner de toohello do arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="a0e75-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="a0e75-173">Olá FolderPath para saudação de saída blob é definido como: **adftutorial/apifactoryoutput / {Slice}** onde **fatia** é calculado dinamicamente Olá com base no valor de **SliceStart**(Iniciar data e hora de cada fatia).</span><span class="sxs-lookup"><span data-stu-id="a0e75-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
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
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
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
10. <span data-ttu-id="a0e75-174">Adicione o código a seguir de saudação que **cria e ativa um pipeline** toohello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="a0e75-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="a0e75-175">Essa pipeline tem uma **CopyActivity** que usa **BlobSource** como fonte e **BlobSink** como coletor.</span><span class="sxs-lookup"><span data-stu-id="a0e75-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="a0e75-176">Hello atividade de cópia realiza a movimentação de dados Olá na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="a0e75-177">atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="a0e75-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="a0e75-178">Consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo para obter detalhes sobre hello atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="a0e75-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
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
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
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
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="a0e75-179">Adicionar Olá toohello de código a seguir **principal** conjunto de dados de saída do status de saudação do método tooget de uma fatia de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0e75-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="a0e75-180">Apenas uma fatia é esperada neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="a0e75-180">There is only one slice expected in this sample.</span></span>

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
13. <span data-ttu-id="a0e75-181">**(opcional)**  Tooget executar detalhes para um toohello da fatia de dados de código a seguir de saudação adicionar **principal** método.</span><span class="sxs-lookup"><span data-stu-id="a0e75-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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
        });
    
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
14. <span data-ttu-id="a0e75-182">Adicionar Olá após o método auxiliar usado pelo Olá **principal** método toohello **programa** classe.</span><span class="sxs-lookup"><span data-stu-id="a0e75-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="a0e75-183">Esse método será exibida uma caixa de diálogo que permite que você forneça **nome de usuário** e **senha** que você use toolog no portal de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

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

15. <span data-ttu-id="a0e75-184">No hello Gerenciador de soluções, expanda o projeto Olá: **DataFactoryAPITestApp**, clique com botão direito **referências**e clique em **adicionar referência**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="a0e75-185">Selecione caixa de seleção para o assembly `System.Configuration` e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="a0e75-186">Crie um aplicativo de console hello.</span><span class="sxs-lookup"><span data-stu-id="a0e75-186">Build hello console application.</span></span> <span data-ttu-id="a0e75-187">Clique em **criar** no menu de saudação e clique em **compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="a0e75-188">Confirme se há pelo menos um arquivo no contêiner de adftutorial Olá em seu armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0e75-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="a0e75-189">Caso contrário, crie Emp.txt arquivo no bloco de notas com hello seguindo conteúdo e carregá-lo toohello adftutorial contêiner.</span><span class="sxs-lookup"><span data-stu-id="a0e75-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="a0e75-190">Execute o exemplo hello clicando **depurar** -> **iniciar depuração** no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0e75-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="a0e75-191">Quando você vir Olá **obtendo detalhes de uma fatia de dados da execução**, aguarde alguns minutos e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="a0e75-192">Use Olá tooverify portal do Azure essa fábrica de dados Olá **APITutorialFactory** é criada com hello artefatos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0e75-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="a0e75-193">Serviço vinculado: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="a0e75-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="a0e75-194">Conjunto de dados: **DatasetBlobSource** e **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="a0e75-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="a0e75-195">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="a0e75-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="a0e75-196">Verificar se um arquivo de saída é criado no hello **apifactoryoutput** pasta Olá **adftutorial** contêiner.</span><span class="sxs-lookup"><span data-stu-id="a0e75-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="a0e75-197">Obter uma lista de fatias de dados com falha</span><span class="sxs-lookup"><span data-stu-id="a0e75-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="a0e75-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0e75-198">Next steps</span></span>
<span data-ttu-id="a0e75-199">Consulte Olá seguinte exemplo para a criação de um pipeline usando o SDK .NET que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure:</span><span class="sxs-lookup"><span data-stu-id="a0e75-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="a0e75-200">Criar um pipeline de dados de toocopy do armazenamento de Blob tooSQL banco de dados</span><span class="sxs-lookup"><span data-stu-id="a0e75-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
