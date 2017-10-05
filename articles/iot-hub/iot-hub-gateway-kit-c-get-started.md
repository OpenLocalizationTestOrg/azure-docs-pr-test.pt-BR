---
title: "Dispositivo SensorTag e Gateway de IoT do Azure - Introdução | Microsoft Docs"
description: "Introdução ao Kit de Início do Gateway IoT, crie seu Hub IoT do Azure e conecte o SensorTag e o Gateway ao Hub IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "hub iot do azure, gateway iot, introdução à Internet das coisas, kit de ferramentas do iot"
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
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="47222-104">Introdução ao Kit de Início do Gateway IoT com um SensorTag</span><span class="sxs-lookup"><span data-stu-id="47222-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="47222-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="47222-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="47222-106">Dispositivo Simulado</span><span class="sxs-lookup"><span data-stu-id="47222-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="47222-107">Neste tutorial, você começa aprendendo as noções básicas de como trabalhar com o [Kit de Início do Gateway IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="47222-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="47222-108">Você estará trabalhando com a NUC da Intel executando o Linux Wind River e o [SensorTag de TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="47222-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="47222-109">Você aprenderá a conectar seus dispositivos diretamente à nuvem usando o Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="47222-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="47222-110">**Ainda não tem um kit?:** Clique [aqui](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="47222-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="47222-111">**Não é tem um SensorTag?:** [Comece com um dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md) ou [compre um SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="47222-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="47222-112">Lição 1: Configurar sua NUC</span><span class="sxs-lookup"><span data-stu-id="47222-112">Lesson 1: Configure your NUC</span></span>
![Diagrama de ponta a ponta da Lição 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="47222-114">Nesta lição, você configura a NUC (Próxima Unidade de Computação) da Intel no Kit como um gateway IoT do Azure, instala o pacote do Azure IoT Edge na NUC e executa um aplicativo de exemplo para verificar a funcionalidade do gateway.</span><span class="sxs-lookup"><span data-stu-id="47222-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="47222-115">*Tempo estimado para conclusão: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="47222-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="47222-116">Vá para [Configurar a NUC da Intel como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="47222-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="47222-117">Lição 2: Criar seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="47222-117">Lesson 2: Create your IoT Hub</span></span>
![Diagrama de ponta a ponta da Lição 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="47222-119">Nesta lição, você instala os softwares e as ferramentas no computador host.</span><span class="sxs-lookup"><span data-stu-id="47222-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="47222-120">Em seguida, você cria sua conta gratuita do Azure, provisiona seu Hub IoT do Azure e cria seu primeiro dispositivo no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="47222-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="47222-121">Conclua a Lição 1 antes de iniciar esta lição.</span><span class="sxs-lookup"><span data-stu-id="47222-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="47222-122">Obter as ferramentas</span><span class="sxs-lookup"><span data-stu-id="47222-122">Get the tools</span></span>
<span data-ttu-id="47222-123">Instale os softwares e as ferramentas no computador host.</span><span class="sxs-lookup"><span data-stu-id="47222-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="47222-124">*Tempo estimado para conclusão: 20 minutos*</span><span class="sxs-lookup"><span data-stu-id="47222-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="47222-125">Acesse [Obter as ferramentas](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="47222-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="47222-126">Criar um Hub IoT e registrar seu dispositivo</span><span class="sxs-lookup"><span data-stu-id="47222-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="47222-127">Crie seu grupo de recursos, provisione seu primeiro Hub IoT do Azure e adicione seu primeiro dispositivo ao Hub IoT usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="47222-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="47222-128">*Tempo estimado para conclusão: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="47222-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="47222-129">Acessar [Criar um Hub IoT e registrar seu dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="47222-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="47222-130">Lição 3: Receber mensagens de SensorTag e ler mensagens do seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="47222-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="47222-131">Nesta lição, você usará scripts para automatizar a configuração e a execução de um aplicativo de exemplo BLE em seu gateway.</span><span class="sxs-lookup"><span data-stu-id="47222-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="47222-132">Esses aplicativos usam uma coleção de módulos para agregar e transformar dados, processam comandos ou executam diversas tarefas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="47222-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="47222-133">Os módulos comunicam-se uns com os outros por meio de um agente de mensagem.</span><span class="sxs-lookup"><span data-stu-id="47222-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="47222-134">O aplicativo de exemplo tem um módulo BLE e um módulo de Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="47222-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="47222-135">O módulo BLE recebe dados do SensorTag do BLE.</span><span class="sxs-lookup"><span data-stu-id="47222-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="47222-136">O módulo do hub IoT compacta os dados recebidos e os envia para o hub IoT por meio da estrutura de gateway fornecida no Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="47222-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagrama de ponta a ponta da Lição 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="47222-138">Configurar e executar o aplicativo BLE de exemplo</span><span class="sxs-lookup"><span data-stu-id="47222-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="47222-139">Configurar a conectividade entre o SensorTag e o gateway.</span><span class="sxs-lookup"><span data-stu-id="47222-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="47222-140">Em seguida, concluir a configuração e executar o aplicativo de exemplo BLE.</span><span class="sxs-lookup"><span data-stu-id="47222-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="47222-141">*Tempo estimado para conclusão: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="47222-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="47222-142">Vá para [Configurar e executar o aplicativo BLE de exemplo](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="47222-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="47222-143">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="47222-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="47222-144">Execute um código de exemplo no computador host para ler mensagens de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="47222-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="47222-145">*Tempo estimado para conclusão: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="47222-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="47222-146">Acessar [Ler mensagens do Hub IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="47222-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="47222-147">Lição 4: salvar mensagens no Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="47222-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="47222-148">Crie um aplicativo de funções do Azure que obtenha as mensagens recebidas de seu Hub IoT e as grave-as no Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="47222-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagrama de ponta a ponta da Lição 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="47222-150">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="47222-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="47222-151">Use um modelo do Azure Resource Manager para criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="47222-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="47222-152">*Tempo estimado para conclusão: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="47222-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="47222-153">Acesse [Criar um aplicativo de funções do Azure e uma Conta de armazenamento do Azure](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="47222-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="47222-154">Ler mensagens mantidas no Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="47222-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="47222-155">Monitore as mensagens do gateway para a nuvem conforme elas são gravadas no Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="47222-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="47222-156">*Tempo estimado para conclusão: 5 minutos*</span><span class="sxs-lookup"><span data-stu-id="47222-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="47222-157">Acesse [Ler mensagens mantidas no Armazenamento de Tabelas do Azure](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="47222-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="47222-158">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="47222-158">Troubleshooting</span></span>
<span data-ttu-id="47222-159">Se tiver problemas durante as lições, procure por soluções no artigo [Solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="47222-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="47222-160">Explorar mais</span><span class="sxs-lookup"><span data-stu-id="47222-160">Explore more</span></span>
<span data-ttu-id="47222-161">Visite a [Zona do desenvolvedor de Kit do Gateway IoT da Intel](http://software.intel.com/iot/microsoft-azure) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="47222-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>