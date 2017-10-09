---
title: "Dispositivo SensorTag e Gateway de IoT do Azure - Introdução | Microsoft Docs"
description: "Introdução ao IoT Gateway Starter Kit, criar o hub IoT do Azure e conecte-se o hub IoT de toohello SensorTag e Gateway"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hub iot do Azure, iot gateway, guia de Introdução com hello internet das coisas, iot toolkit"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="9d945-104">Introdução ao Kit de Início do Gateway IoT com um SensorTag</span><span class="sxs-lookup"><span data-stu-id="9d945-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d945-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="9d945-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="9d945-106">Dispositivo Simulado</span><span class="sxs-lookup"><span data-stu-id="9d945-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="9d945-107">Neste tutorial, você começar a aprender os fundamentos de saudação do trabalho com [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="9d945-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="9d945-108">Você trabalhará com NUC Intel que está executando o Linux vento rio e hello [SensorTag de TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="9d945-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="9d945-109">Você aprenderá como tooseamleesly se conectar a sua nuvem de toohello dispositivos usando o Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9d945-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="9d945-110">**Ainda não tem um kit?:** Clique [aqui](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="9d945-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="9d945-111">**Não é tem um SensorTag?:** [Comece com um dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md) ou [compre um SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="9d945-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="9d945-112">Lição 1: Configurar sua NUC</span><span class="sxs-lookup"><span data-stu-id="9d945-112">Lesson 1: Configure your NUC</span></span>
![Diagrama de ponta a ponta da Lição 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="9d945-114">Nesta lição, você configura NUC Intel (unidade próximo de computação) em Olá Kit como um gateway IoT do Azure, instala pacote do Azure IoT borda Olá em NUC e executar uma exemplo tooverify Olá gateway a funcionalidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d945-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="9d945-115">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="9d945-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="9d945-116">Vá muito[configurar NUC Intel como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="9d945-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="9d945-117">Lição 2: Criar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="9d945-117">Lesson 2: Create your IoT Hub</span></span>
![Diagrama de ponta a ponta da Lição 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="9d945-119">Nesta lição, você instala ferramentas hello e software no computador host.</span><span class="sxs-lookup"><span data-stu-id="9d945-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="9d945-120">Em seguida, criar sua conta gratuita do Azure, provisionar seu hub IoT do Azure e criar seu primeiro dispositivo no hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d945-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="9d945-121">Conclua a Lição 1 antes de iniciar esta lição.</span><span class="sxs-lookup"><span data-stu-id="9d945-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="9d945-122">Obter ferramentas Olá</span><span class="sxs-lookup"><span data-stu-id="9d945-122">Get hello tools</span></span>
<span data-ttu-id="9d945-123">Instale o software e ferramentas de saudação no computador host.</span><span class="sxs-lookup"><span data-stu-id="9d945-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="9d945-124">*Estimado tempo toocomplete: 20 minutos*</span><span class="sxs-lookup"><span data-stu-id="9d945-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="9d945-125">Vá muito[obter ferramentas Olá](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="9d945-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="9d945-126">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="9d945-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="9d945-127">Criar seu grupo de recursos, provisionar o hub IoT do Azure primeiro e adicionar o primeiro dispositivo toohello IoT hub usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d945-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="9d945-128">*Estimado tempo toocomplete: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="9d945-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="9d945-129">Vá muito[criar um hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="9d945-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="9d945-130">Lição 3: Receber mensagens de SensorTag e ler mensagens do seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="9d945-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="9d945-131">Nesta lição, você usará configuração de saudação tooautomate scripts e execução de um aplicativo de exemplo Bilitar no seu gateway.</span><span class="sxs-lookup"><span data-stu-id="9d945-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="9d945-132">Esses aplicativos usam um conjunto de módulos tooaggregate e transformar dados, processam comandos ou executam diversas tarefas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="9d945-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="9d945-133">Os módulos comunicam-se uns com os outros por meio de um agente de mensagem.</span><span class="sxs-lookup"><span data-stu-id="9d945-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="9d945-134">aplicativo de exemplo Hello tem um módulo Bilitar e um módulo de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9d945-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="9d945-135">módulo de Bilitar Olá recebe dados de Bilitar SensorTag.</span><span class="sxs-lookup"><span data-stu-id="9d945-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="9d945-136">Olá pacotes de módulo de hub IoT dados saudação recebidos e o envia tooyour IoT hub por meio da estrutura de gateway Olá fornecida no Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="9d945-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagrama de ponta a ponta da Lição 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="9d945-138">Configurar e executar o aplicativo de exemplo hello Bilitar</span><span class="sxs-lookup"><span data-stu-id="9d945-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="9d945-139">Configure a conectividade de saudação entre SensorTag e seu gateway.</span><span class="sxs-lookup"><span data-stu-id="9d945-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="9d945-140">Em seguida, conclua a configuração de saudação e executar o aplicativo de exemplo hello Bilitar.</span><span class="sxs-lookup"><span data-stu-id="9d945-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="9d945-141">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="9d945-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="9d945-142">Vá muito[configurar e executar hello Bilitar aplicativo de exemplo](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="9d945-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="9d945-143">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="9d945-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="9d945-144">Execute código de exemplo no host do seu computador tooread mensagens de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9d945-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="9d945-145">*Estimado tempo toocomplete: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="9d945-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="9d945-146">Vá muito[ler mensagens de seu hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="9d945-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="9d945-147">Lição 4: Salvar mensagens tooAzure o armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="9d945-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="9d945-148">Crie um aplicativo de função do Azure que obtém as mensagens de entrada de seu hub IoT e grava o armazenamento de tabela tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9d945-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagrama de ponta a ponta da Lição 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="9d945-150">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9d945-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="9d945-151">Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d945-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="9d945-152">*Estimado tempo toocomplete: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="9d945-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="9d945-153">Vá muito[criar uma conta de armazenamento do Azure e o aplicativo de função do Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="9d945-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="9d945-154">Ler mensagens mantidas no Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="9d945-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="9d945-155">Monitorar mensagens de saudação do gateway para a nuvem, como eles são gravados tooAzure o armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="9d945-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="9d945-156">*Estimado tempo toocomplete: 5 minutos*</span><span class="sxs-lookup"><span data-stu-id="9d945-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="9d945-157">Vá muito[ler mensagens mantido no armazenamento de tabela do Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9d945-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9d945-158">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9d945-158">Troubleshooting</span></span>
<span data-ttu-id="9d945-159">Se você tiver problemas durante lições hello, procurar soluções Olá [solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="9d945-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="9d945-160">Explorar mais</span><span class="sxs-lookup"><span data-stu-id="9d945-160">Explore more</span></span>
<span data-ttu-id="9d945-161">Visite Olá [zona de desenvolvedor Intel IoT Gateway Kit](http://software.intel.com/iot/microsoft-azure) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="9d945-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
