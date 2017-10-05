---
title: Criar um Hub IoT usando a CLI do Azure (azure.js) | Microsoft Docs
description: Como criar um Hub IoT do Azure usando a CLI do Azure de plataforma cruzada (azure.js).
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
ms.openlocfilehash: 5e37c6c5e8625ce446ab203f19f9a8b2f1cd5a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli"></a><span data-ttu-id="f829b-103">Criar um Hub IoT usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f829b-103">Create an IoT hub using the Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="f829b-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="f829b-104">Introduction</span></span>

<span data-ttu-id="f829b-105">É possível usar a CLI do Azure (azure.js) para criar e gerenciar Hubs IoT do Azure de forma programática.</span><span class="sxs-lookup"><span data-stu-id="f829b-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="f829b-106">Este artigo mostra como usar a CLI do Azure (azure.js) para criar um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f829b-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span></span>

<span data-ttu-id="f829b-107">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="f829b-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="f829b-108">CLI do Azure (azure.js) – a CLI para os modelos de implantação clássico e de gerenciamento de recursos, conforme descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f829b-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="f829b-109">[CLI do Azure 2.0 (az.py)](iot-hub-create-using-cli.md) – a próxima geração da CLI para o modelo de implantação de gerenciamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="f829b-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="f829b-110">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="f829b-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="f829b-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f829b-111">An active Azure account.</span></span> <span data-ttu-id="f829b-112">Se não tiver uma, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f829b-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="f829b-113">[CLI do Azure 0.10.4][lnk-CLI-install] ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f829b-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="f829b-114">Se já tiver a CLI do Azure instalada, você poderá validar a versão atual no prompt de comando com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f829b-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="f829b-115">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f829b-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f829b-116">A CLI do Azure deve estar no modo Gerenciador de Recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="f829b-116">The Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="f829b-117">Definir sua conta e assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="f829b-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="f829b-118">No prompt de comando, faça logon digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f829b-118">At the command prompt, login by typing the following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="f829b-119">Use o navegador sugerido e o código para autenticar.</span><span class="sxs-lookup"><span data-stu-id="f829b-119">Use the suggested web browser and code to authenticate.</span></span>
1. <span data-ttu-id="f829b-120">Caso tenha várias assinaturas do Azure, conectar-se ao Azure concede a você acesso a todas as assinaturas do Azure associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="f829b-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="f829b-121">Você pode exibir as assinaturas do Azure e identificar qual delas é a padrão, usando o comando:</span><span class="sxs-lookup"><span data-stu-id="f829b-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="f829b-122">Para definir o contexto de assinatura sob o qual você deseja executar o restante dos comandos, use:</span><span class="sxs-lookup"><span data-stu-id="f829b-122">To set the subscription context under which you want to run the rest of the commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="f829b-123">Caso não tenha um grupo de recursos, você poderá criar um chamado **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="f829b-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="f829b-124">O artigo [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] (Usar a CLI do Azure para gerenciar recursos e grupos de recursos do Azure) fornece mais informações sobre como usar a CLI do Azure para gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f829b-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="f829b-125">Crie um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="f829b-125">Create an IoT Hub</span></span>

<span data-ttu-id="f829b-126">Parâmetros requeridos:</span><span class="sxs-lookup"><span data-stu-id="f829b-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="f829b-127">**resource-group**.</span><span class="sxs-lookup"><span data-stu-id="f829b-127">**resource-group**.</span></span> <span data-ttu-id="f829b-128">O nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f829b-128">The resource group name.</span></span> <span data-ttu-id="f829b-129">O formato é alfanumérico, não diferencia maiúsculas de minúsculas, é sublinhado, com hífen e um comprimento de 1 a 64.</span><span class="sxs-lookup"><span data-stu-id="f829b-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="f829b-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="f829b-130">**name**.</span></span> <span data-ttu-id="f829b-131">O nome do Hub IoT a ser criado.</span><span class="sxs-lookup"><span data-stu-id="f829b-131">The name of the IoT hub to be created.</span></span> <span data-ttu-id="f829b-132">O formato é alfanumérico, não diferencia maiúsculas de minúsculas, é sublinhado, com hífen e um comprimento de 3 a 50.</span><span class="sxs-lookup"><span data-stu-id="f829b-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="f829b-133">**location**.</span><span class="sxs-lookup"><span data-stu-id="f829b-133">**location**.</span></span> <span data-ttu-id="f829b-134">O local (região/datacenter do Azure) para provisionar o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f829b-134">The location (azure region/datacenter) to provision the IoT hub.</span></span>
* <span data-ttu-id="f829b-135">**sku-name**.</span><span class="sxs-lookup"><span data-stu-id="f829b-135">**sku-name**.</span></span> <span data-ttu-id="f829b-136">O nome do sku, sendo um destes: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="f829b-136">The name of the sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="f829b-137">Para obter a lista completa mais recente, consulte a página de preços do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f829b-137">For the latest full list, refer to the pricing page for IoT Hub.</span></span>
* <span data-ttu-id="f829b-138">**units**.</span><span class="sxs-lookup"><span data-stu-id="f829b-138">**units**.</span></span> <span data-ttu-id="f829b-139">O número de unidades provisionadas.</span><span class="sxs-lookup"><span data-stu-id="f829b-139">The number of provisioned units.</span></span> <span data-ttu-id="f829b-140">Intervalo: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span><span class="sxs-lookup"><span data-stu-id="f829b-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="f829b-141">Unidades do Hub IoT têm base na contagem total de mensagens e no número de dispositivos que você deseja conectar.</span><span class="sxs-lookup"><span data-stu-id="f829b-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="f829b-142">Para ver todos os parâmetros disponíveis para a criação, você pode usar o comando de ajuda no prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="f829b-142">To see all the parameters available for creation, you can use the help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="f829b-143">Exemplo rápido: para criar um Hub IoT chamado **exampleIoTHubName** no grupo de recursos **exampleResourceGroup**, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f829b-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="f829b-144">Este comando da CLI do Azure cria um Hub IoT Standard S1 pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="f829b-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="f829b-145">Você pode excluir o hub IoT **exampleIoTHubName** usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f829b-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="f829b-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f829b-146">Next steps</span></span>

<span data-ttu-id="f829b-147">Para saber mais sobre como desenvolver para o Hub IoT, veja o seguinte artigo:</span><span class="sxs-lookup"><span data-stu-id="f829b-147">To learn more about developing for IoT Hub, see the following article:</span></span>

* <span data-ttu-id="f829b-148">[SDKs do IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="f829b-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="f829b-149">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="f829b-149">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f829b-150">[Uso do Portal do Azure para gerenciar o Hub IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="f829b-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
