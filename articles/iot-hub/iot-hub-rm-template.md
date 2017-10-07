---
title: aaaCreate um IoT Hub do Azure usando um modelo (.NET) | Microsoft Docs
description: Como toouse uma toocreate de modelo do Azure Resource Manager um IoT Hub com um programa c#.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="220d7-103">Criar um Hub IoT usando um modelo do Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="220d7-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="220d7-104">Você pode usar o Gerenciador de recursos do Azure toocreate e gerenciar programaticamente os hubs de IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="220d7-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="220d7-105">Este tutorial mostra como toouse uma toocreate de modelo do Azure Resource Manager um hub IoT de um programa c#.</span><span class="sxs-lookup"><span data-stu-id="220d7-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="220d7-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="220d7-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="220d7-107">Este artigo aborda usando o modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="220d7-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="220d7-108">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="220d7-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="220d7-109">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="220d7-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="220d7-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="220d7-110">An active Azure account.</span></span> <br/><span data-ttu-id="220d7-111">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="220d7-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="220d7-112">Uma [conta de armazenamento do Azure][lnk-storage-account] em que é possível armazenar seus arquivos de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="220d7-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="220d7-113">[Azure PowerShell 1.0][lnk-powershell-install] ou posterior.</span><span class="sxs-lookup"><span data-stu-id="220d7-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="220d7-114">Preparar seu projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="220d7-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="220d7-115">No Visual Studio, crie um projeto de Visual C# Windows clássico Desktop usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="220d7-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="220d7-116">Projeto de saudação do nome **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="220d7-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="220d7-117">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="220d7-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="220d7-118">Verifique no Gerenciador de pacotes do NuGet, **incluir pré-lançamento**e em Olá **procurar** pesquisa de página para **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="220d7-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="220d7-119">Selecionar pacote de saudação, clique em **instalar**, na **Revise as alterações** clique em **Okey**, em seguida, clique em **aceito** tooaccept licenças de saudação.</span><span class="sxs-lookup"><span data-stu-id="220d7-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="220d7-120">No Gerenciador de Pacotes do NuGet, procure **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="220d7-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="220d7-121">Clique em **instalar**, na **Revise as alterações** clique **Okey**, em seguida, clique em **aceito** tooaccept licença de saudação.</span><span class="sxs-lookup"><span data-stu-id="220d7-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="220d7-122">Em Program.cs, substituir Olá **usando** instruções com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="220d7-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="220d7-123">Em Program.cs, adicione Olá variáveis estáticas, substituindo os valores de espaço reservado Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="220d7-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="220d7-124">Você fez uma anotação de **ApplicationId**, **SubscriptionId**, **TenantId** e **Password** anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="220d7-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="220d7-125">**O nome da sua conta de armazenamento do Azure** é o nome de saudação do hello conta de armazenamento do Azure onde você armazena seus arquivos de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="220d7-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="220d7-126">**Nome do grupo de recursos** é Olá nome do grupo de recursos de saudação usar ao criar hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="220d7-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="220d7-127">nome de saudação pode ser um grupo de recursos já existente ou novo.</span><span class="sxs-lookup"><span data-stu-id="220d7-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="220d7-128">**Nome da implantação** é um nome para a implantação de saudação, como **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="220d7-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="220d7-129">Enviar um toocreate modelo um hub IoT</span><span class="sxs-lookup"><span data-stu-id="220d7-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="220d7-130">Use um JSON modelo e o parâmetro de arquivo toocreate um hub IoT no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="220d7-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="220d7-131">Você também pode usar um hub de IoT do Azure Resource Manager modelo toomake alterações tooan existente.</span><span class="sxs-lookup"><span data-stu-id="220d7-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="220d7-132">No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto, clique em **Adicionar** e depois em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="220d7-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="220d7-133">Adicione um arquivo JSON chamado **template.json** tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="220d7-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="220d7-134">tooadd um toohello de hub IoT padrão **Leste dos EUA** região, substituir conteúdo de saudação do **template.json** com hello após a definição de recurso.</span><span class="sxs-lookup"><span data-stu-id="220d7-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="220d7-135">Para obter a lista atual Olá de regiões que dão suporte ao IoT Hub consulte [Status do Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="220d7-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. <span data-ttu-id="220d7-136">No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto, clique em **Adicionar** e depois em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="220d7-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="220d7-137">Adicione um arquivo JSON chamado **parameters.json** tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="220d7-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="220d7-138">Substitua o conteúdo de saudação do **parameters.json** com hello segue as informações de parâmetro que define um nome para o hub IoT da nova hello como **{suas iniciais} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="220d7-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="220d7-139">o nome do hub IoT Olá deve ser globalmente exclusivo para que ele deve incluir seu nome ou iniciais:</span><span class="sxs-lookup"><span data-stu-id="220d7-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. <span data-ttu-id="220d7-140">Em **Server Explorer**, conectar tooyour assinatura do Azure e no seu armazenamento do Azure conta criar um contêiner chamado **modelos**.</span><span class="sxs-lookup"><span data-stu-id="220d7-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="220d7-141">Em Olá **propriedades** painel, Olá conjunto **acesso de leitura público** permissões para Olá **modelos** contêiner muito**Blob**.</span><span class="sxs-lookup"><span data-stu-id="220d7-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="220d7-142">Em **Server Explorer**, com o botão direito em Olá **modelos** contêiner e clique **exibir contêiner de Blob**.</span><span class="sxs-lookup"><span data-stu-id="220d7-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="220d7-143">Clique em Olá **carregar Blob** botão, selecione dois arquivos de hello, **parameters.json** e **templates.json**e, em seguida, clique em **abrir** Olá tooupload JSON arquivos toohello **modelos** contêiner.</span><span class="sxs-lookup"><span data-stu-id="220d7-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="220d7-144">Olá URLs de blobs Olá contendo Olá dados JSON são:</span><span class="sxs-lookup"><span data-stu-id="220d7-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="220d7-145">Adicione Olá tooProgram.cs do método a seguir:</span><span class="sxs-lookup"><span data-stu-id="220d7-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="220d7-146">Adicionar Olá toohello de código a seguir **CreateIoTHub** método toosubmit Olá modelo e o parâmetro arquivos toohello Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="220d7-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. <span data-ttu-id="220d7-147">Adicionar Olá toohello de código a seguir **CreateIoTHub** método que exibe o status de saudação e chaves Olá para o hub IoT da nova hello:</span><span class="sxs-lookup"><span data-stu-id="220d7-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="220d7-148">Aplicativo hello completa e execução</span><span class="sxs-lookup"><span data-stu-id="220d7-148">Complete and run hello application</span></span>

<span data-ttu-id="220d7-149">Agora você pode concluir aplicativo hello Olá chamada **CreateIoTHub** método antes de compilar e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="220d7-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="220d7-150">Adicionar Olá após o final do código toohello de saudação **principal** método:</span><span class="sxs-lookup"><span data-stu-id="220d7-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="220d7-151">Clique em **Criar** e **Compilar Solução**.</span><span class="sxs-lookup"><span data-stu-id="220d7-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="220d7-152">Corrija todos os erros.</span><span class="sxs-lookup"><span data-stu-id="220d7-152">Correct any errors.</span></span>

3. <span data-ttu-id="220d7-153">Clique em **depurar** e **iniciar depuração** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="220d7-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="220d7-154">Ele pode levar vários minutos para Olá toorun de implantação.</span><span class="sxs-lookup"><span data-stu-id="220d7-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="220d7-155">tooverify seu aplicativo adicionado Olá novo hub IoT, visite Olá [portal do Azure] [ lnk-azure-portal] e exibir a lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="220d7-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="220d7-156">Como alternativa, use Olá **Get-AzureRmResource** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="220d7-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="220d7-157">Este aplicativo de exemplo adiciona um Hub IoT Standard S1 pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="220d7-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="220d7-158">Você pode excluir o hub IoT de saudação por meio de saudação [portal do Azure] [ lnk-azure-portal] ou usando Olá **Remove-AzureRmResource** cmdlet do PowerShell quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="220d7-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="220d7-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="220d7-159">Next steps</span></span>
<span data-ttu-id="220d7-160">Agora que você implantou um hub IoT usando um modelo do Gerenciador de recursos do Azure com um programa c#, você poderá desejar tooexplore adicional:</span><span class="sxs-lookup"><span data-stu-id="220d7-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="220d7-161">Leia sobre os recursos de saudação do hello [provedor de recursos de IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="220d7-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="220d7-162">Leitura [visão geral do Gerenciador de recursos do Azure] [ lnk-azure-rm-overview] toolearn mais sobre os recursos de saudação do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="220d7-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="220d7-163">toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="220d7-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="220d7-164">[Introdução tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="220d7-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="220d7-165">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="220d7-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="220d7-166">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="220d7-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="220d7-167">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="220d7-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
