---
title: Criar pipelines de dados usando o SDK .NET | Microsoft Docs
description: Aprenda como criar, monitorar e gerenciar as data factories do Azure programaticamente usando o SDK da Data Factory.
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
ms.openlocfilehash: 9d9dac75321c5d4e079f49320d9b7c6f56e48754
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="c6f9a-103">Criar, monitorar e gerenciar data factories do Azure usando o SDK do .NET do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c6f9a-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="c6f9a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c6f9a-104">Overview</span></span>
<span data-ttu-id="c6f9a-105">Você pode criar, monitorar e gerenciar as Data Factory do Azure programaticamente usando o SDK do .NET da Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="c6f9a-106">Este artigo contém uma explicação passo a passo que você pode seguir para criar um aplicativo de console .NET de exemplo que cria e monitora uma Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="c6f9a-107">Este artigo não abrange toda a API .NET de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-107">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="c6f9a-108">Consulte [Referência da API do .NET do Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) para obter uma documentação abrangente sobre a API do .NET do de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c6f9a-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c6f9a-109">Prerequisites</span></span>
* <span data-ttu-id="c6f9a-110">Visual Studio 2012 ou 2013 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="c6f9a-111">Baixe e instale o [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c6f9a-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="c6f9a-112">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-112">Azure PowerShell.</span></span> <span data-ttu-id="c6f9a-113">Siga as instruções no artigo [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para instalar a última versão do Azure PowerShell no computador.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-113">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="c6f9a-114">Você pode usar o Azure PowerShell para criar um aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-114">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="c6f9a-115">Criar um aplicativo no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6f9a-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="c6f9a-116">Crie um aplicativo do Azure Active Directory, crie uma entidade de serviço para o aplicativo e atribua-a à função **Colaborador de Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="c6f9a-116">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="c6f9a-117">Inicie o **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="c6f9a-118">Execute o comando a seguir e insira o nome de usuário e a senha que você usa para entrar no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-118">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="c6f9a-119">Execute o comando a seguir para exibir todas as assinaturas dessa conta.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-119">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="c6f9a-120">Execute o comando a seguir para selecionar a assinatura com a qual deseja trabalhar.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-120">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="c6f9a-121">Substitua **&lt;NameOfAzureSubscription**&gt; pelo nome da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-121">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="c6f9a-122">Anote **SubscriptionId** e **TenantId** da saída desse comando.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-122">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="c6f9a-123">Crie um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando o comando a seguir no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="c6f9a-124">Se o grupo de recursos já existe, especifique se deseja atualizá-lo (S) ou mantê-lo como (N).</span><span class="sxs-lookup"><span data-stu-id="c6f9a-124">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="c6f9a-125">Se você utilizar um grupo de recursos diferente, precisará usar o nome do seu grupo de recursos no lugar de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-125">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="c6f9a-126">Criar um aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="c6f9a-127">Se você receber o erro a seguir, especifique uma URL diferente e execute o comando novamente.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-127">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="c6f9a-128">Crie a entidade de serviço do AD.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-128">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="c6f9a-129">Adicione a entidade de serviço à função de **Colaborador do Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="c6f9a-129">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="c6f9a-130">Obtenha a ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-130">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="c6f9a-131">Anote a ID do aplicativo (IDaplicativo) na saída.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-131">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="c6f9a-132">Você deve ter quatro valores após estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c6f9a-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="c6f9a-133">ID do locatário</span><span class="sxs-lookup"><span data-stu-id="c6f9a-133">Tenant ID</span></span>
* <span data-ttu-id="c6f9a-134">ID da assinatura</span><span class="sxs-lookup"><span data-stu-id="c6f9a-134">Subscription ID</span></span>
* <span data-ttu-id="c6f9a-135">ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="c6f9a-135">Application ID</span></span>
* <span data-ttu-id="c6f9a-136">Senha (especificada no primeiro comando)</span><span class="sxs-lookup"><span data-stu-id="c6f9a-136">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="c6f9a-137">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="c6f9a-137">Walkthrough</span></span>
<span data-ttu-id="c6f9a-138">No passo a passo, você cria um data factory com um pipeline que contém uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-138">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="c6f9a-139">A atividade de cópia copia dados de uma pasta no seu armazenamento de blobs do Azure para outra pasta no mesmo armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-139">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="c6f9a-140">A atividade de cópia realiza a movimentação de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-140">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="c6f9a-141">A atividade é habilitada por um serviço globalmente disponível que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-141">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="c6f9a-142">Veja o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) para obter detalhes sobre a Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="c6f9a-143">Usando o Visual Studio 2012/2013/2015, crie um aplicativo de console C# .NET.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="c6f9a-144">Inicie o **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="c6f9a-145">Clique em **Arquivo**, aponte para **Novo** e clique em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-145">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="c6f9a-146">Expanda **Modelos** e selecione **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="c6f9a-147">Neste passo a passo, você usa C#, mas você pode usar qualquer linguagem .NET.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="c6f9a-148">Selecione **Aplicativo de console** na lista de tipos de projetos à direita.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-148">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="c6f9a-149">Digite **DataFactoryAPITestApp** como o Nome.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-149">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="c6f9a-150">Selecione **C:\ADFGetStarted** como o Local.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-150">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="c6f9a-151">Clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-151">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="c6f9a-152">Clique em **Ferramentas**, aponte para **Gerenciador de Pacotes NuGet** e clique em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-152">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="c6f9a-153">No **Console do Gerenciador de Pacotes**, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c6f9a-153">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="c6f9a-154">Execute o seguinte comando para instalar o pacote de Data Factory: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="c6f9a-154">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="c6f9a-155">Execute o seguinte comando para instalar o pacote do Azure Active Directory (use a API do Active Directory no código): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="c6f9a-155">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="c6f9a-156">Substitua o conteúdo do arquivo **App.config** no projeto pelo seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="c6f9a-156">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="c6f9a-157">No arquivo App.Config, atualize os valores para **&lt;ID do aplicativo&gt;**, **&lt;Senha&gt;**, **&lt;ID da assinatura&gt;** e **&lt;ID do locatário&gt;** com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-157">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="c6f9a-158">Adicione as seguintes instruções **using** ao arquivo **Program.cs** no projeto.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-158">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

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
6. <span data-ttu-id="c6f9a-159">Adicione o seguinte código que cria uma instância de classe **DataPipelineManagementClient** ao método **Main**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-159">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="c6f9a-160">Você usa esse objeto para criar um data factory, um serviço vinculado, conjunto de dados de entrada e de saída e um pipeline.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-160">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="c6f9a-161">Você também usa esse objeto para monitorar as partes de um conjunto de dados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-161">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="c6f9a-162">Substitua o valor de **resourceGroupName** pelo nome do seu grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-162">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="c6f9a-163">Você pode criar um grupo de recursos usando o cmdlet [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) .</span><span class="sxs-lookup"><span data-stu-id="c6f9a-163">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="c6f9a-164">O nome de atualização do data factory (NomedataFactory) deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-164">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="c6f9a-165">O nome de data factory deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-165">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="c6f9a-166">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="c6f9a-167">Adicione o seguinte código que cria um **data factory** no método **Main**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-167">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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
8. <span data-ttu-id="c6f9a-168">Adicione o seguinte código, que cria um **serviço vinculado do Armazenamento do Azure** para o método **Main**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-168">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c6f9a-169">Substitua **storageaccountname** e **accountkey** pelo nome e pela chave da sua conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="c6f9a-170">Adicione o seguinte código que cria **conjuntos de dados de entrada e de saída** para o método **Main**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-170">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="c6f9a-171">O **FolderPath** para o blob de entrada é definido como **adftutorial/** em que **adftutoria**l é o nome do contêiner no seu armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-171">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="c6f9a-172">Se esse contêiner não existir em seu armazenamento de blob do Azure, crie um contêiner com o nome **adftutorial** e carregue um arquivo de texto no contêiner.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="c6f9a-173">O FolderPath para o blob de saída é definido como: **adftutorial/apifactoryoutput /{Slice}**, em que a **Slice** é dinamicamente calculada com base no valor de **SliceStart** (data e hora de início de cada fatia).</span><span class="sxs-lookup"><span data-stu-id="c6f9a-173">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="c6f9a-174">Adicione o código a seguir, que **cria e ativa um pipeline** no método **Main**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-174">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="c6f9a-175">Essa pipeline tem uma **CopyActivity** que usa **BlobSource** como fonte e **BlobSink** como coletor.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="c6f9a-176">A atividade de cópia realiza a movimentação de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-176">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="c6f9a-177">A atividade é habilitada por um serviço globalmente disponível que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-177">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="c6f9a-178">Veja o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) para obter detalhes sobre a Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

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
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
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
12. <span data-ttu-id="c6f9a-179">Adicione o seguinte código ao método **Principal** para obter o status de uma fatia de dados do conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-179">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="c6f9a-180">Apenas uma fatia é esperada neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
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
13. <span data-ttu-id="c6f9a-181">**(opcional)** Adicione o seguinte código para obter detalhes de execução de uma fatia de dados ao método **Principal**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-181">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
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
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="c6f9a-182">Adicione o método auxiliar a seguir usado pelo método **Main** na classe **Program**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-182">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="c6f9a-183">Esse método exibe uma caixa de diálogo que permite fornecer o **nome de usuário** e a **senha** que você usa para fazer logon no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

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

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="c6f9a-184">No Gerenciador de Soluções, expanda o projeto: **DataFactoryAPITestApp**, clique com botão direito do mouse em **Referências** e clique em **Adicionar Referência**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-184">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="c6f9a-185">Selecione caixa de seleção para o assembly `System.Configuration` e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="c6f9a-186">Compile o aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-186">Build the console application.</span></span> <span data-ttu-id="c6f9a-187">Clique no menu **Compilar** e clique em **Solução de Compilação**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-187">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="c6f9a-188">Confirme se há pelo menos um arquivo no contêiner adftutorial no seu armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-188">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="c6f9a-189">Caso contrário, crie o arquivo de Emp.txt no bloco de notas com o seguinte conteúdo e carregue-o no contêiner adftutorial.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-189">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="c6f9a-190">Execute o exemplo, clicando em **Depurar** -> **Iniciar Depuração** no menu.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-190">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="c6f9a-191">Quando você vir **Obter detalhes de execução de uma fatia de dados**, aguarde alguns minutos e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-191">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="c6f9a-192">Use o Portal do Azure para verificar se a data factory **APITutorialFactory** foi criada com os seguintes artefatos:</span><span class="sxs-lookup"><span data-stu-id="c6f9a-192">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="c6f9a-193">Serviço vinculado: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="c6f9a-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="c6f9a-194">Conjunto de dados: **DatasetBlobSource** e **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="c6f9a-195">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="c6f9a-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="c6f9a-196">Verifique se um arquivo de saída foi criado na pasta **apifactoryoutput** no contêiner **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="c6f9a-196">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="c6f9a-197">Obter uma lista de fatias de dados com falha</span><span class="sxs-lookup"><span data-stu-id="c6f9a-197">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
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

## <a name="next-steps"></a><span data-ttu-id="c6f9a-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6f9a-198">Next steps</span></span>
<span data-ttu-id="c6f9a-199">Consulte o exemplo a seguir para criar um pipeline usando o SDK do .NET que copia dados de um Armazenamento de Blobs do Azure para um banco de dados SQL do Azure:</span><span class="sxs-lookup"><span data-stu-id="c6f9a-199">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="c6f9a-200">Criar um pipeline para copiar dados do Armazenamento de Blobs para o Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="c6f9a-200">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
