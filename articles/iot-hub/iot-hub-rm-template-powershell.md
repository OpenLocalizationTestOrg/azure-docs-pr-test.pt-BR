---
title: Criar um Hub IoT do Azure usando um modelo (PowerShell) | Microsoft Docs
description: Como usar um modelo do Azure Resource Manager para criar um Hub IoT com o PowerShell.
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
ms.openlocfilehash: f83fac6cffc9e58582417324a4348ca3b6220f0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="6a3c7-103">Criar um Hub IoT usando um modelo do Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="6a3c7-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="6a3c7-104">Você pode usar o Gerenciador de Recursos do Azure para criar e gerenciar hubs IoT do Azure de forma programática.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="6a3c7-105">Este tutorial mostra como usar um modelo do Azure Resource Manager para criar um Hub IoT com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="6a3c7-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6a3c7-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6a3c7-107">Este artigo aborda o uso do modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="6a3c7-108">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="6a3c7-109">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-109">An active Azure account.</span></span> <br/><span data-ttu-id="6a3c7-110">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="6a3c7-111">[Azure PowerShell 1.0][lnk-powershell-install] ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="6a3c7-112">O artigo [Como usar o Azure PowerShell com o Azure Resource Manager][lnk-powershell-arm] fornece mais informações sobre como usar o PowerShell e modelos do Azure Resource Manager para criar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-112">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell and Azure Resource Manager templates to create Azure resources.</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="6a3c7-113">Conecte-se à sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="6a3c7-113">Connect to your Azure subscription</span></span>

<span data-ttu-id="6a3c7-114">Em um prompt de comando do PowerShell, digite o seguinte comando para entrar em sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="6a3c7-115">Caso tenha várias assinaturas do Azure, entrar no Azure concede a você acesso a todas as assinaturas do Azure associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="6a3c7-116">Use o comando a seguir para listar as assinaturas do Azure disponíveis para você:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="6a3c7-117">Use o comando a seguir para selecionar a assinatura que você deseja usar para executar os comandos e criar seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="6a3c7-118">Você pode usar a ID ou nome da assinatura da saída do comando anterior:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="6a3c7-119">Você pode usar os comandos a seguir para descobrir onde você pode implantar um Hub IoT e as versões de API com suporte no momento:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-119">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="6a3c7-120">Crie um grupo de recursos para conter o Hub IoT usando o seguinte comando em um dos locais com suporte para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-120">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span></span> <span data-ttu-id="6a3c7-121">Este exemplo cria um grupo de recursos chamado **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="6a3c7-122">Enviar um modelo para criar um hub IoT</span><span class="sxs-lookup"><span data-stu-id="6a3c7-122">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="6a3c7-123">Use um modelo JSON para criar um Hub IoT em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-123">Use a JSON template to create an IoT hub in your resource group.</span></span> <span data-ttu-id="6a3c7-124">Também é possível usar um modelo do Azure Resource Manager para fazer alterações em um hub IoT existente.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-124">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="6a3c7-125">Use um editor de texto para criar um modelo do Azure Resource Manager chamado **template.json** com a seguinte definição de recurso, a fim de criar um novo Hub IoT padrão.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-125">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span></span> <span data-ttu-id="6a3c7-126">Este exemplo adiciona o Hub IoT à região **Leste dos EUA**, cria dois grupos de consumidores (**cg1** e **cg2**) no ponto de extremidade compatível com o Hub de Eventos e usa a versão de API **2016-02-03**.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-126">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span></span> <span data-ttu-id="6a3c7-127">Esse modelo também espera que você passe o nome do Hub IoT como um parâmetro chamado **hubName**.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-127">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="6a3c7-128">Para obter a lista atual de localizações que dão suporte ao Hub IoT, confira o [Status do Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="6a3c7-128">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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

2. <span data-ttu-id="6a3c7-129">Salve o arquivo de modelo do Azure Resource Manager na máquina local.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-129">Save the Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="6a3c7-130">Este exemplo pressupõe que você o salvará em uma pasta chamada **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="6a3c7-131">Execute o seguinte comando para implantar seu novo Hub IoT, passando o nome de seu Hub IoT como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-131">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span></span> <span data-ttu-id="6a3c7-132">Neste exemplo, o nome do hub IoT é `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-132">In this example, the name of the IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="6a3c7-133">O nome do hub IoT deve ser globalmente exclusivo:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-133">The name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="6a3c7-134">A saída exibe as chaves para o Hub IoT criado.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-134">The output displays the keys for the IoT hub you created.</span></span>

5. <span data-ttu-id="6a3c7-135">Para verificar seu aplicativo adicionado ao novo hub IoT, visite o [Portal do Azure][lnk-azure-portal] e exiba sua lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-135">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="6a3c7-136">Como alternativa, use o cmdlet **Get-AzureRmResource** do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-136">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="6a3c7-137">Este aplicativo de exemplo adiciona um Hub IoT Standard S1 pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="6a3c7-138">É possível excluir o hub IoT por meio do [portal do Azure][lnk-azure-portal] ou usando o cmdlet **Remove-AzureRmResource** do PowerShell quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-138">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a3c7-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a3c7-139">Next steps</span></span>

<span data-ttu-id="6a3c7-140">Agora que você implantou um Hub IoT usando um modelo do Azure Resource Manager com o PowerShell, convém explorar ainda mais:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span></span>

* <span data-ttu-id="6a3c7-141">Leia sobre as funcionalidades da [API REST do provedor de recursos Hub IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="6a3c7-141">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="6a3c7-142">Leia a [Visão geral do Azure Resource Manager][lnk-azure-rm-overview] para saber mais sobre os recursos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6a3c7-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="6a3c7-143">Para saber mais sobre como desenvolver para o Hub IoT, veja os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-143">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="6a3c7-144">[Introdução ao SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="6a3c7-144">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="6a3c7-145">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="6a3c7-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="6a3c7-146">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="6a3c7-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6a3c7-147">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6a3c7-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
