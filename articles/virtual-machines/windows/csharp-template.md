---
title: aaaDeploy uma VM usando o c# e um modelo do Gerenciador de recursos | Microsoft Docs
description: Saiba toohow toouse c# e um modelo de Gerenciador de recursos toodeploy uma VM do Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="483cf-103">Implantar uma Máquina Virtual do Azure usando C# e um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="483cf-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="483cf-104">Este artigo mostra como toodeploy um modelo do Gerenciador de recursos do Azure usando o c#.</span><span class="sxs-lookup"><span data-stu-id="483cf-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="483cf-105">modelo Olá criados por você implanta uma única máquina virtual executando o Windows Server em uma nova rede virtual com uma única sub-rede.</span><span class="sxs-lookup"><span data-stu-id="483cf-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="483cf-106">Para obter uma descrição detalhada do recurso de máquina virtual hello, consulte [máquinas virtuais em um modelo do Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="483cf-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="483cf-107">Para obter mais informações sobre todos os recursos de saudação em um modelo, consulte [passo a passo do Gerenciador de recursos do Azure modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="483cf-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="483cf-108">Leva aproximadamente 10 minutos toodo essas etapas.</span><span class="sxs-lookup"><span data-stu-id="483cf-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="483cf-109">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="483cf-109">Create a Visual Studio project</span></span>

<span data-ttu-id="483cf-110">Nesta etapa, certifique-se de que o Visual Studio está instalado e você criar um modelo de saudação toodeploy console aplicativo usado.</span><span class="sxs-lookup"><span data-stu-id="483cf-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="483cf-111">Se você ainda não fez isso, instale o [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="483cf-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="483cf-112">Selecione **desenvolvimento de área de trabalho do .NET** Olá página cargas de trabalho e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="483cf-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="483cf-113">Olá resumo, você verá que **ferramentas de desenvolvimento do .NET Framework 4 4.6** é selecionado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="483cf-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="483cf-114">Se você já tiver instalado o Visual Studio, você pode adicionar carga de trabalho do .NET hello usando Olá iniciador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="483cf-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="483cf-115">No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="483cf-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="483cf-116">Em **modelos** > **Visual C#**, selecione **aplicativo de Console (.NET Framework)**, digite *myDotnetProject* para nome de saudação do Olá projeto local selecione Olá Olá do projeto do e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="483cf-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="483cf-117">Instalar pacotes de saudação</span><span class="sxs-lookup"><span data-stu-id="483cf-117">Install hello packages</span></span>

<span data-ttu-id="483cf-118">Pacotes do NuGet são Olá mais fácil maneira tooinstall Olá bibliotecas que você precisa toofinish essas etapas.</span><span class="sxs-lookup"><span data-stu-id="483cf-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="483cf-119">bibliotecas de saudação tooget que você precisa no Visual Studio, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="483cf-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="483cf-120">Clique em **Ferramentas** > **Gerenciador de Pacotes Nuget** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="483cf-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="483cf-121">Digite os seguintes comandos no console de saudação:</span><span class="sxs-lookup"><span data-stu-id="483cf-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="483cf-122">Criar arquivos de saudação</span><span class="sxs-lookup"><span data-stu-id="483cf-122">Create hello files</span></span>

<span data-ttu-id="483cf-123">Nesta etapa, você pode criar um arquivo de modelo que implanta recursos hello e um arquivo de parâmetros que fornece o modelo de toohello de valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="483cf-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="483cf-124">Você também pode criar um arquivo de autorização é usada tooperform do Azure Resource Manager operations.</span><span class="sxs-lookup"><span data-stu-id="483cf-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="483cf-125">Criar arquivo de modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="483cf-125">Create hello template file</span></span>

1. <span data-ttu-id="483cf-126">No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="483cf-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="483cf-127">Arquivo de saudação do nome *CreateVMTemplate.json*e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="483cf-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="483cf-128">Adicione o arquivo de toohello código JSON que você criou:</span><span class="sxs-lookup"><span data-stu-id="483cf-128">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. <span data-ttu-id="483cf-129">Salve o arquivo de CreateVMTemplate.json hello.</span><span class="sxs-lookup"><span data-stu-id="483cf-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="483cf-130">Criar arquivo de parâmetros de saudação</span><span class="sxs-lookup"><span data-stu-id="483cf-130">Create hello parameters file</span></span>

<span data-ttu-id="483cf-131">toospecify valores para parâmetros de recursos de saudação que são definidos no modelo de saudação, você criar um arquivo de parâmetros que contém os valores hello.</span><span class="sxs-lookup"><span data-stu-id="483cf-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="483cf-132">No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="483cf-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="483cf-133">Arquivo de saudação do nome *Parameters.json*e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="483cf-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="483cf-134">Adicione o arquivo de toohello código JSON que você criou:</span><span class="sxs-lookup"><span data-stu-id="483cf-134">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. <span data-ttu-id="483cf-135">Salve o arquivo de Parameters.json hello.</span><span class="sxs-lookup"><span data-stu-id="483cf-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="483cf-136">Criar arquivo de autorização Olá</span><span class="sxs-lookup"><span data-stu-id="483cf-136">Create hello authorization file</span></span>

<span data-ttu-id="483cf-137">Antes de implantar um modelo, certifique-se de que você tenha acesso tooan [entidade de serviço do Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="483cf-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="483cf-138">Da entidade de serviço hello, você deve adquirir um token para autenticar solicitações tooAzure Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="483cf-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="483cf-139">Você também deve registrar a ID do aplicativo hello, chave de autenticação hello e ID de locatário Olá que você precisa no arquivo de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="483cf-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="483cf-140">No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="483cf-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="483cf-141">Arquivo de saudação do nome *azureauth.properties*e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="483cf-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="483cf-142">Adicione estas propriedades de autorização:</span><span class="sxs-lookup"><span data-stu-id="483cf-142">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="483cf-143">Substituir  **&lt;id da assinatura&gt;**  com o identificador de assinatura,  **&lt;id do aplicativo&gt;**  com hello aplicativo do Active Directory identificador,  **&lt;chave de autenticação&gt;**  com chave de aplicativo hello, e  **&lt;id de locatário&gt;**  com locatário Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="483cf-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="483cf-144">Salve o arquivo de azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="483cf-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="483cf-145">Definir uma variável de ambiente no Windows chamado AZURE_AUTH_LOCATION com arquivo hello de tooauthorization de caminho completo que você criou, por exemplo hello PowerShell pode ser usado o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="483cf-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="483cf-146">Crie saudação do cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="483cf-146">Create hello management client</span></span>

1. <span data-ttu-id="483cf-147">Abra o arquivo Program.cs Olá projeto Olá que você criou e, em seguida, adicioná-las usando toohello existente instruções na parte superior do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="483cf-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="483cf-148">cliente de gerenciamento de saudação toocreate, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="483cf-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="483cf-149">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="483cf-149">Create a resource group</span></span>

<span data-ttu-id="483cf-150">toospecify valores para o aplicativo hello, adicione o método do código toohello Main:</span><span class="sxs-lookup"><span data-stu-id="483cf-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="483cf-151">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="483cf-151">Create a storage account</span></span>

<span data-ttu-id="483cf-152">parâmetros e modelo Olá implantados por meio de uma conta de armazenamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="483cf-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="483cf-153">Nesta etapa, você cria conta hello e carregar arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="483cf-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="483cf-154">toocreate Olá conta, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="483cf-154">toocreate hello account, add this code toohello Main method:</span></span>

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a><span data-ttu-id="483cf-155">Implante o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="483cf-155">Deploy hello template</span></span>

<span data-ttu-id="483cf-156">Implante o modelo hello e parâmetros de conta de armazenamento Olá que foi criado.</span><span class="sxs-lookup"><span data-stu-id="483cf-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="483cf-157">modelo de saudação toodeploy, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="483cf-157">toodeploy hello template, add this code toohello Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a><span data-ttu-id="483cf-158">Excluir recursos Olá</span><span class="sxs-lookup"><span data-stu-id="483cf-158">Delete hello resources</span></span>

<span data-ttu-id="483cf-159">Como você é cobrado pelos recursos usados no Azure, é sempre recursos toodelete de práticas recomendadas que não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="483cf-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="483cf-160">Você não precisa toodelete cada recurso separadamente de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="483cf-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="483cf-161">Exclua grupo de recursos de saudação e todos os seus recursos são excluídos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="483cf-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="483cf-162">recurso de saudação toodelete grupo, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="483cf-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="483cf-163">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="483cf-163">Run hello application</span></span>

<span data-ttu-id="483cf-164">Ele deve levar cerca de cinco minutos para este toorun do aplicativo de console completamente do início toofinish.</span><span class="sxs-lookup"><span data-stu-id="483cf-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="483cf-165">aplicativo de console hello toorun, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="483cf-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="483cf-166">Antes de pressionar **Enter** toostart recursos de exclusão, você pode levar alguns minutos criação de saudação do tooverify de recursos de saudação em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="483cf-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="483cf-167">Clique em Olá implantação status toosee informações sobre a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="483cf-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="483cf-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="483cf-168">Next steps</span></span>
* <span data-ttu-id="483cf-169">Se houver problemas com a implantação de hello, a próxima etapa seria toolook em [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="483cf-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="483cf-170">Saiba como toodeploy uma máquina virtual e seus recursos de suporte, revisando [implantar um Azure Máquina Virtual usando o c#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="483cf-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
