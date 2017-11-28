---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 2: registrar dispositivo | Microsoft Docs"
description: 
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Hub iot do Azure, nuvem de Internet das coisas, criar dispositivo de Hub IoT do Azure, SensorTag de TI, bli de TI
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 23cfbe21-22c6-4fe1-ae41-63714a897f12
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d1052ed2fa9e022966e6e71fa2c7d4f18c333b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-azure-iot-hub-and-register-your-device"></a><span data-ttu-id="9c5c3-103">Criar seu Hub IoT do Azure e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="9c5c3-103">Create your Azure IoT hub and register your device</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9c5c3-104">O que você fará</span><span class="sxs-lookup"><span data-stu-id="9c5c3-104">What you will do</span></span>

- <span data-ttu-id="9c5c3-105">Criar um grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="9c5c3-105">Create a resource group</span></span>
- <span data-ttu-id="9c5c3-106">Criar seu primeiro Hub IoT</span><span class="sxs-lookup"><span data-stu-id="9c5c3-106">Create your first IoT hub</span></span>
- <span data-ttu-id="9c5c3-107">Registre seu dispositivo em seu hub IoT usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-107">Register your device in your IoT hub by using hello Azure CLI.</span></span> 

<span data-ttu-id="9c5c3-108">Quando você registra seu dispositivo em seu hub IoT, Olá serviço Azure IoT Hub gera uma chave para tooauthenticate de toouse seu dispositivo com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-108">When you register your device in your IoT hub, hello Azure IoT Hub service generates a key for your device toouse tooauthenticate with hello service.</span></span> 

<span data-ttu-id="9c5c3-109">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9c5c3-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9c5c3-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="9c5c3-110">What you will learn</span></span>

<span data-ttu-id="9c5c3-111">Nesta lição, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="9c5c3-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="9c5c3-112">Como toouse Olá toocreate CLI do Azure com um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-112">How toouse hello Azure CLI toocreate an IoT hub.</span></span>
- <span data-ttu-id="9c5c3-113">Como tooregister um dispositivo em um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-113">How tooregister a device in an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9c5c3-114">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="9c5c3-114">What you need</span></span>

- <span data-ttu-id="9c5c3-115">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-115">An active Azure subscription.</span></span> <span data-ttu-id="9c5c3-116">Se não tiver uma conta do Azure, você pode [criar uma conta gratuita do Azure](http://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-116">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>
- <span data-ttu-id="9c5c3-117">Você deve ter Olá que CLI do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-117">You should have hello Azure CLI installed.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="9c5c3-118">Crie um hub IoT</span><span class="sxs-lookup"><span data-stu-id="9c5c3-118">Create an IoT hub</span></span>

<span data-ttu-id="9c5c3-119">toocreate um hub IoT, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="9c5c3-119">toocreate an IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="9c5c3-120">Entre no tooyour conta do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c5c3-120">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="9c5c3-121">Todas as suas assinaturas disponíveis serão listadas após uma entrada bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-121">All your available subscriptions will be listed after a successful sign-in.</span></span>

2. <span data-ttu-id="9c5c3-122">Defina o valor padrão de saudação assinatura do Azure que você deseja toouse executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c5c3-122">Set hello default Azure subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="9c5c3-123">`subscription ID or name`podem ser encontrados na saída Olá Olá `az login` ou hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-123">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="9c5c3-124">Registre o provedor de saudação executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-124">Register hello provider by running hello following command.</span></span> <span data-ttu-id="9c5c3-125">Provedores de recursos são serviços que fornecem recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-125">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="9c5c3-126">Você deve registrar o provedor de saudação antes de implantar Olá recursos do Azure que Olá ofertas do provedor.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-126">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```

4. <span data-ttu-id="9c5c3-127">Criar um grupo de recursos denominado `iot-gateway` na região do Oeste dos EUA Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c5c3-127">Create a resource group named `iot-gateway` in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-gateway --location westus
   ```
   
   <span data-ttu-id="9c5c3-128">`westus`é o local de saudação criar seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-128">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="9c5c3-129">Se você quiser toouse em outro local, você pode executar `az account list-locations -o table` toosee todos Olá locais Azure suporta.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-129">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>

5. <span data-ttu-id="9c5c3-130">Criar um hub IoT em Olá `iot-gateway` grupo de recursos executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c5c3-130">Create an IoT hub in hello `iot-gateway` resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-gateway
   ```

<span data-ttu-id="9c5c3-131">Por padrão, a ferramenta Olá cria um IoT Hub no tipo de preço grátis hello.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-131">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="9c5c3-132">Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="9c5c3-132">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE]
> <span data-ttu-id="9c5c3-133">nome de saudação do seu hub IoT deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-133">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="9c5c3-134">Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-134">You can create only one F1 edition of Azure Iot Hub under your Azure subscription.</span></span>

## <a name="register-your-device-in-your-iot-hub"></a><span data-ttu-id="9c5c3-135">Registrar seu dispositivo em seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="9c5c3-135">Register your device in your IoT hub</span></span>

<span data-ttu-id="9c5c3-136">Cada dispositivo que envia o hub de IoT tooyour mensagens e recebe mensagens de seu hub IoT deve ser registrado com uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-136">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span>
<span data-ttu-id="9c5c3-137">Registre seu dispositivo no Hub IoT do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="9c5c3-137">Register your device in your IoT hub by running following command:</span></span>

```bash
az iot device create --device-id mydevice --hub-name {my hub name} --resource-group iot-gateway
```

## <a name="summary"></a><span data-ttu-id="9c5c3-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="9c5c3-138">Summary</span></span>

<span data-ttu-id="9c5c3-139">Você criou um Hub IoT do Azure e registrou seu dispositivo lógico com uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-139">You've created an IoT hub and registered your logical device with a device identity in your IoT hub.</span></span> <span data-ttu-id="9c5c3-140">Você está pronto toolearn como tooconfigure e executar um gateway exemplo aplicativo toosend de dados do seu hub IoT tooyour de dispositivo físico Olá de nuvem.</span><span class="sxs-lookup"><span data-stu-id="9c5c3-140">You're ready toolearn how tooconfigure and run a gateway sample application toosend data from your physical device tooyour IoT hub in hello cloud.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c5c3-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c5c3-141">Next steps</span></span>
[<span data-ttu-id="9c5c3-142">Configurar e executar um aplicativo de exemplo de upload de nuvem de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="9c5c3-142">Configure and run a simulated device cloud upload sample application</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)