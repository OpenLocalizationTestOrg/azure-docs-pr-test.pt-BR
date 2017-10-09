---
title: aaaCreate um IoT Hub do Azure usando um modelo (PowerShell) | Microsoft Docs
description: Como toouse uma toocreate de modelo do Azure Resource Manager um IoT Hub com o PowerShell.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="655ee-103">Criar um Hub IoT usando um modelo do Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="655ee-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="655ee-104">Você pode usar o Gerenciador de recursos do Azure toocreate e gerenciar programaticamente os hubs de IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="655ee-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="655ee-105">Este tutorial mostra como toouse uma toocreate de modelo do Azure Resource Manager um hub IoT com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="655ee-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="655ee-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="655ee-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="655ee-107">Este artigo aborda usando o modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="655ee-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="655ee-108">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="655ee-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="655ee-109">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="655ee-109">An active Azure account.</span></span> <br/><span data-ttu-id="655ee-110">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="655ee-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="655ee-111">[Azure PowerShell 1.0][lnk-powershell-install] ou posterior.</span><span class="sxs-lookup"><span data-stu-id="655ee-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="655ee-112">artigo Olá [usando o PowerShell do Azure com o Azure Resource Manager] [ lnk-powershell-arm] fornece mais informações sobre como toouse PowerShell e o Azure Resource Manager modelos toocreate Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="655ee-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="655ee-113">Conecte-se tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="655ee-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="655ee-114">Em um prompt de comando do PowerShell, digite Olá comando toosign em tooyour assinatura do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="655ee-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="655ee-115">Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="655ee-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="655ee-116">Use Olá toolist Olá assinaturas do Azure para você toouse de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="655ee-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="655ee-117">Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toocreate seu hub IoT a seguir.</span><span class="sxs-lookup"><span data-stu-id="655ee-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="655ee-118">Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="655ee-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="655ee-119">Você pode usar o hello comandos toodiscover onde você pode implantar um hub IoT e versões de API Olá atualmente com suporte a seguir:</span><span class="sxs-lookup"><span data-stu-id="655ee-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="655ee-120">Crie um toocontain do grupo de recursos o hub IoT usando Olá seguinte comando em um dos locais de saudação com suporte para o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="655ee-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="655ee-121">Este exemplo cria um grupo de recursos chamado **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="655ee-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="655ee-122">Enviar um toocreate modelo um hub IoT</span><span class="sxs-lookup"><span data-stu-id="655ee-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="655ee-123">Use um modelo JSON toocreate um hub IoT no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="655ee-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="655ee-124">Você também pode usar um hub de IoT do Azure Resource Manager modelo toomake alterações tooan existente.</span><span class="sxs-lookup"><span data-stu-id="655ee-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="655ee-125">Usar um toocreate do editor de texto chamado de um modelo do Azure Resource Manager **template.json** com hello toocreate de definição de recurso a seguir um novo hub IoT padrão.</span><span class="sxs-lookup"><span data-stu-id="655ee-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="655ee-126">Este exemplo adiciona Olá IoT Hub Olá **Leste dos EUA** região, cria dois grupos de consumidores (**cg1** e **cg2**) no ponto de extremidade Olá compatível com o Hub de eventos e usa Olá **2016-02-03** versão da API.</span><span class="sxs-lookup"><span data-stu-id="655ee-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="655ee-127">Esse modelo também que toopass no nome do hub IoT hello como um parâmetro chamado **hubName**.</span><span class="sxs-lookup"><span data-stu-id="655ee-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="655ee-128">Para obter a lista atual Olá locais que dão suporte ao IoT Hub consulte [Status do Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="655ee-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
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

2. <span data-ttu-id="655ee-129">Salve arquivo de modelo de Gerenciador de recursos do Azure Olá em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="655ee-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="655ee-130">Este exemplo pressupõe que você o salvará em uma pasta chamada **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="655ee-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="655ee-131">Execute Olá toodeploy de comando a seguir o novo hub IoT, passando o nome de saudação do seu hub IoT como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="655ee-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="655ee-132">Neste exemplo, o nome de saudação do hub IoT de saudação é `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="655ee-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="655ee-133">nome de saudação do seu hub IoT deve ser globalmente exclusivo:</span><span class="sxs-lookup"><span data-stu-id="655ee-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="655ee-134">saída de Hello exibe chaves Olá para o hub IoT de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="655ee-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="655ee-135">tooverify seu aplicativo adicionado Olá novo hub IoT, visite Olá [portal do Azure] [ lnk-azure-portal] e exibir a lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="655ee-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="655ee-136">Como alternativa, use Olá **Get-AzureRmResource** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="655ee-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="655ee-137">Este aplicativo de exemplo adiciona um Hub IoT Standard S1 pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="655ee-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="655ee-138">Você pode excluir o hub IoT de saudação por meio de saudação [portal do Azure] [ lnk-azure-portal] ou usando Olá **Remove-AzureRmResource** cmdlet do PowerShell quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="655ee-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="655ee-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="655ee-139">Next steps</span></span>

<span data-ttu-id="655ee-140">Agora que você implantou um hub IoT usando um modelo do Gerenciador de recursos do Azure com o PowerShell, você poderá desejar tooexplore adicional:</span><span class="sxs-lookup"><span data-stu-id="655ee-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="655ee-141">Leia sobre os recursos de saudação do hello [provedor de recursos de IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="655ee-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="655ee-142">Leitura [visão geral do Gerenciador de recursos do Azure] [ lnk-azure-rm-overview] toolearn mais sobre os recursos de saudação do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="655ee-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="655ee-143">toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="655ee-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="655ee-144">[Introdução tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="655ee-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="655ee-145">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="655ee-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="655ee-146">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="655ee-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="655ee-147">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="655ee-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
