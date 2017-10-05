---
title: "Conectar o Intel Edison (Nó) ao IoT do Azure - Lição 2: registrar dispositivo| Microsoft Docs"
description: Crie um grupo de recursos, crie um Hub IoT do Azure e registre o Edison no Hub IoT do Azure usando a CLI do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: c1465cc2-d0d9-4326-967c-64d95b61dd54
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 81584c1b7314c4331ac059b8e3ed782970588ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="5e329-103">Criar seu Hub IoT e registrar o Intel Edison</span><span class="sxs-lookup"><span data-stu-id="5e329-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5e329-104">O que você fará</span><span class="sxs-lookup"><span data-stu-id="5e329-104">What you will do</span></span>
* <span data-ttu-id="5e329-105">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e329-105">Create a resource group.</span></span>
* <span data-ttu-id="5e329-106">Criar seu hub IoT do Azure no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e329-106">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="5e329-107">Adicionar o Intel Edison ao Hub IoT do Azure usando a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="5e329-107">Add Intel Edison to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="5e329-108">Quando você usa a CLI do Azure para adicionar o Edison ao Hub IoT, o serviço gera uma chave para a autenticação do Edison com o serviço.</span><span class="sxs-lookup"><span data-stu-id="5e329-108">When you use the Azure CLI to add Edison to your IoT hub, the service generates a key for Edison to authenticate with the service.</span></span> <span data-ttu-id="5e329-109">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="5e329-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e329-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="5e329-110">What you will learn</span></span>
<span data-ttu-id="5e329-111">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="5e329-111">In this article, you will learn:</span></span>
* <span data-ttu-id="5e329-112">Como usar a CLI do Azure para criar um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e329-112">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="5e329-113">Como criar uma identidade de dispositivo para o Edison em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e329-113">How to create a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e329-114">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="5e329-114">What you need</span></span>
* <span data-ttu-id="5e329-115">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e329-115">An Azure account.</span></span> <span data-ttu-id="5e329-116">Se não tiver uma conta do Azure, crie uma [conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5e329-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="5e329-117">Você deve ter a CLI do Azure instalada.</span><span class="sxs-lookup"><span data-stu-id="5e329-117">You should have the Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="5e329-118">Criar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="5e329-118">Create your IoT hub</span></span>
<span data-ttu-id="5e329-119">O Hub IoT do Azure ajuda a conectar, monitorar e gerenciar milhões de ativos IoT.</span><span class="sxs-lookup"><span data-stu-id="5e329-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="5e329-120">Para criar seu Hub IoT, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5e329-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="5e329-121">Faça logon em sua conta do Azure executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5e329-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="5e329-122">Todas as suas assinaturas disponíveis são listadas após um logon bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="5e329-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="5e329-123">Defina a assinatura padrão que deseja usar executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5e329-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="5e329-124">`subscription ID or name` podem ser encontrados na saída do `az login` ou do comando `az account list`.</span><span class="sxs-lookup"><span data-stu-id="5e329-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="5e329-125">Registre o provedor executando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="5e329-125">Register the provider by running the following command.</span></span> <span data-ttu-id="5e329-126">Provedores de recursos são serviços que fornecem recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5e329-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="5e329-127">Você deve registrar o provedor antes de implantar o recurso do Azure que o provedor oferece.</span><span class="sxs-lookup"><span data-stu-id="5e329-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="5e329-128">Crie um grupo de recursos denominado iot-sample na região Oeste dos EUA executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5e329-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="5e329-129">`westus` é o local no qual você cria seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e329-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="5e329-130">Se você quiser usar outro local, execute `az account list-locations -o table` para ver todos os locais com suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e329-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="5e329-131">Crie um hub IoT no grupo de recursos iot-sample executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5e329-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="5e329-132">Por padrão, a ferramenta cria um Hub IoT no tipo de preços gratuito.</span><span class="sxs-lookup"><span data-stu-id="5e329-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="5e329-133">Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="5e329-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="5e329-134">O nome do hub IoT deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5e329-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="5e329-135">Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e329-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="5e329-136">Registrar o Edison em seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="5e329-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="5e329-137">Cada dispositivo que envia mensagens para/de seu Hub IoT deve ser registrado com uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="5e329-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="5e329-138">Registre o Edison em seu Hub IoT executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5e329-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="5e329-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="5e329-139">Summary</span></span>
<span data-ttu-id="5e329-140">Você criou um Hub IoT e registrou o Edison com uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e329-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="5e329-141">Você está pronto para saber como enviar mensagens do Edison para seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e329-141">You're ready to learn how to send messages from Edison to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e329-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e329-142">Next steps</span></span>
<span data-ttu-id="5e329-143">[Criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure para processar e armazenar mensagens do Hub IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="5e329-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md