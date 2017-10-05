---
title: Criar um Hub IoT do Azure usando um cmdlet do PowerShell | Microsoft Docs
description: Como usar um cmdlet do PowerShell para criar um hub IoT.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 02227adeb8a9a7463506efa44ddc2977f8aae65a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="2cdeb-103">Criar um hub IoT usando o cmdlet New-AzureRmIotHub</span><span class="sxs-lookup"><span data-stu-id="2cdeb-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="2cdeb-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="2cdeb-104">Introduction</span></span>

<span data-ttu-id="2cdeb-105">É possível usar os cmdlets do Azure PowerShell para criar e gerenciar hubs IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="2cdeb-106">Este tutorial mostra como criar um hub IoT com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="2cdeb-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2cdeb-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2cdeb-108">Este artigo aborda o uso do modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="2cdeb-109">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2cdeb-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-110">An active Azure account.</span></span> <br/><span data-ttu-id="2cdeb-111">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="2cdeb-112">[Cmdlets do Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="2cdeb-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="2cdeb-113">Conecte-se à sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="2cdeb-113">Connect to your Azure subscription</span></span>
<span data-ttu-id="2cdeb-114">Em um prompt de comando do PowerShell, digite o seguinte comando para entrar em sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="2cdeb-115">Caso tenha várias assinaturas do Azure, entrar no Azure concede a você acesso a todas as assinaturas do Azure associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="2cdeb-116">Use o comando a seguir para listar as assinaturas do Azure disponíveis para você:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="2cdeb-117">Use o comando a seguir para selecionar a assinatura que você deseja usar para executar os comandos e criar seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="2cdeb-118">Você pode usar a ID ou nome da assinatura da saída do comando anterior:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="2cdeb-119">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2cdeb-119">Create resource group</span></span>

<span data-ttu-id="2cdeb-120">Você precisa de um grupo de recursos para implantar um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-120">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="2cdeb-121">É possível usar um grupo de recursos existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="2cdeb-122">Você pode usar o seguinte comando para descobrir as localizações em que é possível implantar um hub IoT:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-122">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="2cdeb-123">Para criar um grupo de recursos para o hub IoT em uma das localizações com suporte no Hub IoT, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-123">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="2cdeb-124">Este exemplo cria um grupo de recursos chamado **MyIoTRG1** na região **Leste dos EUA**:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-124">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="2cdeb-125">Crie um hub IoT</span><span class="sxs-lookup"><span data-stu-id="2cdeb-125">Create an IoT hub</span></span>

<span data-ttu-id="2cdeb-126">Para criar um hub IoT no grupo de recursos criado na etapa anterior, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-126">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="2cdeb-127">Este exemplo cria um hub **S1** chamado **MyTestIoTHub** na região **Leste dos EUA**:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-127">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="2cdeb-128">O nome do hub IoT deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-128">The name of the IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="2cdeb-129">É possível listar todos os hubs IoT da assinatura usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-129">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="2cdeb-130">O exemplo anterior adiciona um Hub IoT S1 Standard pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="2cdeb-130">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="2cdeb-131">É possível excluir o hub IoT usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-131">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="2cdeb-132">Como alternativa, você pode remover um grupo de recursos e todos os recursos que ele contém usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-132">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="2cdeb-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2cdeb-133">Next steps</span></span>

<span data-ttu-id="2cdeb-134">Agora que você implantou um hub IoT usando um cmdlet do PowerShell, talvez você deseje explorar ainda mais:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="2cdeb-135">Descubra outros [cmdlets do PowerShell para trabalhar com o hub IoT][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="2cdeb-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="2cdeb-136">Leia sobre as funcionalidades da [API REST do provedor de recursos Hub IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="2cdeb-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="2cdeb-137">Para saber mais sobre como desenvolver para o Hub IoT, veja os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="2cdeb-138">[Introdução ao SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="2cdeb-138">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="2cdeb-139">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="2cdeb-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="2cdeb-140">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="2cdeb-140">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2cdeb-141">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2cdeb-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
