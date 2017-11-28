---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Lição 3: criar aplicativo de funções| Microsoft Docs"
description: "O aplicativo de funções do Azure escuta os eventos de Hub IoT do Azure, processa as mensagens recebidas e grava-as no armazenamento de Tabelas do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "armazenar dados na nuvem, dados armazenados na nuvem, serviço de nuvem de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 739b82e9-5d4e-4485-8971-f57cbb682faf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30018cc2d03fc19c13625ef066989a89f21800e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="880f8-104">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="880f8-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="880f8-105">O [Azure Functions](../../articles/azure-functions/functions-overview.md) é uma solução para executar facilmente *funções* (pequenos trechos de código) na nuvem.</span><span class="sxs-lookup"><span data-stu-id="880f8-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="880f8-106">Um aplicativo de funções do Azure hospeda a execução de suas funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="880f8-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="880f8-107">O que você fará</span><span class="sxs-lookup"><span data-stu-id="880f8-107">What will you do</span></span>
<span data-ttu-id="880f8-108">Use um modelo do Azure Resource Manager para criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="880f8-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="880f8-109">O aplicativo de funções do Azure escuta os eventos de Hub IoT do Azure, processa as mensagens recebidas e grava-as no armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="880f8-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="880f8-110">A conta de armazenamento é usada para ler as cópias persistentes de mensagens da tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="880f8-110">The storage account is used for reading the persisted copies of messages from Azure table.</span></span> <span data-ttu-id="880f8-111">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="880f8-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="880f8-112">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="880f8-112">What will you learn</span></span>
<span data-ttu-id="880f8-113">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="880f8-113">In this article, you will learn:</span></span>
* <span data-ttu-id="880f8-114">Como usar o [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) para implantar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="880f8-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="880f8-115">Como usar um aplicativo de funções do Azure para processar mensagens do Hub IoT e gravá-las em uma tabela no armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="880f8-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="880f8-116">Do que você precisa</span><span class="sxs-lookup"><span data-stu-id="880f8-116">What do you need</span></span>
<span data-ttu-id="880f8-117">Você deve ter concluído com sucesso:</span><span class="sxs-lookup"><span data-stu-id="880f8-117">You must have successfully completed:</span></span>
- <span data-ttu-id="880f8-118">[Introdução ao Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="880f8-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="880f8-119">[Criar seu Hub IoT do Azure][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="880f8-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="880f8-120">Abrir o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="880f8-120">Open the sample app</span></span>
<span data-ttu-id="880f8-121">Abra o projeto de exemplo no Visual Studio Code executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="880f8-121">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Estrutura do repositório][repo-structure]

* <span data-ttu-id="880f8-123">O arquivo na subpasta `app` é o arquivo de origem chave.</span><span class="sxs-lookup"><span data-stu-id="880f8-123">The file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="880f8-124">Esse arquivo de origem contém o código para enviar uma mensagem 20 vezes para o hub IoT e piscar o LED para cada mensagem que ele envia.</span><span class="sxs-lookup"><span data-stu-id="880f8-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="880f8-125">O arquivo `arm-template.json` é o modelo do Azure Resource Manager que contém um aplicativo de funções do Azure e uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="880f8-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="880f8-126">O arquivo `arm-template-param.json` é o arquivo de configuração usado pelo modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="880f8-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="880f8-127">A subpasta `ReceiveDeviceMessages` contém o código do Node.js para a função do Azure.</span><span class="sxs-lookup"><span data-stu-id="880f8-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="880f8-128">Configurar modelos do Azure Resource Manager e criar recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="880f8-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="880f8-129">Atualize o arquivo `arm-template-param.json` no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="880f8-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parâmetros do modelo do Azure Resource Manager][arm-template-parameters]

* <span data-ttu-id="880f8-131">Substitua **[o nome de seu Hub IoT]** por **{nome do meu hub}** que foi especificado quando você [criou o Hub IoT e registrou o Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="880f8-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="880f8-132">Substitua **[cadeia de caracteres de prefixo para novos recursos]** pelo prefixo que quiser.</span><span class="sxs-lookup"><span data-stu-id="880f8-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="880f8-133">O prefixo garante que o nome do recurso seja globalmente exclusivo para evitar conflitos.</span><span class="sxs-lookup"><span data-stu-id="880f8-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="880f8-134">Não use um traço nem número inicial no prefixo.</span><span class="sxs-lookup"><span data-stu-id="880f8-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="880f8-135">Depois de atualizar o arquivo `arm-template-param.json`, implante os recursos do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="880f8-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="880f8-136">Levará cerca de cinco minutos para criar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="880f8-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="880f8-137">Embora a criação de recursos esteja em andamento, você pode passar para o próximo artigo.</span><span class="sxs-lookup"><span data-stu-id="880f8-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="880f8-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="880f8-138">Summary</span></span>
<span data-ttu-id="880f8-139">Você criou o aplicativo de funções do Azure para processar as mensagens de hub IoT e uma conta de Armazenamento do Azure para armazenar essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="880f8-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="880f8-140">Agora, é possível implantar e executar o exemplo para enviar mensagens do dispositivo para a nuvem no Edison.</span><span class="sxs-lookup"><span data-stu-id="880f8-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="880f8-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="880f8-141">Next steps</span></span>
<span data-ttu-id="880f8-142">[Executar um aplicativo de exemplo para enviar mensagens do dispositivo para a nuvem no Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="880f8-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-c-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure_c.png
[arm-template-parameters]: /media/iot-hub-intel-edison-lessons/lesson3/arm_para_c.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md