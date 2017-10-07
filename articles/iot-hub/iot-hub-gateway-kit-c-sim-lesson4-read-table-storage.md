---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 4: armazenamento de tabelas | Microsoft Docs"
description: "Salvar mensagens de hub do Intel NUC tooyour IoT, gravá-los tooAzure o armazenamento de tabela e, em seguida, lê-los da nuvem de saudação."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "recuperar dados da nuvem, serviço de nuvem de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 78e4b6ea-968d-401e-a7dc-8f9acdb3ec1a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 43e299d63bbbe10d4d867af25e700c3a7cc07c53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="8a0e4-104">Ler mensagens mantidas no Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="8a0e4-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="8a0e4-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="8a0e4-105">What you will do</span></span>

- <span data-ttu-id="8a0e4-106">Execute o aplicativo de exemplo hello gateway no gateway que envia o hub de IoT tooyour mensagens.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-106">Run hello gateway sample application on your gateway that sends messages tooyour IoT hub.</span></span>
- <span data-ttu-id="8a0e4-107">Execute o código de exemplo em suas mensagens de tooread do computador host no seu armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-107">Run sample code on your host computer tooread messages in your Azure Table storage.</span></span>

<span data-ttu-id="8a0e4-108">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="8a0e4-108">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8a0e4-109">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="8a0e4-109">What you will learn</span></span>

<span data-ttu-id="8a0e4-110">Como Olá toouse gulp ferramenta toorun Olá exemplo tooread mensagens de código em seu armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-110">How toouse hello gulp tool toorun hello sample code tooread messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8a0e4-111">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="8a0e4-111">What you need</span></span>

<span data-ttu-id="8a0e4-112">Você tem êxito Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="8a0e4-112">You have have successfully done hello following tasks:</span></span>

- <span data-ttu-id="8a0e4-113">[Criado Olá aplicativo de função do Azure e a conta de armazenamento do Azure Olá](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="8a0e4-113">[Created hello Azure function app and hello Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="8a0e4-114">[Execute o aplicativo de exemplo hello gateway](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="8a0e4-114">[Run hello gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="8a0e4-115">[Ler mensagens do Hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="8a0e4-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="8a0e4-116">Obtenha cadeias de conexão do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8a0e4-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="8a0e4-117">No início desta lição, você criou com êxito uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="8a0e4-118">cadeia de conexão tooget Olá Olá do Azure da conta de armazenamento, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a0e4-118">tooget hello connection string of hello Azure storage account, run hello following commands:</span></span>

* <span data-ttu-id="8a0e4-119">Liste todas suas contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="8a0e4-120">Obtenha a cadeia de conexão do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="8a0e4-121">Use `iot-gateway` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação na lição 2.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-121">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="8a0e4-122">Configurar conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="8a0e4-122">Configure hello device connection</span></span>

<span data-ttu-id="8a0e4-123">Saudação de atualização `config-azure.json` arquivos de forma que o código de exemplo hello que é executado no computador de host Olá pode ler a mensagem em seu armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-123">Update hello `config-azure.json` file so that hello sample code that runs on hello host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="8a0e4-124">tooconfigure Olá conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8a0e4-124">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="8a0e4-125">Arquivo de configuração de dispositivo aberto Olá `config-azure.json` executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a0e4-125">Open hello device configuration file `config-azure.json` by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuração](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="8a0e4-127">Substituir `[Azure storage connection string]` com hello cadeia de caracteres de conexão de armazenamento do Azure que você obteve.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-127">Replace `[Azure storage connection string]` with hello Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="8a0e4-128">`[IoT hub connection string]` já deve ter sido substituído na seção [Ler mensagens do Hub IoT do Azure](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md), na Lição 3.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="8a0e4-129">Ler mensagens no Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="8a0e4-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="8a0e4-130">Execute o aplicativo de exemplo hello gateway e ler mensagens de armazenamento de tabela do Azure por Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a0e4-130">Run hello gateway sample application and read Azure Table storage messages by hello following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="8a0e4-131">O hub IoT dispara a mensagem de toosave do aplicativo de função do Azure em seu armazenamento de tabela do Azure quando a nova mensagem chega.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-131">Your IoT hub triggers your Azure Function application toosave message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="8a0e4-132">Olá `gulp run` comando executa o aplicativo de exemplo do gateway que envia o hub de IoT tooyour mensagens.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-132">hello `gulp run` command runs gateway sample application that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="8a0e4-133">Com `table-storage` parâmetro, ela também gera uma saudação de tooreceive do processo filho salva a mensagem em seu armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-133">With `table-storage` parameter, it also spawns a child process tooreceive hello saved message in your Azure Table storage.</span></span>

<span data-ttu-id="8a0e4-134">mensagens de saudação que estão sendo enviadas e recebidos são todos Olá exibidos imediatamente na mesma janela do console Olá computador host.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-134">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="8a0e4-135">instância de aplicativo de exemplo Hello será encerrado automaticamente em 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-135">hello sample application instance will terminate automatically in 40 seconds.</span></span>

   ![leitura de gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="8a0e4-137">Resumo</span><span class="sxs-lookup"><span data-stu-id="8a0e4-137">Summary</span></span>

<span data-ttu-id="8a0e4-138">Executar mensagens de saudação tooread do código de exemplo hello em seu armazenamento de tabela do Azure salvo pelo seu aplicativo de função do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a0e4-138">You've run hello sample code tooread hello messages in your Azure Table storage saved by your Azure Function application.</span></span>
