---
title: "Dispositivo simulado e Gateway do IoT do Azure - Introdução | Microsoft Docs"
description: "Introdução ao IoT Gateway Starter Kit, criar o hub IoT do Azure e conecte Gateway toohello IoT hub"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hub iot do Azure, iot gateway, guia de Introdução com hello internet das coisas, iot toolkit"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="8dcbb-104">Introdução ao Kit de Início do Gateway IoT com um dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="8dcbb-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8dcbb-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="8dcbb-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="8dcbb-106">Dispositivo Simulado</span><span class="sxs-lookup"><span data-stu-id="8dcbb-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="8dcbb-107">Neste tutorial, você começar a aprender os fundamentos de saudação do trabalho com [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="8dcbb-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="8dcbb-108">Você estará trabalhando com a NUC da Intel executando o Linux Wind River.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="8dcbb-109">Você aprenderá como tooseamleesly se conectar a sua nuvem de toohello dispositivos usando o Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="8dcbb-110">**Ainda não tem um kit?:** Clique [aqui](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="8dcbb-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="8dcbb-111">Lição 1: Configurar sua NUC</span><span class="sxs-lookup"><span data-stu-id="8dcbb-111">Lesson 1: Configure your NUC</span></span>
![Diagrama de ponta a ponta da Lição 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="8dcbb-113">Nesta lição, você configura NUC Intel (unidade próximo de computação) em Olá Kit como um gateway IoT do Azure, instala pacote do Azure IoT borda Olá em NUC e executar uma exemplo tooverify Olá gateway a funcionalidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="8dcbb-114">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="8dcbb-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="8dcbb-115">Vá muito[configurar NUC Intel como um gateway IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="8dcbb-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="8dcbb-116">Lição 2: Criar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="8dcbb-116">Lesson 2: Create your IoT Hub</span></span>
![Diagrama de ponta a ponta da Lição 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="8dcbb-118">Nesta lição, você instala ferramentas hello e software no computador host.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="8dcbb-119">Em seguida, criar sua conta gratuita do Azure, provisionar seu hub IoT do Azure e criar seu primeiro dispositivo no hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="8dcbb-120">Conclua a Lição 1 antes de iniciar esta lição.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="8dcbb-121">Obter ferramentas Olá</span><span class="sxs-lookup"><span data-stu-id="8dcbb-121">Get hello tools</span></span>
<span data-ttu-id="8dcbb-122">Instale o software e ferramentas de saudação no computador host.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="8dcbb-123">*Estimado tempo toocomplete: 20 minutos*</span><span class="sxs-lookup"><span data-stu-id="8dcbb-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="8dcbb-124">Vá muito[obter ferramentas Olá](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="8dcbb-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="8dcbb-125">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="8dcbb-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="8dcbb-126">Criar seu grupo de recursos, provisionar o hub IoT do Azure primeiro e adicionar o primeiro dispositivo toohello IoT hub usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="8dcbb-127">*Estimado tempo toocomplete: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="8dcbb-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="8dcbb-128">Vá muito[criar um hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="8dcbb-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="8dcbb-129">Lição 3: Receber mensagens de dispositivo simulado hello e ler mensagens de seu hub IoT</span><span class="sxs-lookup"><span data-stu-id="8dcbb-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="8dcbb-130">Nesta lição, você usará configuração de saudação tooautomate scripts e execução de um aplicativo de dispositivo simulado em seu gateway.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="8dcbb-131">aplicativo de dispositivo simulado Hello gera dados de temperatura de exemplo e o envia tooan módulos de hubs de IoT.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="8dcbb-132">Olá pacotes de módulo de hub IoT dados saudação recebidos e o envia tooyour IoT hub por meio da estrutura de gateway Olá fornecida no Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagrama de ponta a ponta da Lição 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="8dcbb-134">Configurar e executar um dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="8dcbb-134">Configure and run a simulated device</span></span>
<span data-ttu-id="8dcbb-135">Prepare os códigos de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-135">Prepare hello sample codes.</span></span> <span data-ttu-id="8dcbb-136">Em seguida, configurar e executar o aplicativo de exemplo hello simulado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="8dcbb-137">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="8dcbb-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="8dcbb-138">Vá muito[configurar e executar um dispositivo simulado](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="8dcbb-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="8dcbb-139">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="8dcbb-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="8dcbb-140">Execute um código de exemplo em suas mensagens de saudação do tooread de computador host do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="8dcbb-141">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="8dcbb-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="8dcbb-142">Vá muito[ler mensagens de seu hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="8dcbb-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="8dcbb-143">Lição 4: Salvar mensagens tooAzure o armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="8dcbb-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="8dcbb-144">Crie um aplicativo de função do Azure que obtém as mensagens de entrada de seu hub IoT e grava o armazenamento de tabela tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagrama de ponta a ponta da Lição 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="8dcbb-146">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8dcbb-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="8dcbb-147">Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="8dcbb-148">*Estimado tempo toocomplete: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="8dcbb-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="8dcbb-149">Vá muito[criar uma conta de armazenamento do Azure e o aplicativo de função do Azure](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="8dcbb-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="8dcbb-150">Ler mensagens mantidas no Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="8dcbb-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="8dcbb-151">Monitorar mensagens de saudação do gateway para a nuvem, como eles são gravados tooAzure o armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="8dcbb-152">*Estimado tempo toocomplete: 5 minutos*</span><span class="sxs-lookup"><span data-stu-id="8dcbb-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="8dcbb-153">Vá muito[ler mensagens mantido no armazenamento de tabela do Azure](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8dcbb-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8dcbb-154">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8dcbb-154">Troubleshooting</span></span>
<span data-ttu-id="8dcbb-155">Se você tiver problemas durante lições hello, procurar soluções Olá [solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="8dcbb-156">Explorar mais</span><span class="sxs-lookup"><span data-stu-id="8dcbb-156">Explore more</span></span>
<span data-ttu-id="8dcbb-157">Visite Olá [zona de desenvolvedor Intel IoT Gateway Kit](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="8dcbb-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
