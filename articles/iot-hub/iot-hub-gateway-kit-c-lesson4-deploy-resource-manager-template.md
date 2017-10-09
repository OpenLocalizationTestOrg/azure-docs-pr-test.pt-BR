---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 4: criar aplicativo de funções | Microsoft Docs"
description: "Salvar mensagens de hub do Intel NUC tooyour IoT, gravá-los tooAzure o armazenamento de tabela e, em seguida, lê-los da nuvem de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "armazenando dados em nuvem hello, dados armazenados na nuvem, o serviço de nuvem iot"
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
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="f91ef-104">Criar um aplicativo de funções do Azure e uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f91ef-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="f91ef-105">As funções do Azure é uma solução para executar facilmente _funções_ (pequenos pedaços de código) na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="f91ef-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="f91ef-106">Um aplicativo de função do Azure hospeda execução Olá das funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="f91ef-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="f91ef-107">O que você fará</span><span class="sxs-lookup"><span data-stu-id="f91ef-107">What you will do</span></span>

- <span data-ttu-id="f91ef-108">Use um toocreate de modelo do Azure Resource Manager, um aplicativo de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f91ef-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="f91ef-109">aplicativo de função do Azure Olá escuta eventos de hub IoT tooAzure, processa as mensagens de entrada e grava o armazenamento de tabela tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f91ef-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="f91ef-110">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f91ef-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="f91ef-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="f91ef-111">What you will learn</span></span>

<span data-ttu-id="f91ef-112">Nesta lição, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="f91ef-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f91ef-113">Como toouse toodeploy do Gerenciador de recursos do Azure recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f91ef-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="f91ef-114">Como toouse do Azure funcionam aplicativo tooprocess mensagens de IoT Hub e gravá-los tooa tabela no armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f91ef-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f91ef-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="f91ef-115">What you need</span></span>

<span data-ttu-id="f91ef-116">Você deve ter concluído lições anteriores Olá com êxito:</span><span class="sxs-lookup"><span data-stu-id="f91ef-116">You must have successfully completed hello previous lessons:</span></span>

- <span data-ttu-id="f91ef-117">[Lesson 1: Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) (Lição 1: Configurar a NUC da Intel como um gateway IoT)</span><span class="sxs-lookup"><span data-stu-id="f91ef-117">[Lesson 1: Set up your Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>
- <span data-ttu-id="f91ef-118">[Lesson 2: Get your host computer and Azure IoT hub ready](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md) (Lição 2: Prepare seu computador host e hub do IoT do Azure)</span><span class="sxs-lookup"><span data-stu-id="f91ef-118">[Lesson 2: Get your host computer and Azure IoT hub ready](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>
- [<span data-ttu-id="f91ef-119">Lição 3: Receber mensagens de SensorTag e ler mensagens do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="f91ef-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="f91ef-120">Abrir um aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="f91ef-120">Open a sample app</span></span>

<span data-ttu-id="f91ef-121">Vá tooyour `iot-hub-c-intel-nuc-gateway-getting-started` pasta do repositório, arquivos de configuração de saudação inicializar e projeto de exemplo hello, em seguida, abra no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f91ef-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![estrutura do repositório](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="f91ef-123">Olá `arm-template.json` arquivo é hello Azure Resource Manager modelo que contém um aplicativo de função do Azure e uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f91ef-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="f91ef-124">Olá `arm-template-param.json` arquivo é o arquivo de configuração de saudação usado pelo modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="f91ef-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="f91ef-125">Olá `ReceiveDeviceMessages` subpasta contém o código de Node. js Olá para Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="f91ef-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="f91ef-126">Configurar modelos do Azure Resource Manager e criar recursos no Azure</span><span class="sxs-lookup"><span data-stu-id="f91ef-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="f91ef-127">Saudação de atualização `arm-template-param.json` arquivo no código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f91ef-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm template json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="f91ef-129">Substitua `[your IoT Hub name]` pelo `{my hub name}` especificado na Lição 2.</span><span class="sxs-lookup"><span data-stu-id="f91ef-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="f91ef-130">Depois de atualizar Olá `arm-template-param.json` de arquivos, implante Olá recursos tooAzure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f91ef-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="f91ef-131">Use `iot-gateway` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação na lição 2.</span><span class="sxs-lookup"><span data-stu-id="f91ef-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="f91ef-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="f91ef-132">Summary</span></span>

<span data-ttu-id="f91ef-133">Você criou seu tooprocess do aplicativo de função do Azure mensagens de hub IoT e o armazenamento do Azure conta toostore essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="f91ef-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="f91ef-134">Agora você pode ler as mensagens enviadas pelo hub IoT de tooyour de gateway.</span><span class="sxs-lookup"><span data-stu-id="f91ef-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f91ef-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f91ef-135">Next steps</span></span>
<span data-ttu-id="f91ef-136">[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md) (Ler as mensagens persistidas no Armazenamento de Tabelas do Azure).</span><span class="sxs-lookup"><span data-stu-id="f91ef-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
