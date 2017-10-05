---
title: "Conectar o Raspberry Pi (Nó) ao IoT do Azure - Lição 3: armazenamento de tabelas | Microsoft Docs"
description: "Monitore as mensagens do dispositivo para a nuvem conforme elas são gravadas no armazenamento de tabelas do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "recuperar dados da nuvem, serviço de nuvem de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8c5558bb-3c31-4445-90e6-b1a978738545
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 16b7f2e38bfe3b40d199cb6e07976433aa54ea32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="5dd4a-104">Ler mensagens mantidas no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5dd4a-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="5dd4a-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="5dd4a-105">What you will do</span></span>
<span data-ttu-id="5dd4a-106">Monitore as mensagens do dispositivo para a nuvem enviadas do Raspberry Pi 3 para o hub IoT conforme elas são gravadas no armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="5dd4a-107">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5dd4a-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5dd4a-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="5dd4a-108">What you will learn</span></span>
<span data-ttu-id="5dd4a-109">Neste artigo, você aprenderá como usar a tarefa read-message do gulp para ler mensagens mantidas no armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5dd4a-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="5dd4a-110">What you need</span></span>
<span data-ttu-id="5dd4a-111">Antes de iniciar esse processo você deve ter concluído com sucesso [Executar o aplicativo de exemplo de piscar do Azure em seu Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="5dd4a-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="5dd4a-112">Ler novas mensagens de sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5dd4a-112">Read new messages from your storage account</span></span>
<span data-ttu-id="5dd4a-113">No artigo anterior, você executou um aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="5dd4a-114">O aplicativo de exemplo envia mensagens para o hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="5dd4a-115">As mensagens enviadas para o Hub IoT são armazenadas em seu armazenamento de tabelas do Azure por meio do aplicativo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="5dd4a-116">Você precisa da cadeia de conexão do Armazenamento do Azure para ler mensagens de seu armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="5dd4a-117">Para ler as mensagens armazenadas em seu armazenamento de tabelas do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5dd4a-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="5dd4a-118">Obtenha a cadeia de conexão executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5dd4a-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="5dd4a-119">O primeiro comando recupera o `storage name` usado no segundo comando para obter a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="5dd4a-120">Use `iot-sample` como o valor de `{resource group name}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="5dd4a-121">Abra o arquivo de configuração `config-raspberrypi.json` no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5dd4a-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="5dd4a-122">Substitua `[Azure storage connection string]` pela cadeia de conexão obtida na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="5dd4a-123">Salve o arquivo `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="5dd4a-124">Envie mensagens novamente e leia-as de seu armazenamento de tabelas do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5dd4a-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="5dd4a-125">A lógica para leitura do armazenamento de tabelas do Azure está no arquivo `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
   ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a><span data-ttu-id="5dd4a-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="5dd4a-127">Summary</span></span>
<span data-ttu-id="5dd4a-128">Você conectou com sucesso o Pi ao Hub IoT na nuvem e usou o aplicativo de exemplo de piscar para enviar mensagens do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="5dd4a-129">Você também usou o aplicativo de funções do Azure para armazenar mensagens do hub IoT recebidas em seu armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="5dd4a-130">Agora você pode enviar mensagens de nuvem para dispositivo do Hub IoT para o Pi.</span><span class="sxs-lookup"><span data-stu-id="5dd4a-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dd4a-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5dd4a-131">Next steps</span></span>
[<span data-ttu-id="5dd4a-132">Executar um aplicativo de exemplo para receber mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="5dd4a-132">Run a sample application to receive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

