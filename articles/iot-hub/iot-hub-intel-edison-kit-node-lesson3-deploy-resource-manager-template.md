---
title: "Conectar-se Edison Intel (nó) tooAzure IoT – lição 3: criar a função de aplicativo | Microsoft Docs"
description: "aplicativo de função do Azure Olá escuta eventos de hub IoT tooAzure, processa as mensagens de entrada e grava o armazenamento de tabela tooAzure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "armazenando dados em nuvem hello, dados armazenados na nuvem, o serviço de nuvem iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8ea0a4cdf978158d70e47eaed57e3de378b638d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="e2507-104">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e2507-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="e2507-105">[As funções do Azure](../../articles/azure-functions/functions-overview.md) é uma solução para executar facilmente *funções* (pequenos pedaços de código) na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="e2507-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="e2507-106">Um aplicativo de função do Azure hospeda execução Olá das funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="e2507-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="e2507-107">O que você fará</span><span class="sxs-lookup"><span data-stu-id="e2507-107">What will you do</span></span>
<span data-ttu-id="e2507-108">Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2507-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="e2507-109">aplicativo de função do Azure Olá escuta eventos de hub IoT tooAzure, processa as mensagens de entrada e grava o armazenamento de tabela tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e2507-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="e2507-110">Olá conta de armazenamento é usada para ler Olá persistentes cópias das mensagens da tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2507-110">hello storage account is used for reading hello persisted copies of messages from Azure table.</span></span> <span data-ttu-id="e2507-111">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="e2507-111">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="e2507-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="e2507-112">What will you learn</span></span>
<span data-ttu-id="e2507-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="e2507-113">In this article, you will learn:</span></span>
* <span data-ttu-id="e2507-114">Como toouse [do Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="e2507-114">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="e2507-115">Como toouse do Azure funcionam aplicativo tooprocess mensagens de hub IoT e gravá-los tooa tabela no armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2507-115">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="e2507-116">Do que você precisa</span><span class="sxs-lookup"><span data-stu-id="e2507-116">What do you need</span></span>
<span data-ttu-id="e2507-117">Você deve ter concluído com sucesso:</span><span class="sxs-lookup"><span data-stu-id="e2507-117">You must have successfully completed:</span></span>
- <span data-ttu-id="e2507-118">[Introdução ao Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="e2507-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="e2507-119">[Criar seu Hub IoT do Azure][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="e2507-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="e2507-120">Aplicativo de exemplo hello aberto</span><span class="sxs-lookup"><span data-stu-id="e2507-120">Open hello sample app</span></span>
<span data-ttu-id="e2507-121">Abra o projeto de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2507-121">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Estrutura do repositório][repo-structure]

* <span data-ttu-id="e2507-123">arquivo Olá Olá `app` subpasta é o arquivo de origem da chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2507-123">hello file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="e2507-124">Esse arquivo de origem contém Olá código toosend uma mensagem 20 vezes tooyour IoT hub e intermitência Olá LED para cada mensagem que ele envia.</span><span class="sxs-lookup"><span data-stu-id="e2507-124">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="e2507-125">Olá `arm-template.json` arquivo é hello Azure Resource Manager modelo que contém um aplicativo de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2507-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="e2507-126">Olá `arm-template-param.json` arquivo é o arquivo de configuração de saudação usado pelo modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="e2507-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="e2507-127">Olá `ReceiveDeviceMessages` subpasta contém o código de Node. js Olá para Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2507-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="e2507-128">Configurar modelos do Azure Resource Manager e criar recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="e2507-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="e2507-129">Saudação de atualização `arm-template-param.json` arquivo no código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2507-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parâmetros do modelo do Azure Resource Manager][arm-template-parameters]

* <span data-ttu-id="e2507-131">Substitua **[o nome de seu Hub IoT]** por **{nome do meu hub}** que foi especificado quando você [criou o Hub IoT e registrou o Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="e2507-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="e2507-132">Substitua **[cadeia de caracteres de prefixo para novos recursos]** pelo prefixo que quiser.</span><span class="sxs-lookup"><span data-stu-id="e2507-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="e2507-133">prefixo de saudação garante que esse nome de recurso de saudação é globalmente exclusivo tooavoid conflito.</span><span class="sxs-lookup"><span data-stu-id="e2507-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="e2507-134">Não use um traço ou o número inicial no prefixo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2507-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="e2507-135">Depois de atualizar Olá `arm-template-param.json` de arquivos, implante Olá recursos tooAzure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2507-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="e2507-136">Leva aproximadamente cinco minutos toocreate esses recursos.</span><span class="sxs-lookup"><span data-stu-id="e2507-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="e2507-137">Durante a criação do recurso hello está em andamento, você pode mover toohello próximo artigo.</span><span class="sxs-lookup"><span data-stu-id="e2507-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="e2507-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="e2507-138">Summary</span></span>
<span data-ttu-id="e2507-139">Você criou seu tooprocess do aplicativo de função do Azure mensagens de hub IoT e o armazenamento do Azure conta toostore essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="e2507-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="e2507-140">Agora você pode implantar e executar mensagens de saudação do exemplo toosend dispositivo para nuvem em Edison.</span><span class="sxs-lookup"><span data-stu-id="e2507-140">You can now deploy and run hello sample toosend device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2507-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2507-141">Next steps</span></span>
<span data-ttu-id="e2507-142">[Execute um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem no Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="e2507-142">[Run a sample application toosend device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md