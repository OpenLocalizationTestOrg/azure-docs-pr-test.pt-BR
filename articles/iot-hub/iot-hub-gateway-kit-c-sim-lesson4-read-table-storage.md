---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 4: armazenamento de tabelas | Microsoft Docs"
description: Salve mensagens da NUC da Intel para o hub IoT, grave-as no Armazenamento de Tabelas do Azure e, em seguida, leia-as na nuvem.
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
ms.openlocfilehash: de5fae794c195132e2a487c0095845c756aa28e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="eb0aa-104">Ler mensagens mantidas no Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="eb0aa-104">Read messages persisted in Azure Table storage</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="eb0aa-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="eb0aa-105">What you will do</span></span>

- <span data-ttu-id="eb0aa-106">Execute o aplicativo de exemplo de gateway no gateway que envia mensagens ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-106">Run the gateway sample application on your gateway that sends messages to your IoT hub.</span></span>
- <span data-ttu-id="eb0aa-107">Execute um código de exemplo no computador host para ler mensagens no seu Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-107">Run sample code on your host computer to read messages in your Azure Table storage.</span></span>

<span data-ttu-id="eb0aa-108">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="eb0aa-108">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eb0aa-109">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="eb0aa-109">What you will learn</span></span>

<span data-ttu-id="eb0aa-110">Como usar a ferramenta gulp para executar o código de exemplo para ler mensagens no Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-110">How to use the gulp tool to run the sample code to read messages in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eb0aa-111">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="eb0aa-111">What you need</span></span>

<span data-ttu-id="eb0aa-112">Você realizou as seguintes tarefas com êxito:</span><span class="sxs-lookup"><span data-stu-id="eb0aa-112">You have have successfully done the following tasks:</span></span>

- <span data-ttu-id="eb0aa-113">[O aplicativo de funções do Azure e a conta de armazenamento do Azure foram criados](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="eb0aa-113">[Created the Azure function app and the Azure storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span></span>
- <span data-ttu-id="eb0aa-114">[Executar o aplicativo de exemplo do gateway](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="eb0aa-114">[Run the gateway sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>
- <span data-ttu-id="eb0aa-115">[Ler mensagens do Hub IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span><span class="sxs-lookup"><span data-stu-id="eb0aa-115">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md).</span></span>

## <a name="get-your-azure-storage-connection-strings"></a><span data-ttu-id="eb0aa-116">Obtenha cadeias de conexão do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="eb0aa-116">Get your Azure storage connection strings</span></span>

<span data-ttu-id="eb0aa-117">No início desta lição, você criou com êxito uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-117">Early in this lesson, you successfully created an Azure storage account.</span></span> <span data-ttu-id="eb0aa-118">Para obter a cadeia de conexão da conta de armazenamento do Azure, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="eb0aa-118">To get the connection string of the Azure storage account, run the following commands:</span></span>

* <span data-ttu-id="eb0aa-119">Liste todas suas contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-119">List all your storage accounts.</span></span>

```bash
az storage account list -g iot-gateway --query [].name
```

* <span data-ttu-id="eb0aa-120">Obtenha a cadeia de conexão do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-120">Get azure storage connection string.</span></span>

```bash
az storage account show-connection-string -g iot-gateway -n {storage name}
```

<span data-ttu-id="eb0aa-121">Use `iot-gateway` como o valor de `{resource group name}` se não tiver alterado o valor na Lição 2.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-121">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="eb0aa-122">Configurar a conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="eb0aa-122">Configure the device connection</span></span>

<span data-ttu-id="eb0aa-123">Atualize o arquivo `config-azure.json` para que o código de exemplo executado no computador host possa ler mensagens no Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-123">Update the `config-azure.json` file so that the sample code that runs on the host computer can read message in your Azure Table storage.</span></span> <span data-ttu-id="eb0aa-124">Para configurar a conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="eb0aa-124">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="eb0aa-125">Abra o arquivo de configuração do dispositivo `config-azure.json` executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="eb0aa-125">Open the device configuration file `config-azure.json` by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

   ![configuração](media/iot-hub-gateway-kit-lessons/lesson4/config_azure.png)

2. <span data-ttu-id="eb0aa-127">Substitua `[Azure storage connection string]` pela cadeia de conexão do armazenamento do Azure que você obteve.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-127">Replace `[Azure storage connection string]` with the Azure storage connection string that you obtained.</span></span>

   <span data-ttu-id="eb0aa-128">`[IoT hub connection string]` já deve ter sido substituído na seção [Ler mensagens do Hub IoT do Azure](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md), na Lição 3.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-128">`[IoT hub connection string]` should already be replaced in section [Read messages from Azure IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) in Lesson3.</span></span>

## <a name="read-messages-in-your-azure-table-storage"></a><span data-ttu-id="eb0aa-129">Ler mensagens no Armazenamento de Tabelas do Azure</span><span class="sxs-lookup"><span data-stu-id="eb0aa-129">Read messages in your Azure Table storage</span></span>

<span data-ttu-id="eb0aa-130">Execute o aplicativo de exemplo no gateway e leia as mensagens de armazenamento de tabelas do Azure executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="eb0aa-130">Run the gateway sample application and read Azure Table storage messages by the following command:</span></span>

```bash
gulp run --table-storage
```

<span data-ttu-id="eb0aa-131">O Hub IoT dispara o aplicativo de Funções do Azure para salvar a mensagem no Armazenamento de Tabelas do Azure quando a nova mensagem chega.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-131">Your IoT hub triggers your Azure Function application to save message into your Azure Table storage when new message arrives.</span></span>
<span data-ttu-id="eb0aa-132">O comando `gulp run` executa o aplicativo de exemplo no gateway que envia mensagens ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-132">The `gulp run` command runs gateway sample application that sends messages to your IoT hub.</span></span> <span data-ttu-id="eb0aa-133">Com o parâmetro `table-storage`, ele também gera um processo filho para receber a mensagem salva no Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-133">With `table-storage` parameter, it also spawns a child process to receive the saved message in your Azure Table storage.</span></span>

<span data-ttu-id="eb0aa-134">As mensagens que estão sendo enviadas e recebidas são todas exibidas instantaneamente na mesma janela de console no computador host.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-134">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="eb0aa-135">A instância do aplicativo de exemplo será encerrada automaticamente em 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-135">The sample application instance will terminate automatically in 40 seconds.</span></span>

   ![leitura de gulp](media/iot-hub-gateway-kit-lessons/lesson4/gulp_run_read_table_simudev.png)


## <a name="summary"></a><span data-ttu-id="eb0aa-137">Resumo</span><span class="sxs-lookup"><span data-stu-id="eb0aa-137">Summary</span></span>

<span data-ttu-id="eb0aa-138">Você executou o código de exemplo para ler as mensagens no Armazenamento de Tabelas do Azure salvas pelo aplicativo de Funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0aa-138">You've run the sample code to read the messages in your Azure Table storage saved by your Azure Function application.</span></span>
