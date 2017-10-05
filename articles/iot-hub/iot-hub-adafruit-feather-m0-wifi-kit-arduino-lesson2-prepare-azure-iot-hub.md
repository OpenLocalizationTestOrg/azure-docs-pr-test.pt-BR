---
title: "Conectar o Arduino ao IoT do Azure - Lição 2: Registrar dispositivo| Microsoft Docs"
description: Crie um grupo de recursos, crie um Hub IoT do Azure e registre o Adafruit Feather M0 WiFi no Hub IoT do Azure usando a CLI do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "conectar o arduino à nuvem, hub iot do azure, nuvem de Internet das coisas, criar dispositivo de hub iot do azure, nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 5edc690b-7a1d-4ebc-b011-ff27bfffe6e8
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c5ad5e900671c7cedd3cdad2c2aa345315de223b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-iot-hub-and-register-your-adafruit-feather-m0-wifi-arduino-board"></a><span data-ttu-id="0a1f4-104">Crie seu Hub IoT e registre sua placa do Adafruit Feather M0 WiFi Arduino</span><span class="sxs-lookup"><span data-stu-id="0a1f4-104">Create your IoT hub and register your Adafruit Feather M0 WiFi Arduino board</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0a1f4-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="0a1f4-105">What you will do</span></span>
* <span data-ttu-id="0a1f4-106">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-106">Create a resource group.</span></span>
* <span data-ttu-id="0a1f4-107">Criar seu hub IoT do Azure no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-107">Create your Azure IoT hub in the resource group.</span></span>
* <span data-ttu-id="0a1f4-108">Adicione sua placa Arduino ao Hub IoT do Azure usando a interface de linha de comando do Azure (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="0a1f4-108">Add your Arduino board to the Azure IoT hub by using the Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="0a1f4-109">Quando você usa a CLI do Azure para adicionar sua placa Arduino ao Hub IoT, o serviço gera uma chave para a autenticação da placa Arduino com o serviço.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-109">When you use the Azure CLI to add your Arduino board to your IoT hub, the service generates a key for your Arduino board to authenticate with the service.</span></span> <span data-ttu-id="0a1f4-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshoot].</span><span class="sxs-lookup"><span data-stu-id="0a1f4-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshoot].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0a1f4-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="0a1f4-111">What you will learn</span></span>
<span data-ttu-id="0a1f4-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="0a1f4-112">In this article, you will learn:</span></span>
* <span data-ttu-id="0a1f4-113">Como usar a CLI do Azure para criar um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-113">How to use the Azure CLI to create an IoT hub.</span></span>
* <span data-ttu-id="0a1f4-114">Como criar uma identidade de dispositivo para sua placa Arduino no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-114">How to create a device identity for your Arduino board in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0a1f4-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="0a1f4-115">What you need</span></span>
* <span data-ttu-id="0a1f4-116">Uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="0a1f4-116">An Azure account</span></span>
* <span data-ttu-id="0a1f4-117">Um computador com a CLI do Azure instalada</span><span class="sxs-lookup"><span data-stu-id="0a1f4-117">A computer with the Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="0a1f4-118">Criar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="0a1f4-118">Create your IoT hub</span></span>
<span data-ttu-id="0a1f4-119">O Hub IoT do Azure ajuda a conectar, monitorar e gerenciar milhões de ativos IoT.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="0a1f4-120">Para criar seu Hub IoT, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="0a1f4-120">To create your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="0a1f4-121">Faça logon em sua conta do Azure executando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a1f4-121">Sign in to your Azure account by running the following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="0a1f4-122">Todas as suas assinaturas disponíveis são listadas após um logon bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="0a1f4-123">Defina a assinatura padrão que deseja usar executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0a1f4-123">Set the default subscription that you want to use by running the following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="0a1f4-124">`subscription ID or name` podem ser encontrados na saída do `az login` ou do comando `az account list`.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-124">`subscription ID or name` can be found in the output of the `az login` or the `az account list` command.</span></span>

3. <span data-ttu-id="0a1f4-125">Registre o provedor executando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-125">Register the provider by running the following command.</span></span> <span data-ttu-id="0a1f4-126">Provedores de recursos são serviços que fornecem recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="0a1f4-127">Você deve registrar o provedor antes de implantar o recurso do Azure que o provedor oferece.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-127">You must register the provider before you can deploy the Azure resource that the provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="0a1f4-128">Crie um grupo de recursos denominado iot-sample na região Oeste dos EUA executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0a1f4-128">Create a resource group named iot-sample in the West US region by running the following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="0a1f4-129">`westus` é o local no qual você cria seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-129">`westus` is the location you create your resource group.</span></span> <span data-ttu-id="0a1f4-130">Se você quiser usar outro local, execute `az account list-locations -o table` para ver todos os locais com suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-130">If you want to use another location, you can run `az account list-locations -o table` to see all the locations Azure supports.</span></span>

5. <span data-ttu-id="0a1f4-131">Crie um hub IoT no grupo de recursos iot-sample executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0a1f4-131">Create an IoT hub in the iot-sample resource group by running the following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="0a1f4-132">Por padrão, a ferramenta cria um Hub IoT no tipo de preços gratuito.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-132">By default, the tool creates an IoT Hub in the Free pricing tier.</span></span> <span data-ttu-id="0a1f4-133">Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="0a1f4-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="0a1f4-134">O nome do hub IoT deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-134">The name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="0a1f4-135">Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-your-arduino-board-in-your-iot-hub"></a><span data-ttu-id="0a1f4-136">Registrar sua placa Arduino no Hub IoT</span><span class="sxs-lookup"><span data-stu-id="0a1f4-136">Register your Arduino board in your IoT hub</span></span>
<span data-ttu-id="0a1f4-137">Cada dispositivo que envia mensagens para/de seu Hub IoT deve ser registrado com uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-137">Each device that sends messages to your IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="0a1f4-138">Registre sua placa Arduino no Hub IoT executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0a1f4-138">Register your Arduino board in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mym0wifi --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="0a1f4-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="0a1f4-139">Summary</span></span>
<span data-ttu-id="0a1f4-140">Você criou um Hub IoT e registrou sua placa Arduino com uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-140">You've created an IoT hub and registered your Arduino board with a device identity in your IoT hub.</span></span> <span data-ttu-id="0a1f4-141">Você está pronto para saber como enviar mensagens da placa Arduino para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0a1f4-141">You're ready to learn how to send messages from your Arduino board to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a1f4-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a1f4-142">Next steps</span></span>
<span data-ttu-id="0a1f4-143">[Criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure para processar e armazenar mensagens do Hub IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="0a1f4-143">[Create an Azure function app and an Azure Storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshoot]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md