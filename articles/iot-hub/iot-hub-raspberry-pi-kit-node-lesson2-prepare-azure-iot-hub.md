---
featureFlags: usabilla
title: "Conecte-se framboesa Pi (nó) tooAzure IoT - lição 2: registro de dispositivo | Microsoft Docs"
description: "Criar um grupo de recursos, criar um hub IoT do Azure e registrar Pi no saudação do registro do IoT Hub identidade usando a CLI do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: nuvem raspberry pi, pi cloud connect
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 736215b6-e7e4-46f9-af30-0ded9ffa5204
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 97533298d52d1187c49a4c35ddda922d6e45c87d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-iot-hub-and-register-raspberry-pi-3"></a><span data-ttu-id="ac4af-104">Criar seu Hub IoT e registrar o Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="ac4af-104">Create your IoT hub and register Raspberry Pi 3</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="ac4af-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="ac4af-105">What you will do</span></span>
* <span data-ttu-id="ac4af-106">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ac4af-106">Create a resource group.</span></span>
* <span data-ttu-id="ac4af-107">Crie o hub IoT do Azure no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac4af-107">Create your Azure IoT hub in hello resource group.</span></span>
* <span data-ttu-id="ac4af-108">Adicione framboesa Pi 3 toohello Azure IoT hub usando hello Azure interface de linha de comando (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="ac4af-108">Add Raspberry Pi 3 toohello Azure IoT hub by using hello Azure command-line interface (Azure CLI).</span></span>

<span data-ttu-id="ac4af-109">Quando você usa o hub IoT do Azure CLI tooadd Pi tooyour, o serviço hello gera uma chave para tooauthenticate Pi com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac4af-109">When you use Azure CLI tooadd Pi tooyour IoT hub, hello service generates a key for Pi tooauthenticate with hello service.</span></span> <span data-ttu-id="ac4af-110">Se você tiver problemas, buscar soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ac4af-110">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ac4af-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="ac4af-111">What you will learn</span></span>
<span data-ttu-id="ac4af-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="ac4af-112">In this article, you will learn:</span></span>
* <span data-ttu-id="ac4af-113">Como toouse CLI do Azure toocreate um hub IoT</span><span class="sxs-lookup"><span data-stu-id="ac4af-113">How toouse Azure CLI toocreate an IoT hub</span></span>
* <span data-ttu-id="ac4af-114">Como toocreate uma identidade de dispositivo para Pi em seu hub IoT</span><span class="sxs-lookup"><span data-stu-id="ac4af-114">How toocreate a device identity for Pi in your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ac4af-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="ac4af-115">What you need</span></span>
* <span data-ttu-id="ac4af-116">Uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="ac4af-116">An Azure account</span></span>
* <span data-ttu-id="ac4af-117">Um Mac ou um computador com Windows com hello CLI do Azure instalado</span><span class="sxs-lookup"><span data-stu-id="ac4af-117">A Mac or a Windows computer with hello Azure CLI installed</span></span>

## <a name="create-your-iot-hub"></a><span data-ttu-id="ac4af-118">Criar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="ac4af-118">Create your IoT hub</span></span>
<span data-ttu-id="ac4af-119">O Hub IoT do Azure ajuda a conectar, monitorar e gerenciar milhões de ativos IoT.</span><span class="sxs-lookup"><span data-stu-id="ac4af-119">Azure IoT Hub helps you connect, monitor, and manage millions of IoT assets.</span></span> <span data-ttu-id="ac4af-120">toocreate seu hub IoT, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ac4af-120">toocreate your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="ac4af-121">Entre no tooyour conta do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac4af-121">Sign in tooyour Azure account by running hello following command:</span></span>

   ```bash
   az login
   ```

   <span data-ttu-id="ac4af-122">Todas as suas assinaturas disponíveis são listadas após um logon bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="ac4af-122">All your available subscriptions are listed after a successful sign-in.</span></span>

2. <span data-ttu-id="ac4af-123">Defina saudação padrão assinatura que você deseja toouse executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac4af-123">Set hello default subscription that you want toouse by running hello following command:</span></span>

   ```bash
   az account set --subscription {subscription id or name}
   ```

   <span data-ttu-id="ac4af-124">`subscription ID or name`podem ser encontrados na saída Olá Olá `az login` ou hello `az account list` comando.</span><span class="sxs-lookup"><span data-stu-id="ac4af-124">`subscription ID or name` can be found in hello output of hello `az login` or hello `az account list` command.</span></span>

3. <span data-ttu-id="ac4af-125">Registre o provedor de saudação executando o comando a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac4af-125">Register hello provider by running hello following command.</span></span> <span data-ttu-id="ac4af-126">Provedores de recursos são serviços que fornecem recursos para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac4af-126">Resource providers are services that provide resources for your application.</span></span> <span data-ttu-id="ac4af-127">Você deve registrar o provedor de saudação antes de implantar Olá recursos do Azure que Olá ofertas do provedor.</span><span class="sxs-lookup"><span data-stu-id="ac4af-127">You must register hello provider before you can deploy hello Azure resource that hello provider offers.</span></span>

   ```bash
   az provider register -n "Microsoft.Devices"
   ```
4. <span data-ttu-id="ac4af-128">Crie um grupo de recursos denominado exemplo iot na região Oeste dos EUA de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac4af-128">Create a resource group named iot-sample in hello West US region by running hello following command:</span></span>

   ```bash
   az group create --name iot-sample --location westus
   ```

   <span data-ttu-id="ac4af-129">`westus`é o local de saudação criar seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ac4af-129">`westus` is hello location you create your resource group.</span></span> <span data-ttu-id="ac4af-130">Se você quiser toouse em outro local, você pode executar `az account list-locations -o table` toosee todos Olá locais Azure suporta.</span><span class="sxs-lookup"><span data-stu-id="ac4af-130">If you want toouse another location, you can run `az account list-locations -o table` toosee all hello locations Azure supports.</span></span>
 
5. <span data-ttu-id="ac4af-131">Crie um hub IoT no grupo de recursos de exemplo iot Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac4af-131">Create an IoT hub in hello iot-sample resource group by running hello following command:</span></span>

   ```bash
   az iot hub create --name {my hub name} --resource-group iot-sample
   ```

   <span data-ttu-id="ac4af-132">Por padrão, a ferramenta Olá cria um IoT Hub no tipo de preço grátis hello.</span><span class="sxs-lookup"><span data-stu-id="ac4af-132">By default, hello tool creates an IoT Hub in hello Free pricing tier.</span></span> <span data-ttu-id="ac4af-133">Para saber mais, confira [Preço do Hub IoT do Azure](https://azure.microsoft.com/pricing/details/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="ac4af-133">For more infomation, see [Azure IoT Hub pricing](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

> [!NOTE] 
> <span data-ttu-id="ac4af-134">nome de saudação do seu hub IoT deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ac4af-134">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="ac4af-135">Você pode criar apenas uma edição F1 do Hub IoT do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac4af-135">You can create only one F1 edition of Azure IoT Hub under your Azure subscription.</span></span>

## <a name="register-pi-in-your-iot-hub"></a><span data-ttu-id="ac4af-136">Registrar o Pi em seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="ac4af-136">Register Pi in your IoT hub</span></span>
<span data-ttu-id="ac4af-137">Cada dispositivo que envia o hub de IoT tooyour mensagens e recebe mensagens de seu hub IoT deve ser registrado com uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="ac4af-137">Each device that sends messages tooyour IoT hub and receives messages from your IoT hub must be registered with a unique ID.</span></span> <span data-ttu-id="ac4af-138">Usará tooregister CLI do Azure o Pi e criar um certificado autoassinado do x. 509 para autenticação de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac4af-138">You will use Azure CLI tooregister your Pi and create a self-signed X.509 certificate for device authentication.</span></span>

<span data-ttu-id="ac4af-139">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac4af-139">Run hello following command:</span></span>

```bash
# For Windows command prompt
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir %USERPROFILE%\.iot-hub-getting-started
 
# For macOS or Ubuntu
az iot device create --device-id myraspberrypi --hub-name {my hub name} --x509 --output-dir ~/.iot-hub-getting-started
```

## <a name="summary"></a><span data-ttu-id="ac4af-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="ac4af-140">Summary</span></span>
<span data-ttu-id="ac4af-141">Você criou um Hub IoT do Azure e registrou seu Pi com uma identidade de dispositivo em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ac4af-141">You've created an IoT hub and registered Pi with a device identity in your IoT hub.</span></span> <span data-ttu-id="ac4af-142">Você está pronto toolearn como toosend mensagens do hub de IoT tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="ac4af-142">You're ready toolearn how toosend messages from Pi tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac4af-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac4af-143">Next steps</span></span>
[<span data-ttu-id="ac4af-144">Criar um aplicativo de função do Azure e um tooprocess de conta de armazenamento do Azure e armazenar mensagens de hub IoT</span><span class="sxs-lookup"><span data-stu-id="ac4af-144">Create an Azure function app and an Azure storage account tooprocess and store IoT hub messages</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md)

