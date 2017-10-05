---
title: Criar um Hub IoT usando a CLI do Azure (az.py) | Microsoft Docs
description: Como criar um Hub IoT do Azure usando a CLI do Azure 2.0 de plataforma cruzada (az.py).
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
ms.openlocfilehash: 161089159999a4a63a39b059e69a08b7a9297445
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli-20"></a><span data-ttu-id="b8256-103">Criar um Hub IoT usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b8256-103">Create an IoT hub using the Azure CLI 2.0</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="b8256-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="b8256-104">Introduction</span></span>

<span data-ttu-id="b8256-105">É possível usar a CLI do Azure 2.0 (az.py) para criar e gerenciar Hubs IoT do Azure de forma programática.</span><span class="sxs-lookup"><span data-stu-id="b8256-105">You can use Azure CLI 2.0 (az.py) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="b8256-106">Este artigo mostra como usar a CLI do Azure 2.0 (az.py) para criar um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b8256-106">This article shows you how to use the Azure CLI 2.0 (az.py) to create an IoT hub.</span></span>

<span data-ttu-id="b8256-107">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="b8256-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="b8256-108">[CLI do Azure (azure.js)](iot-hub-create-using-cli-nodejs.md) – a CLI para os modelos de implantação clássico e de gerenciamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8256-108">[Azure CLI (azure.js)](iot-hub-create-using-cli-nodejs.md) – the CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="b8256-109">CLI do Azure 2.0 (az.py) – a próxima geração da CLI para o modelo de implantação de gerenciamento de recursos, conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b8256-109">Azure CLI 2.0 (az.py) - the next generation CLI for the resource management deployment model as described in this article.</span></span>

<span data-ttu-id="b8256-110">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="b8256-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b8256-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8256-111">An active Azure account.</span></span> <span data-ttu-id="b8256-112">Se você não tem uma conta, pode criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="b8256-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b8256-113">[CLI do Azure 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="b8256-113">[Azure CLI 2.0][lnk-CLI-install].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="b8256-114">Entre e configure sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="b8256-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="b8256-115">Entre na sua conta do Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b8256-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="b8256-116">Ao prompt de comando, execute o [comando de logon][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="b8256-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>
    
    ```azurecli
    az login
    ```

    <span data-ttu-id="b8256-117">Siga as instruções de autenticação usando o código e entre em sua conta do Azure por meio de um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="b8256-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

2. <span data-ttu-id="b8256-118">Se você tiver várias assinaturas do Azure, entrar o Azure lhe dará acesso a todas as contas do Azure associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="b8256-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="b8256-119">Use o seguinte [comando para listar as contas do Azure][lnk-az-account-command] disponíveis para você:</span><span class="sxs-lookup"><span data-stu-id="b8256-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>
    
    ```azurecli
    az account list 
    ```

    <span data-ttu-id="b8256-120">Use o comando a seguir para selecionar a assinatura que você deseja usar para executar os comandos e criar seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b8256-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="b8256-121">Você pode usar a ID ou nome da assinatura da saída do comando anterior:</span><span class="sxs-lookup"><span data-stu-id="b8256-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="create-an-iot-hub"></a><span data-ttu-id="b8256-122">Crie um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="b8256-122">Create an IoT Hub</span></span>

<span data-ttu-id="b8256-123">Use a CLI do Azure para criar um grupo de recursos e, em seguida, adicione um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b8256-123">Use the Azure CLI to create a resource group and then add an IoT hub.</span></span>

1. <span data-ttu-id="b8256-124">Quando cria um Hub IoT, você deve criá-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8256-124">When you create an IoT hub, you must create it in a resource group.</span></span> <span data-ttu-id="b8256-125">Use um grupo de recursos existente ou execute o seguinte [comando para criar um grupo de recursos][lnk-az-resource-command]:</span><span class="sxs-lookup"><span data-stu-id="b8256-125">Either use an existing resource group, or run the following [command to create a resource group][lnk-az-resource-command]:</span></span>
    
    ```azurecli
     az group create --name {your resource group name} --location westus
    ```

    > [!TIP]
    > <span data-ttu-id="b8256-126">O exemplo anterior cria o grupo de recursos localizado no Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="b8256-126">The previous example creates the resource group in the West US location.</span></span> <span data-ttu-id="b8256-127">Você pode exibir uma lista dos locais disponíveis executando o comando `az account list-locations -o table`.</span><span class="sxs-lookup"><span data-stu-id="b8256-127">You can view a list of available locations by running the command `az account list-locations -o table`.</span></span>
    >
    >

2. <span data-ttu-id="b8256-128">Execute o seguinte [comando para criar um hub IoT][lnk-az-iot-command] no seu grupo de recursos usando um nome globalmente exclusivo para o hub IoT:</span><span class="sxs-lookup"><span data-stu-id="b8256-128">Run the following [command to create an IoT hub][lnk-az-iot-command] in your resource group, using a globally unique name for your IoT hub:</span></span>
    
    ```azurecli
    az iot hub create --name {your iot hub name} --resource-group {your resource group name} --sku S1
    ```

   [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


> [!NOTE]
> <span data-ttu-id="b8256-129">O comando anterior cria um Hub IoT com tipo de preço S1, pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="b8256-129">The previous command creates an IoT hub in the S1 pricing tier for which you are billed.</span></span> <span data-ttu-id="b8256-130">Para saber mais, confira [Preço do Hub IoT do Azure][lnk-iot-pricing].</span><span class="sxs-lookup"><span data-stu-id="b8256-130">For more information, see [Azure IoT Hub pricing][lnk-iot-pricing].</span></span>
>
>

## <a name="remove-an-iot-hub"></a><span data-ttu-id="b8256-131">Remover um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="b8256-131">Remove an IoT Hub</span></span>

<span data-ttu-id="b8256-132">Você pode usar a CLI do Azure para [excluir um recurso individual][lnk-az-resource-command], como um Hub IoT ou excluir um grupo de recursos e todos os seus recursos, incluindo os Hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="b8256-132">You can use the Azure CLI to [delete an individual resource][lnk-az-resource-command], such as an IoT hub, or delete a resource group and all its resources, including any IoT hubs.</span></span>

<span data-ttu-id="b8256-133">Para excluir um Hub IoT, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b8256-133">To delete an IoT hub, run the following command:</span></span>

```azurecli
az iot hub delete --name {your iot hub name} --resource-group {your resource group name}
```

<span data-ttu-id="b8256-134">Para excluir um grupo de recursos e todos os seus recursos, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b8256-134">To delete a resource group and all its resources, run the following command:</span></span>

```azurecli
az group delete --name {your resource group name}
```

## <a name="next-steps"></a><span data-ttu-id="b8256-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8256-135">Next steps</span></span>
<span data-ttu-id="b8256-136">Para saber mais sobre como desenvolver para o Hub IoT, veja os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b8256-136">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="b8256-137">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="b8256-137">[IoT Hub developer guide][lnk-devguide]</span></span>

<span data-ttu-id="b8256-138">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="b8256-138">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b8256-139">[Uso do Portal do Azure para gerenciar o Hub IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="b8256-139">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

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
