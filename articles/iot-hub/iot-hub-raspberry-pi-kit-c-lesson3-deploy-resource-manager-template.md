---
title: "Connect Raspberry PI (C) tooAzure IoT – lição 3: implantação de modelo | Microsoft Docs"
description: "aplicativo de função do Azure Olá escuta eventos de hub IoT tooAzure, processa as mensagens de entrada e grava o armazenamento de tabela tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "armazenando dados em nuvem hello, dados armazenados na nuvem, o serviço de nuvem iot"
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
ms.openlocfilehash: 11aaad4935681d8b3d338779eec1b19d77cb11e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="2e7a1-104">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2e7a1-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="2e7a1-105">[As funções do Azure](../../articles/azure-functions/functions-overview.md) é uma solução para executar facilmente *funções* (pequenos pedaços de código) na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="2e7a1-106">Um aplicativo de função do Azure hospeda execução Olá das funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="2e7a1-107">O que você fará</span><span class="sxs-lookup"><span data-stu-id="2e7a1-107">What will you do</span></span>
<span data-ttu-id="2e7a1-108">Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="2e7a1-109">aplicativo de função do Azure Olá escuta eventos de hub IoT tooAzure, processa as mensagens de entrada e grava o armazenamento de tabela tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="2e7a1-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2e7a1-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="2e7a1-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="2e7a1-111">What will you learn</span></span>
<span data-ttu-id="2e7a1-112">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="2e7a1-112">In this article, you will learn:</span></span>
* <span data-ttu-id="2e7a1-113">Como toouse [do Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="2e7a1-114">Como toouse do Azure funcionam aplicativo tooprocess mensagens de hub IoT e gravá-los tooa tabela no armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="2e7a1-115">Do que você precisa</span><span class="sxs-lookup"><span data-stu-id="2e7a1-115">What do you need</span></span>
* <span data-ttu-id="2e7a1-116">Você deve ter concluído com sucesso:</span><span class="sxs-lookup"><span data-stu-id="2e7a1-116">You must have successfully completed:</span></span>
- [<span data-ttu-id="2e7a1-117">Introdução ao seu Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="2e7a1-117">Get started with your Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)
- [<span data-ttu-id="2e7a1-118">Criar seu Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="2e7a1-118">Create your Azure IoT hub</span></span>](iot-hub-raspberry-pi-kit-c-get-started.md)

## <a name="open-hello-sample-app"></a><span data-ttu-id="2e7a1-119">Aplicativo de exemplo hello aberto</span><span class="sxs-lookup"><span data-stu-id="2e7a1-119">Open hello sample app</span></span>
<span data-ttu-id="2e7a1-120">Abra o projeto de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e7a1-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Estrutura do repositório](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure_c.png)

* <span data-ttu-id="2e7a1-122">Olá `main.c` arquivo hello `app` subpasta é o arquivo de origem da chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-122">hello `main.c` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="2e7a1-123">Esse arquivo de origem contém Olá código toosend uma mensagem 20 vezes tooyour IoT hub e intermitência Olá LED para cada mensagem que ele envia.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="2e7a1-124">Olá `arm-template.json` arquivo é hello Azure Resource Manager modelo que contém um aplicativo de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-124">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="2e7a1-125">Olá `arm-template-param.json` arquivo é o arquivo de configuração de saudação usado pelo modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-125">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="2e7a1-126">Olá `ReceiveDeviceMessages` subpasta contém o código de Node. js Olá para Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-126">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="2e7a1-127">Configurar modelos do Azure Resource Manager e criar recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="2e7a1-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="2e7a1-128">Saudação de atualização `arm-template-param.json` arquivo no código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-128">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parâmetros do modelo do Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para_c.png)

* <span data-ttu-id="2e7a1-130">Substitua **[seu nome de Hub IoT]** pelo **{meu nome de hub}** que foi especificado quando você [criou o Hub IoT e registrou o Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="2e7a1-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="2e7a1-131">Substitua **[cadeia de caracteres de prefixo para novos recursos]** pelo prefixo que quiser.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="2e7a1-132">prefixo de saudação garante que esse nome de recurso de saudação é globalmente exclusivo tooavoid conflito.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-132">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="2e7a1-133">Não use um traço ou o número inicial no prefixo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-133">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="2e7a1-134">Depois de atualizar Olá `arm-template-param.json` de arquivos, implante Olá recursos tooAzure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2e7a1-134">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="2e7a1-135">Leva aproximadamente cinco minutos toocreate esses recursos.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-135">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="2e7a1-136">Durante a criação do recurso hello está em andamento, você pode mover toohello próximo artigo.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-136">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="2e7a1-137">Resumo</span><span class="sxs-lookup"><span data-stu-id="2e7a1-137">Summary</span></span>
<span data-ttu-id="2e7a1-138">Você criou seu tooprocess do aplicativo de função do Azure mensagens de hub IoT e o armazenamento do Azure conta toostore essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-138">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="2e7a1-139">Agora você pode implantar e executar mensagens de saudação do exemplo toosend dispositivo para nuvem em Pi.</span><span class="sxs-lookup"><span data-stu-id="2e7a1-139">You can now deploy and run hello sample toosend device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e7a1-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e7a1-140">Next steps</span></span>
[<span data-ttu-id="2e7a1-141">Executar um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem</span><span class="sxs-lookup"><span data-stu-id="2e7a1-141">Run a sample application toosend device-to-cloud messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md)

