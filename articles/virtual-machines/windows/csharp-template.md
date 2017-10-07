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
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>Implantar uma Máquina Virtual do Azure usando C# e um modelo do Resource Manager
Este artigo mostra como toodeploy um modelo do Gerenciador de recursos do Azure usando o c#. modelo Olá criados por você implanta uma única máquina virtual executando o Windows Server em uma nova rede virtual com uma única sub-rede.

Para obter uma descrição detalhada do recurso de máquina virtual hello, consulte [máquinas virtuais em um modelo do Azure Resource Manager](template-description.md). Para obter mais informações sobre todos os recursos de saudação em um modelo, consulte [passo a passo do Gerenciador de recursos do Azure modelo](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Leva aproximadamente 10 minutos toodo essas etapas.

## <a name="create-a-visual-studio-project"></a>Criar um projeto do Visual Studio

Nesta etapa, certifique-se de que o Visual Studio está instalado e você criar um modelo de saudação toodeploy console aplicativo usado.

1. Se você ainda não fez isso, instale o [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selecione **desenvolvimento de área de trabalho do .NET** Olá página cargas de trabalho e, em seguida, clique em **instalar**. Olá resumo, você verá que **ferramentas de desenvolvimento do .NET Framework 4 4.6** é selecionado automaticamente para você. Se você já tiver instalado o Visual Studio, você pode adicionar carga de trabalho do .NET hello usando Olá iniciador do Visual Studio.
2. No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.
3. Em **modelos** > **Visual C#**, selecione **aplicativo de Console (.NET Framework)**, digite *myDotnetProject* para nome de saudação do Olá projeto local selecione Olá Olá do projeto do e, em seguida, clique em **Okey**.

## <a name="install-hello-packages"></a>Instalar pacotes de saudação

Pacotes do NuGet são Olá mais fácil maneira tooinstall Olá bibliotecas que você precisa toofinish essas etapas. bibliotecas de saudação tooget que você precisa no Visual Studio, siga estas etapas:

1. Clique em **Ferramentas** > **Gerenciador de Pacotes Nuget** e em **Console do Gerenciador de Pacotes**.
2. Digite os seguintes comandos no console de saudação:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Criar arquivos de saudação

Nesta etapa, você pode criar um arquivo de modelo que implanta recursos hello e um arquivo de parâmetros que fornece o modelo de toohello de valores de parâmetro. Você também pode criar um arquivo de autorização é usada tooperform do Azure Resource Manager operations.

### <a name="create-hello-template-file"></a>Criar arquivo de modelo de saudação

1. No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*. Arquivo de saudação do nome *CreateVMTemplate.json*e, em seguida, clique em **adicionar**.
2. Adicione o arquivo de toohello código JSON que você criou:

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

3. Salve o arquivo de CreateVMTemplate.json hello.

### <a name="create-hello-parameters-file"></a>Criar arquivo de parâmetros de saudação

toospecify valores para parâmetros de recursos de saudação que são definidos no modelo de saudação, você criar um arquivo de parâmetros que contém os valores hello.

1. No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*. Arquivo de saudação do nome *Parameters.json*e, em seguida, clique em **adicionar**.
2. Adicione o arquivo de toohello código JSON que você criou:

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

4. Salve o arquivo de Parameters.json hello.

### <a name="create-hello-authorization-file"></a>Criar arquivo de autorização Olá

Antes de implantar um modelo, certifique-se de que você tenha acesso tooan [entidade de serviço do Active Directory](../../resource-group-authenticate-service-principal.md). Da entidade de serviço hello, você deve adquirir um token para autenticar solicitações tooAzure Gerenciador de recursos. Você também deve registrar a ID do aplicativo hello, chave de autenticação hello e ID de locatário Olá que você precisa no arquivo de autorização de saudação.

1. No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*. Arquivo de saudação do nome *azureauth.properties*e, em seguida, clique em **adicionar**.
2. Adicione estas propriedades de autorização:

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

    Substituir  **&lt;id da assinatura&gt;**  com o identificador de assinatura,  **&lt;id do aplicativo&gt;**  com hello aplicativo do Active Directory identificador,  **&lt;chave de autenticação&gt;**  com chave de aplicativo hello, e  **&lt;id de locatário&gt;**  com locatário Olá identificador.

3. Salve o arquivo de azureauth.properties hello.
4. Definir uma variável de ambiente no Windows chamado AZURE_AUTH_LOCATION com arquivo hello de tooauthorization de caminho completo que você criou, por exemplo hello PowerShell pode ser usado o comando a seguir:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Crie saudação do cliente de gerenciamento

1. Abra o arquivo Program.cs Olá projeto Olá que você criou e, em seguida, adicioná-las usando toohello existente instruções na parte superior do arquivo hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. cliente de gerenciamento de saudação toocreate, adicione este código toohello método Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

toospecify valores para o aplicativo hello, adicione o método do código toohello Main:

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

parâmetros e modelo Olá implantados por meio de uma conta de armazenamento no Azure. Nesta etapa, você cria conta hello e carregar arquivos de saudação. 

toocreate Olá conta, adicione este código toohello método Main:

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

## <a name="deploy-hello-template"></a>Implante o modelo de saudação

Implante o modelo hello e parâmetros de conta de armazenamento Olá que foi criado. 

modelo de saudação toodeploy, adicione este código toohello método Main:

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

## <a name="delete-hello-resources"></a>Excluir recursos Olá

Como você é cobrado pelos recursos usados no Azure, é sempre recursos toodelete de práticas recomendadas que não são mais necessários. Você não precisa toodelete cada recurso separadamente de um grupo de recursos. Exclua grupo de recursos de saudação e todos os seus recursos são excluídos automaticamente. 

recurso de saudação toodelete grupo, adicione este código toohello método Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Executar o aplicativo hello

Ele deve levar cerca de cinco minutos para este toorun do aplicativo de console completamente do início toofinish. 

1. aplicativo de console hello toorun, clique em **iniciar**.

2. Antes de pressionar **Enter** toostart recursos de exclusão, você pode levar alguns minutos criação de saudação do tooverify de recursos de saudação em Olá portal do Azure. Clique em Olá implantação status toosee informações sobre a implantação de saudação.

## <a name="next-steps"></a>Próximas etapas
* Se houver problemas com a implantação de hello, a próxima etapa seria toolook em [solucionar erros comuns de implantação do Azure com o Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
* Saiba como toodeploy uma máquina virtual e seus recursos de suporte, revisando [implantar um Azure Máquina Virtual usando o c#](csharp.md).
