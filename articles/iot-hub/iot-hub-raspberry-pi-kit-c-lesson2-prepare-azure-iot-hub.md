---
title: "Conectar Raspberry Pi (C) ao IoT do Azure - Lição 2: registrar dispositivo | Microsoft Docs"
description: Crie um grupo de recursos, crie um Hub IoT do Azure e registre o Pi nele usando a CLI do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: nuvem raspberry pi, pi cloud connect
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 4bcfb071-b3ae-48cc-8ea5-7e7434732287
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d7bfd8f6ae8d15dfe09f06a40a4ab415ff2e0a7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="d138b-104">Criar seu Hub IoT e registrar o Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d138b-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d138b-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="d138b-105">What you will do</span></span>
* <span data-ttu-id="d138b-106">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="d138b-106">Create a resource group.</span></span>
* <span data-ttu-id="d138b-107">Criar seu hub IoT do Azure no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d138b-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="d138b-108">Adicione o Raspberry Pi 3 para o Hub IoT do Azure usando a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="d138b-108">Add Raspberry Pi 3 to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="d138b-109">Quando você usa a CLI do Azure para adicionar o Pi ao Hub IoT, o serviço gera uma chave para autenticar o Pi com o serviço.</span><span class="sxs-lookup"><span data-stu-id="d138b-109">When you use the Azure CLI to add Pi to your IoT hub, the service generates a key for Pi to authenticate with the service.</span></span> <span data-ttu-id="d138b-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d138b-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d138b-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="d138b-111">What you will learn</span></span>
<span data-ttu-id="d138b-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="d138b-112">In this article, you will learn:</span></span>
* <span data-ttu-id="d138b-113">Como usar a CLI do Azure para criar um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d138b-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="d138b-114">Como criar uma identidade de dispositivo para seu Pi no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d138b-114">How to create a device identity for Pi in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d138b-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="d138b-115">What you need</span></span>
* <span data-ttu-id="d138b-116">Uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="d138b-116">An Azure account</span></span>
* <span data-ttu-id="d138b-117">Um computador Mac ou Windows com a CLI do Azure instalada</span><span class="sxs-lookup"><span data-stu-id="d138b-117">A Mac or a Windows computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="d138b-118">Criar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="d138b-118">Create your IoT hub</span></span>
<span data-ttu-id="d138b-119">O Hub IoT do Azure ajuda a conectar, monitorar e gerenciar milhões de ativos IoT.</span><span class="sxs-lookup"><span data-stu-id="d138b-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="d138b-120">Para criar seu Hub IoT, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d138b-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="d138b-121">Faça logon em sua conta do Azure executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d138b-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="d138b-122">Todas as suas assinaturas disponíveis são listadas após um logon bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="d138b-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="d138b-123">Defina a assinatura padrão que deseja usar executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d138b-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="d138b-124">`subscription ID or name` podem ser encontrados na saída do `az login` ou do comando `az account list`.</span><span class="sxs-lookup"><span data-stu-id="d138b-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="d138b-125">Registre o provedor executando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="d138b-125">Register the provider by running the following command.</span></span> <span data-ttu-id="d138b-126">Provedores de recursos são serviços que fornecem recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d138b-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="d138b-127">Você deve registrar o provedor antes de implantar o recurso do Azure que o provedor oferece.</span><span class="sxs-lookup"><span data-stu-id="d138b-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="d138b-128">Crie um grupo de recursos denominado iot-sample na região Oeste dos EUA executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d138b-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="d138b-129">`westus` é o local no qual você cria seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d138b-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="d138b-130">Se você quiser usar outro local, execute `az account list-locations -o table` para ver todos os locais com suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="d138b-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>
 
5. <span data-ttu-id="d138b-131">Crie um hub IoT no grupo de recursos iot-sample executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d138b-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="d138b-132">Por padrão, a ferramenta cria um Hub IoT no tipo de preços gratuito.</span><span class="sxs-lookup"><span data-stu-id="d138b-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="d138b-133">Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="d138b-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="d138b-134">O nome do hub IoT deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="d138b-134">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="d138b-135">Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d138b-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="d138b-136">Registrar o Pi em seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="d138b-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="d138b-137">Cada dispositivo que envia mensagens para/de seu Hub IoT deve ser registrado com uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="d138b-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="d138b-138">Registre seu Pi no hub executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d138b-138">Register Pi in your hub by running following command:</span></span>

```bash
az iot device create --device-id myraspberrypi --hub {my hub name} --resource-group iot-sample
```

## <a name="summary"></a><span data-ttu-id="d138b-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="d138b-139">Summary</span></span>
<span data-ttu-id="d138b-140">Você criou um Hub IoT do Azure e registrou seu Pi com uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d138b-140">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="d138b-141">Você está pronto para saber como enviar mensagens do Pi para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d138b-141">You're ready to learn how to send messages from Pi to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d138b-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d138b-142">Next steps</span></span>
<span data-ttu-id="d138b-143">[Criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure para processar e armazenar mensagens do Hub IoT](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="d138b-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

