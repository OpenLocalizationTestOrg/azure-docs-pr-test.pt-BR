---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Lição 3: monitorar mensagens| Microsoft Docs"
description: "Monitore as mensagens do dispositivo para a nuvem conforme elas são gravadas no armazenamento de tabelas do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados na nuvem, coleta de dados de nuvem, serviço de nuvem iot, dados iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: cad545c3-dd88-486c-a663-d587a924ccd4
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 249b5e0e96051fa2adeedfb9befd98fc939b4d40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="cc033-104">Ler mensagens mantidas no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cc033-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cc033-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="cc033-105">What you will do</span></span>
<span data-ttu-id="cc033-106">Monitorar as mensagens do dispositivo para a nuvem enviadas do Intel Edison para o Hub IoT conforme elas são gravadas no Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc033-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="cc033-107">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="cc033-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cc033-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="cc033-108">What you will learn</span></span>
<span data-ttu-id="cc033-109">Neste artigo, você aprenderá como usar a tarefa read-message do gulp para ler mensagens mantidas no armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc033-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cc033-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="cc033-110">What you need</span></span>
<span data-ttu-id="cc033-111">Antes de iniciar esse processo, você precisa ter concluído com sucesso [Executar o aplicativo de exemplo de piscar do Azure no Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="cc033-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="cc033-112">Ler novas mensagens de sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="cc033-112">Read new messages from your storage account</span></span>
<span data-ttu-id="cc033-113">No artigo anterior, você executou um aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="cc033-113">In the previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="cc033-114">O aplicativo de exemplo envia mensagens para o hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc033-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="cc033-115">As mensagens enviadas para o Hub IoT são armazenadas em seu armazenamento de tabelas do Azure por meio do aplicativo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc033-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="cc033-116">Você precisa da cadeia de conexão do Armazenamento do Azure para ler mensagens de seu armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc033-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="cc033-117">Para ler as mensagens armazenadas em seu armazenamento de tabelas do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="cc033-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="cc033-118">Obtenha a cadeia de conexão executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="cc033-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="cc033-119">O primeiro comando recupera o `storage name` usado no segundo comando para obter a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="cc033-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="cc033-120">Use `iot-sample` como o valor de `{resource group name}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="cc033-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="cc033-121">Abra o arquivo de configuração `config-edison.json` no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cc033-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="cc033-122">Substitua `[Azure storage connection string]` pela cadeia de conexão obtida na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="cc033-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="cc033-123">Salve o arquivo `config-edison.json`.</span><span class="sxs-lookup"><span data-stu-id="cc033-123">Save the `config-edison.json` file.</span></span>
5. <span data-ttu-id="cc033-124">Envie mensagens novamente e leia-as de seu armazenamento de tabelas do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cc033-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="cc033-125">A lógica para leitura do armazenamento de tabelas do Azure está no arquivo `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="cc033-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![gulp run --read-storage][gulp run]

## <a name="summary"></a><span data-ttu-id="cc033-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="cc033-127">Summary</span></span>
<span data-ttu-id="cc033-128">Você conectou com sucesso o Edison ao Hub IoT na nuvem e usou o aplicativo de exemplo de piscar para enviar mensagens do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="cc033-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="cc033-129">Você também usou o aplicativo de funções do Azure para armazenar mensagens do hub IoT recebidas em seu armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc033-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="cc033-130">Agora, é possível enviar mensagens da nuvem para o dispositivo do Hub IoT para o Edison.</span><span class="sxs-lookup"><span data-stu-id="cc033-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc033-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc033-131">Next steps</span></span>
<span data-ttu-id="cc033-132">[Executar um aplicativo de exemplo para receber mensagens da nuvem para o dispositivo][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="cc033-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-c-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message_c.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md