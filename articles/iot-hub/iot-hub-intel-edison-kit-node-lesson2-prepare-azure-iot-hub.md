---
title: "Conecte-se Edison Intel (nó) tooAzure IoT - lição 2: registro de dispositivo | Microsoft Docs"
description: "Criar um grupo de recursos, criar um hub IoT do Azure e registrar Edison no hub do Azure IoT hello usando Olá CLI do Azure."
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
ms.openlocfilehash: a70cd8d6a6d620a2cf6226397e061af6cf81e0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-intel-edison"></a><span data-ttu-id="9c07b-103">Criar seu Hub IoT e registrar o Intel Edison</span><span class="sxs-lookup"><span data-stu-id="9c07b-103">Create your IoT hub and register Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9c07b-104">O que você fará</span><span class="sxs-lookup"><span data-stu-id="9c07b-104">What you will do</span></span>
* <span data-ttu-id="9c07b-105">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c07b-105">Create a resource group.</span></span>
* <span data-ttu-id="9c07b-106">Crie o hub IoT do Azure no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c07b-106">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="9c07b-107">Adicione o hub do Intel Edison toohello IoT do Azure usando hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="9c07b-107">Add Intel Edison toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="9c07b-108">Quando você usa Olá CLI do Azure tooadd hub de IoT tooyour Edison, serviço hello gera uma chave para tooauthenticate Edison com serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c07b-108">When you use hello Azure CLI tooadd Edison tooyour IoT hub, hello service generates a key for Edison tooauthenticate with hello service.</span></span> <span data-ttu-id="9c07b-109">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="9c07b-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9c07b-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="9c07b-110">What you will learn</span></span>
<span data-ttu-id="9c07b-111">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="9c07b-111">In this article, you will learn:</span></span>
* <span data-ttu-id="9c07b-112">Como toouse Olá toocreate CLI do Azure com um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c07b-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
* <span data-ttu-id="9c07b-113">Como toocreate uma identidade de dispositivo para Edison em seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c07b-113">How toocreate a device identity for Edison in your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9c07b-114">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="9c07b-114">What you need</span></span>
* <span data-ttu-id="9c07b-115">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c07b-115">An Azure account.</span></span> <span data-ttu-id="9c07b-116">Se não tiver uma conta do Azure, crie uma [conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9c07b-116">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
* <span data-ttu-id="9c07b-117">Você deve ter Olá que CLI do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="9c07b-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="9c07b-118">Criar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="9c07b-118">Create your IoT hub</span></span>
<span data-ttu-id="9c07b-119">O Hub IoT do Azure ajuda a conectar, monitorar e gerenciar milhões de ativos IoT.</span><span class="sxs-lookup"><span data-stu-id="9c07b-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="9c07b-120">toocreate seu hub IoT, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="9c07b-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="9c07b-121">Entre no tooyour conta do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c07b-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="9c07b-122">Todas as suas assinaturas disponíveis são listadas após um logon bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="9c07b-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="9c07b-123">Defina saudação padrão assinatura que você deseja toouse executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c07b-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="9c07b-124">`subscription ID or name`podem ser encontrados na saída Olá Olá `az login` ou hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="9c07b-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="9c07b-125">Registre o provedor de saudação executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c07b-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="9c07b-126">Provedores de recursos são serviços que fornecem recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9c07b-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="9c07b-127">Você deve registrar o provedor de saudação antes de implantar Olá recursos do Azure que Olá ofertas do provedor.</span><span class="sxs-lookup"><span data-stu-id="9c07b-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="9c07b-128">Crie um grupo de recursos denominado exemplo iot na região Oeste dos EUA de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c07b-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="9c07b-129">`westus`é o local de saudação criar seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c07b-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="9c07b-130">Se você quiser toouse em outro local, você pode executar `az account list-locations -o table` toosee todos Olá locais Azure suporta.</span><span class="sxs-lookup"><span data-stu-id="9c07b-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="9c07b-131">Crie um hub IoT no grupo de recursos de exemplo iot Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c07b-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

<span data-ttu-id="9c07b-132">Por padrão, a ferramenta Olá cria um IoT Hub no tipo de preço grátis hello.</span><span class="sxs-lookup"><span data-stu-id="9c07b-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="9c07b-133">Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="9c07b-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="9c07b-134">nome de saudação do seu hub IoT deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9c07b-134">hello name of your IoT hub must be globally unique.</span></span>
> <span data-ttu-id="9c07b-135">Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c07b-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>


## <a name="register-edison-in-your-iot-hub"></a><span data-ttu-id="9c07b-136">Registrar o Edison em seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="9c07b-136">Register Edison in your IoT hub</span></span>
<span data-ttu-id="9c07b-137">Cada dispositivo que envia o hub de IoT tooyour mensagens e recebe mensagens de seu hub IoT deve ser registrado com uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="9c07b-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>

<span data-ttu-id="9c07b-138">Registre o Edison em seu Hub IoT executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="9c07b-138">Register Edison in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id myinteledison --hub-name {my hub name}
```

## <a name="summary"></a><span data-ttu-id="9c07b-139">Resumo</span><span class="sxs-lookup"><span data-stu-id="9c07b-139">Summary</span></span>
<span data-ttu-id="9c07b-140">Você criou um Hub IoT e registrou o Edison com uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c07b-140">You've created an IoT hub and registered Edison with a device identity in your IoT hub.</span></span> <span data-ttu-id="9c07b-141">Você está pronto toolearn como toosend mensagens do hub de IoT tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="9c07b-141">You're ready toolearn how toosend messages from Edison tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c07b-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c07b-142">Next steps</span></span>
<span data-ttu-id="9c07b-143">[Criar um aplicativo de função do Azure e um armazenamento do Azure conta tooprocess e o repositório de hub IoT mensagens][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="9c07b-143">[Create an Azure function app and an Azure Storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md