---
title: aaaCreate um hub IoT usando a CLI do Azure (azure.js) | Microsoft Docs
description: "Como toocreate um hub IoT do Azure usando Olá CLI do Azure de plataforma cruzada (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="4d009-103">Criar um hub IoT usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4d009-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="4d009-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="4d009-104">Introduction</span></span>

<span data-ttu-id="4d009-105">Você pode usar a CLI do Azure (azure.js) toocreate e gerenciar programaticamente os hubs de IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d009-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="4d009-106">Este artigo mostra como toouse Olá CLI do Azure (azure.js) toocreate um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4d009-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="4d009-107">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d009-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="4d009-108">CLI do Azure (azure.js) – hello CLI para hello clássico e modelos de implantação de gerenciamento de recurso conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4d009-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="4d009-109">[2.0 do CLI do Azure (az.py)](iot-hub-create-using-cli.md) -Olá próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d009-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="4d009-110">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d009-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4d009-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d009-111">An active Azure account.</span></span> <span data-ttu-id="4d009-112">Se não tiver uma, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="4d009-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="4d009-113">[CLI do Azure 0.10.4][lnk-CLI-install] ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4d009-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="4d009-114">Se você já tiver Olá CLI do Azure instalado, você pode validar a versão atual Olá no prompt de comando Olá com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d009-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="4d009-115">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4d009-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4d009-116">Olá CLI do Azure deve estar no modo do Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="4d009-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="4d009-117">Definir sua conta e assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="4d009-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="4d009-118">No prompt de comando hello, logon digitando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d009-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="4d009-119">Saudação de uso sugerido navegador da web e tooauthenticate de código.</span><span class="sxs-lookup"><span data-stu-id="4d009-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="4d009-120">Se você tiver várias assinaturas do Azure, conectar-se tooAzure concede acesso tooall hello Azure assinaturas associadas com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="4d009-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="4d009-121">Você pode exibir hello assinaturas do Azure e identificar qual é o padrão de saudação, usando o comando hello:</span><span class="sxs-lookup"><span data-stu-id="4d009-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="4d009-122">uso de comandos de contexto de assinatura de saudação tooset sob a qual você deseja toorun restante Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="4d009-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="4d009-123">Caso não tenha um grupo de recursos, você poderá criar um chamado **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="4d009-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="4d009-124">artigo Olá [usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos] [ lnk-CLI-arm] fornece mais informações sobre como toouse Olá CLI do Azure toomanage Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="4d009-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="4d009-125">Crie um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="4d009-125">Create an IoT Hub</span></span>

<span data-ttu-id="4d009-126">Parâmetros requeridos:</span><span class="sxs-lookup"><span data-stu-id="4d009-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="4d009-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="4d009-127">**resource-group**.</span></span> <span data-ttu-id="4d009-128">nome do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d009-128">hello resource group name.</span></span> <span data-ttu-id="4d009-129">formato de saudação é sublinhado alfanumérico, não diferencia maiusculas de minúsculas e hífen, comprimento de 1 a 64.</span><span class="sxs-lookup"><span data-stu-id="4d009-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="4d009-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="4d009-130">**name**.</span></span> <span data-ttu-id="4d009-131">nome de saudação do hello IoT hub toobe criado.</span><span class="sxs-lookup"><span data-stu-id="4d009-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="4d009-132">formato de saudação é sublinhado alfanumérico, não diferencia maiusculas de minúsculas e hífen, comprimento de 3 a 50.</span><span class="sxs-lookup"><span data-stu-id="4d009-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="4d009-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="4d009-133">**location**.</span></span> <span data-ttu-id="4d009-134">hub Olá local (região/datacenter do azure) tooprovision Olá IoT.</span><span class="sxs-lookup"><span data-stu-id="4d009-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="4d009-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="4d009-135">**sku-name**.</span></span> <span data-ttu-id="4d009-136">nome de saudação do sku hello, um dos: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="4d009-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="4d009-137">Para lista de completo mais recente Olá, consulte toohello página de preços para o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4d009-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="4d009-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="4d009-138">**units**.</span></span> <span data-ttu-id="4d009-139">número de saudação de unidades provisionadas.</span><span class="sxs-lookup"><span data-stu-id="4d009-139">hello number of provisioned units.</span></span> <span data-ttu-id="4d009-140">Intervalo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="4d009-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="4d009-141">Unidades de IoT Hub são baseadas no número de contagem e hello sua mensagem total de dispositivos que você deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4d009-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="4d009-142">toosee todos os parâmetros disponíveis para a criação de hello, você pode usar o comando de ajuda de saudação no prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="4d009-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="4d009-143">Exemplo rápido: toocreate chamado de um IoT Hub **exampleIoTHubName** no grupo de recursos de saudação **exampleResourceGroup**, execute hello seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4d009-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="4d009-144">Este comando da CLI do Azure cria um Hub IoT Standard S1 pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="4d009-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="4d009-145">Você pode excluir o hub IoT de saudação **exampleIoTHubName** usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4d009-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="4d009-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d009-146">Next steps</span></span>

<span data-ttu-id="4d009-147">toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4d009-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="4d009-148">[SDKs do IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="4d009-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="4d009-149">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="4d009-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4d009-150">[Usando Olá toomanage portal do Azure IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="4d009-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
