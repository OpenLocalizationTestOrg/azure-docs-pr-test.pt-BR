---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 4: criar aplicativo de funções | Microsoft Docs"
description: Salve mensagens da NUC da Intel para o hub IoT, grave-as no Armazenamento de Tabelas do Azure e, em seguida, leia-as na nuvem.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "armazenar dados na nuvem, dados armazenados na nuvem, serviço de nuvem de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 717c91e8332660f19d596c05a8a23afd8df1d51c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="f0aa3-104">Criar um aplicativo de funções do Azure e uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f0aa3-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="f0aa3-105">O Azure Functions é uma solução para executar _funções_ (pequenos trechos de código) com facilidade na nuvem.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="f0aa3-106">Um aplicativo de funções do Azure hospeda a execução de suas funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="f0aa3-107">O que você fará</span><span class="sxs-lookup"><span data-stu-id="f0aa3-107">What you will do</span></span>

- <span data-ttu-id="f0aa3-108">Use um modelo do Azure Resource Manager para criar um aplicativo de funções do Azure e uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="f0aa3-109">O aplicativo de funções do Azure escuta os eventos de Hub IoT do Azure, processa as mensagens recebidas e grava-as no armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="f0aa3-110">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f0aa3-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="f0aa3-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="f0aa3-111">What you will learn</span></span>

<span data-ttu-id="f0aa3-112">Nesta lição, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="f0aa3-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f0aa3-113">Como usar o Azure Resource Manager para implantar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="f0aa3-114">Como usar um aplicativo de funções do Azure para processar mensagens do Hub IoT e gravá-las em uma tabela no armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f0aa3-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="f0aa3-115">What you need</span></span>

<span data-ttu-id="f0aa3-116">Você deve ter concluído com sucesso as lições anteriores:</span><span class="sxs-lookup"><span data-stu-id="f0aa3-116">You must have successfully completed the previous lessons:</span></span>

- <span data-ttu-id="f0aa3-117">[Lesson 1: Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) (Lição 1: Configurar a NUC da Intel como um gateway IoT)</span><span class="sxs-lookup"><span data-stu-id="f0aa3-117">[Lesson 1: Set up your Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>
- <span data-ttu-id="f0aa3-118">[Lesson 2: Get your host computer and Azure IoT hub ready](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md) (Lição 2: Prepare seu computador host e hub do IoT do Azure)</span><span class="sxs-lookup"><span data-stu-id="f0aa3-118">[Lesson 2: Get your host computer and Azure IoT hub ready](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>
- [<span data-ttu-id="f0aa3-119">Lição 3: Receber mensagens de SensorTag e ler mensagens do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="f0aa3-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="f0aa3-120">Abrir um aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="f0aa3-120">Open a sample app</span></span>

<span data-ttu-id="f0aa3-121">Vá para sua pasta do repositório `iot-hub-c-intel-nuc-gateway-getting-started`, inicialize os arquivos de configuração e, em seguida, abra o projeto de exemplo no código do Visual Studio, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f0aa3-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![estrutura do repositório](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="f0aa3-123">O arquivo `arm-template.json` é o modelo do Azure Resource Manager que contém um aplicativo de funções do Azure e uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="f0aa3-124">O arquivo `arm-template-param.json` é o arquivo de configuração usado pelo modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="f0aa3-125">A subpasta `ReceiveDeviceMessages` contém o código do Node.js para a função do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="f0aa3-126">Configurar modelos do Azure Resource Manager e criar recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="f0aa3-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="f0aa3-127">Atualize o arquivo `arm-template-param.json` no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm template json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="f0aa3-129">Substitua `[your IoT Hub name]` pelo `{my hub name}` especificado na Lição 2.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="f0aa3-130">Depois de atualizar o arquivo `arm-template-param.json`, implante os recursos do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f0aa3-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="f0aa3-131">Use `iot-gateway` como o valor de `{resource group name}` se não tiver alterado o valor na Lição 2.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="f0aa3-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="f0aa3-132">Summary</span></span>

<span data-ttu-id="f0aa3-133">Você criou o aplicativo de funções do Azure para processar as mensagens de hub IoT e uma conta de Armazenamento do Azure para armazenar essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="f0aa3-134">Agora você pode ler as mensagens enviadas pelo gateway para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f0aa3-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0aa3-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0aa3-135">Next steps</span></span>
<span data-ttu-id="f0aa3-136">[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md) (Ler as mensagens persistidas no Armazenamento de Tabelas do Azure).</span><span class="sxs-lookup"><span data-stu-id="f0aa3-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
