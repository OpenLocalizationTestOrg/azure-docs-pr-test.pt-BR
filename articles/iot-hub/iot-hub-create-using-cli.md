---
title: aaaCreate um IoT Hub usando a CLI do Azure (az.py) | Microsoft Docs
description: "Como toocreate um hub IoT do Azure usando Olá plataforma cruzada do Azure CLI 2.0 (az.py)."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-hub
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 9c9639235c2ac343e6ceb9578291dafaea26ea24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli-20"></a><span data-ttu-id="0cc89-103">Criar um hub IoT usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0cc89-103">Create an IoT hub using hello Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="0cc89-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="0cc89-104">Introduction</span></span>

<span data-ttu-id="0cc89-105">Você pode usar a CLI do Azure 2.0 (az.py) toocreate e gerenciar programaticamente os hubs de IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc89-105">You can use Azure CLI 2.0 (az.py) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="0cc89-106">Este artigo mostra como toouse Olá CLI do Azure 2.0 (az.py) toocreate um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0cc89-106">This article shows you how toouse hello Azure CLI 2.0 (az.py) toocreate an IoT hub.</span></span>

<span data-ttu-id="0cc89-107">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cc89-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="0cc89-108">[CLI do Azure (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.</span><span class="sxs-lookup"><span data-stu-id="0cc89-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – hello CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="0cc89-109">Azure CLI 2.0 (az.py) - Olá próxima geração CLI para Olá recurso Gerenciamento modelo de implantação conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0cc89-109">Azure CLI 2.0 (az.py) - hello next generation CLI for hello resource management deployment model as described in this article.</span></span>

<span data-ttu-id="0cc89-110">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cc89-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0cc89-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc89-111">An active Azure account.</span></span> <span data-ttu-id="0cc89-112">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0cc89-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0cc89-113">[CLI do Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="0cc89-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="0cc89-114">Entre e configure sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="0cc89-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="0cc89-115">Entre no tooyour conta do Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0cc89-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="0cc89-116">No prompt de comando do hello, execute Olá [comando login][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="0cc89-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="0cc89-117">Siga Olá instruções tooauthenticate usando código hello e entrar tooyour conta do Azure por meio de um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="0cc89-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

2. <span data-ttu-id="0cc89-118">Se você tiver várias assinaturas do Azure, entrar tooAzure concede acesso tooall Olá associadas com suas credenciais de contas do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc89-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="0cc89-119">Use os seguintes Olá [toolist comando Olá contas do Azure] [ lnk-az-account-command] disponíveis para você toouse:</span><span class="sxs-lookup"><span data-stu-id="0cc89-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="0cc89-120">Use Olá assinatura tooselect de comando que você deseja toouse toorun Olá comandos toocreate seu hub IoT a seguir.</span><span class="sxs-lookup"><span data-stu-id="0cc89-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="0cc89-121">Você pode usar a ID ou nome de assinatura de saudação da saída de saudação do comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="0cc89-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="0cc89-122">Crie um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="0cc89-122">Create an IoT Hub</span></span>

<span data-ttu-id="0cc89-123">Use Olá CLI do Azure toocreate um grupo de recursos e, em seguida, adicione um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0cc89-123">Use hello Azure CLI toocreate a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="0cc89-124">Quando cria um Hub IoT, você deve criá-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0cc89-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="0cc89-125">Use um grupo de recursos existente, ou execute seguinte Olá [comando toocreate um grupo de recursos][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="0cc89-125">Either use an existing resource group, or run hello following [command toocreate a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="0cc89-126">exemplo de anterior Olá cria o grupo de recursos Olá Olá local Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="0cc89-126">hello previous example creates hello resource group in hello West US location.</span></span> <span data-ttu-id="0cc89-127">Você pode exibir uma lista de locais disponíveis, executando o comando Olá `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="0cc89-127">You can view a list of available locations by running hello command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="0cc89-128">Execute seguinte Olá [toocreate comando um hub IoT] [ lnk-az-iot-command] no seu grupo de recursos, usando um nome exclusivo para o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="0cc89-128">Run hello following [command toocreate an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="0cc89-129">comando anterior Olá cria um hub IoT no hello S1 preço para o qual você é cobrado.</span><span class="sxs-lookup"><span data-stu-id="0cc89-129">hello previous command creates an IoT hub in hello S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="0cc89-130">Para saber mais, confira [Preço do Hub IoT do Azure][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="0cc89-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="0cc89-131">Remover um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="0cc89-131">Remove an IoT Hub</span></span>

<span data-ttu-id="0cc89-132">Você pode usar o hello CLI do Azure muito[excluir um recurso individual][lnk-az-resource-command], como um hub IoT ou excluir um grupo de recursos e todos os seus recursos, incluindo qualquer hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="0cc89-132">You can use hello Azure CLI too[delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="0cc89-133">toodelete um hub IoT, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cc89-133">toodelete an IoT hub, run hello following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="0cc89-134">toodelete um grupo de recursos e todos os seus recursos, Olá execução seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0cc89-134">toodelete a resource group and all its resources, run hello following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="0cc89-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0cc89-135">Next steps</span></span>
<span data-ttu-id="0cc89-136">toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cc89-136">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="0cc89-137">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="0cc89-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="0cc89-138">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="0cc89-138">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0cc89-139">[Usando Olá toomanage portal do Azure IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="0cc89-139">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-devguide]: iot-hub-devguide.md
[lnk-portal]: iot-hub-create-through-portal.md 
