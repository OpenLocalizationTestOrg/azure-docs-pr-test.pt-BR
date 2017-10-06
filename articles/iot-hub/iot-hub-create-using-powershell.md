---
title: aaaCreate um IoT Hub do Azure usando um cmdlet do PowerShell | Microsoft Docs
description: Como toouse uma toocreate de cmdlet do PowerShell um hub IoT.
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
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="00a77-103">Criar um hub IoT usando o cmdlet Olá AzureRmIotHub novo</span><span class="sxs-lookup"><span data-stu-id="00a77-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="00a77-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="00a77-104">Introduction</span></span>

<span data-ttu-id="00a77-105">Você pode usar toocreate de cmdlets do PowerShell do Azure e gerenciar os hubs IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="00a77-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="00a77-106">Este tutorial mostra como toocreate um hub IoT com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00a77-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="00a77-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="00a77-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="00a77-108">Este artigo aborda usando o modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="00a77-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="00a77-109">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="00a77-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="00a77-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="00a77-110">An active Azure account.</span></span> <br/><span data-ttu-id="00a77-111">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="00a77-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="00a77-112">[Cmdlets do Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="00a77-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="00a77-113">Conecte-se tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="00a77-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="00a77-114">Em um prompt de comando do PowerShell, digite Olá comando toosign em tooyour assinatura do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="00a77-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="00a77-115">Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="00a77-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="00a77-116">Use Olá toolist Olá assinaturas do Azure para você toouse de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="00a77-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="00a77-117">Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toocreate seu hub IoT a seguir.</span><span class="sxs-lookup"><span data-stu-id="00a77-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="00a77-118">Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="00a77-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="00a77-119">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="00a77-119">Create resource group</span></span>

<span data-ttu-id="00a77-120">Você precisa de um grupo de recursos toodeploy um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="00a77-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="00a77-121">É possível usar um grupo de recursos existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="00a77-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="00a77-122">Você pode usar o hello seguintes comando toodiscover Olá locais onde você pode implantar um hub IoT:</span><span class="sxs-lookup"><span data-stu-id="00a77-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="00a77-123">toocreate um grupo de recursos para o hub IoT em um dos locais de saudação com suporte para o IoT Hub, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="00a77-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="00a77-124">Este exemplo cria um grupo de recursos chamado **MyIoTRG1** em Olá **Leste dos EUA** região:</span><span class="sxs-lookup"><span data-stu-id="00a77-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="00a77-125">Crie um hub IoT</span><span class="sxs-lookup"><span data-stu-id="00a77-125">Create an IoT hub</span></span>

<span data-ttu-id="00a77-126">toocreate um hub IoT no grupo de recursos de saudação criado na etapa anterior de saudação, Olá use comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="00a77-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="00a77-127">Este exemplo cria um **S1** hub chamado **MyTestIoTHub** em Olá **Leste dos EUA** região:</span><span class="sxs-lookup"><span data-stu-id="00a77-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="00a77-128">nome de saudação do hub IoT de saudação deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="00a77-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="00a77-129">Você pode listar todos os hubs de IoT Olá em sua assinatura usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="00a77-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="00a77-130">exemplo anterior Hello adiciona um IoT Hub de padrão de S1 para o qual você é cobrado.</span><span class="sxs-lookup"><span data-stu-id="00a77-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="00a77-131">Você pode excluir o hub IoT de saudação usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="00a77-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="00a77-132">Como alternativa, você pode remover um grupo de recursos e todos os recursos nele usando o comando a seguir de saudação de hello:</span><span class="sxs-lookup"><span data-stu-id="00a77-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="00a77-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00a77-133">Next steps</span></span>

<span data-ttu-id="00a77-134">Agora que você implantou um hub IoT usando um cmdlet do PowerShell, você poderá desejar tooexplore adicional:</span><span class="sxs-lookup"><span data-stu-id="00a77-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="00a77-135">Descubra outros [cmdlets do PowerShell para trabalhar com o hub IoT][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="00a77-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="00a77-136">Leia sobre os recursos de saudação do hello [provedor de recursos de IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="00a77-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="00a77-137">toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="00a77-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="00a77-138">[Introdução tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="00a77-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="00a77-139">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="00a77-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="00a77-140">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="00a77-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="00a77-141">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="00a77-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
