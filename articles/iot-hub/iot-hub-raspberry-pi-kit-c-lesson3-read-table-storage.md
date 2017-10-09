---
title: "Connect Raspberry PI (C) tooAzure IoT – lição 3: armazenamento de tabela | Microsoft Docs"
description: "Monitorar mensagens de saudação do dispositivo para nuvem, como eles são gravados tooyour armazenamento de tabela do Azure."
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
ms.openlocfilehash: 307ce2bc595339790db7379cc011fe262c2b8734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="7c1d9-104">Ler mensagens mantidas no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="7c1d9-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="7c1d9-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="7c1d9-105">What you will do</span></span>
<span data-ttu-id="7c1d9-106">Mensagens de dispositivo para nuvem de saudação do monitor que são enviadas de framboesa Pi 3 tooyour IoT hub como mensagens de saudação são gravadas tooyour armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-106">Monitor hello device-to-cloud messages that are sent from Raspberry Pi 3 tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="7c1d9-107">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d9-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7c1d9-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="7c1d9-108">What you will learn</span></span>
<span data-ttu-id="7c1d9-109">Neste artigo, você aprenderá como mensagens de tooread toouse saudação gulp tarefa Ler mensagem persistente em seu armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7c1d9-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="7c1d9-110">What you need</span></span>
<span data-ttu-id="7c1d9-111">Antes de iniciar esse processo, você deve foi concluído com êxito [executar o aplicativo de exemplo hello intermitência do Azure em framboesa Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="7c1d9-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="7c1d9-112">Ler novas mensagens de sua conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7c1d9-112">Read new messages from your storage account</span></span>
<span data-ttu-id="7c1d9-113">Artigo anterior de saudação, você executou um aplicativo de exemplo em Pi.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-113">In hello previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="7c1d9-114">Olá exemplo aplicativo enviado mensagens tooyour Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="7c1d9-115">mensagens de saudação enviadas tooyour IoT hub são armazenadas em seu armazenamento de tabela do Azure por meio do aplicativo de função do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="7c1d9-116">Você precisa de armazenamento do Azure conexão cadeia de caracteres tooread mensagens de saudação do seu armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="7c1d9-117">mensagens de tooread armazenadas em seu armazenamento de tabela do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="7c1d9-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="7c1d9-118">Obter cadeia de caracteres de conexão Olá executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c1d9-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="7c1d9-119">Olá primeiro comando recupera Olá `storage name` que é usado em Olá segundo comando tooget Olá conexão cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="7c1d9-120">Use `iot-sample` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="7c1d9-121">Arquivo de configuração de saudação abrir `config-raspberrypi.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c1d9-121">Open hello configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="7c1d9-122">Substituir `[Azure storage connection string]` com a cadeia de caracteres de conexão de saudação você obteve na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="7c1d9-123">Salvar Olá `config-raspberrypi.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-123">Save hello `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="7c1d9-124">Enviar mensagens novamente e lê-los do seu armazenamento de tabela do Azure executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c1d9-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="7c1d9-125">Olá lógica para leitura do armazenamento de tabela do Azure está em Olá `azure-table.js` arquivo.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>
   
   ![gulp run --read-storage](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a><span data-ttu-id="7c1d9-127">Resumo</span><span class="sxs-lookup"><span data-stu-id="7c1d9-127">Summary</span></span>
<span data-ttu-id="7c1d9-128">Já conectado Pi tooyour IoT hub de nuvem hello e usado mensagens de dispositivo para nuvem toosend do aplicativo de exemplo de intermitência Olá com êxito.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-128">You've successfully connected Pi tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="7c1d9-129">Você também usou hello Azure função aplicativo toostore entrada IoT hub mensagens tooyour Azure armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="7c1d9-130">Agora você pode enviar mensagens de nuvem para dispositivo de sua tooPi de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7c1d9-130">You can now send cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c1d9-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c1d9-131">Next steps</span></span>
[<span data-ttu-id="7c1d9-132">Executar um tooreceive do aplicativo de exemplo mensagens de nuvem para dispositivo</span><span class="sxs-lookup"><span data-stu-id="7c1d9-132">Run a sample application tooreceive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

