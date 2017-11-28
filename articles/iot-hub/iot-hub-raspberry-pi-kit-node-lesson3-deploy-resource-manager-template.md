---
title: "Conectar o Raspberry Pi (Nó) ao IoT do Azure - Lição 3: implantação de modelo | Microsoft Docs"
description: "O aplicativo de funções do Azure escuta os eventos de Hub IoT do Azure, processa as mensagens recebidas e grava-as no armazenamento de Tabelas do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "armazenar dados na nuvem, dados armazenados na nuvem, serviço de nuvem de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="7feec-104">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="7feec-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="7feec-105">O [Azure Functions](../azure-functions/functions-overview.md) é uma solução para executar facilmente *funções* (pequenos trechos de código) na nuvem.</span><span class="sxs-lookup"><span data-stu-id="7feec-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="7feec-106">Um aplicativo de funções do Azure hospeda a execução de suas funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="7feec-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="7feec-107">O que você fará</span><span class="sxs-lookup"><span data-stu-id="7feec-107">What you will do</span></span>
<span data-ttu-id="7feec-108">Use um modelo do Azure Resource Manager para criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7feec-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="7feec-109">O aplicativo de funções do Azure escuta os eventos de Hub IoT do Azure, processa as mensagens recebidas e grava-as no armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="7feec-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="7feec-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7feec-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7feec-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7feec-111">What you will learn</span></span>
<span data-ttu-id="7feec-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="7feec-112">In this article, you will learn:</span></span>

* <span data-ttu-id="7feec-113">Como usar o [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) para implantar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7feec-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="7feec-114">Como usar um aplicativo de funções do Azure para processar mensagens do Hub IoT e gravá-las em uma tabela no armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="7feec-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7feec-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7feec-115">What you need</span></span>
<span data-ttu-id="7feec-116">Você deve ter concluído com sucesso:</span><span class="sxs-lookup"><span data-stu-id="7feec-116">You must have successfully completed:</span></span>
* [<span data-ttu-id="7feec-117">Introdução ao Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="7feec-117">Get started with Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)
* [<span data-ttu-id="7feec-118">Criar seu Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="7feec-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-node-get-started.md)

## <a name="open-the-sample-app"></a><span data-ttu-id="7feec-119">Abrir o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="7feec-119">Open the sample app</span></span>
<span data-ttu-id="7feec-120">Abra o projeto de exemplo no Visual Studio Code executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7feec-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Estrutura do repositório](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="7feec-122">O arquivo `app.js` na subpasta `app` é o arquivo de origem chave.</span><span class="sxs-lookup"><span data-stu-id="7feec-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="7feec-123">Esse arquivo de origem contém o código para enviar uma mensagem 20 vezes para o hub IoT e piscar o LED para cada mensagem que ele envia.</span><span class="sxs-lookup"><span data-stu-id="7feec-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="7feec-124">O arquivo `arm-template.json` é o modelo do Azure Resource Manager que contém um aplicativo de funções do Azure e uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7feec-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="7feec-125">O arquivo `arm-template-param.json` é o arquivo de configuração usado pelo modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7feec-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="7feec-126">A subpasta `ReceiveDeviceMessages` contém o código do Node.js para a função do Azure.</span><span class="sxs-lookup"><span data-stu-id="7feec-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="7feec-127">Configurar modelos do Azure Resource Manager e criar recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="7feec-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="7feec-128">Atualize o arquivo `arm-template-param.json` no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="7feec-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parâmetros do modelo do Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="7feec-130">Substitua **[seu nome de Hub IoT]** pelo **{meu nome de hub}** que foi especificado quando você [criou o Hub IoT e registrou o Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="7feec-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="7feec-131">Substitua **[cadeia de caracteres de prefixo para novos recursos]** pelo prefixo que quiser.</span><span class="sxs-lookup"><span data-stu-id="7feec-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="7feec-132">O prefixo garante que o nome do recurso seja globalmente exclusivo para evitar conflitos.</span><span class="sxs-lookup"><span data-stu-id="7feec-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="7feec-133">Não use um traço nem número inicial no prefixo.</span><span class="sxs-lookup"><span data-stu-id="7feec-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="7feec-134">Depois de atualizar o arquivo `arm-template-param.json`, implante os recursos do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7feec-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="7feec-135">Levará cerca de cinco minutos para criar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="7feec-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="7feec-136">Embora a criação de recursos esteja em andamento, você pode passar para o próximo artigo.</span><span class="sxs-lookup"><span data-stu-id="7feec-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="7feec-137">Resumo</span><span class="sxs-lookup"><span data-stu-id="7feec-137">Summary</span></span>
<span data-ttu-id="7feec-138">Você criou o aplicativo de funções do Azure para processar as mensagens de hub IoT e uma conta de Armazenamento do Azure para armazenar essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="7feec-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="7feec-139">Agora você pode implantar e executar o exemplo para enviar mensagens do dispositivo para a nuvem no Pi.</span><span class="sxs-lookup"><span data-stu-id="7feec-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7feec-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7feec-140">Next steps</span></span>
[<span data-ttu-id="7feec-141">Executar o aplicativo de exemplo para enviar mensagens do dispositivo para a nuvem no Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="7feec-141">Run a sample application to send device-to-cloud messages on Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)

