---
title: Passo a passo da Captura de Hubs de Eventos do Azure | Microsoft Docs
description: Exemplo que usa o SDK do Python do Azure para demonstrar o uso do recurso Captura de Hubs de Eventos.
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: a764a116755c20f60e92e553bd7c896425272b85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="b56f2-103">Passo a passo da Captura de Hubs de Eventos: Python</span><span class="sxs-lookup"><span data-stu-id="b56f2-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="b56f2-104">A Captura de Hubs de Eventos é um recurso dos Hubs de Eventos que habilita o fornecimento automático dos dados de streaming no Hub de Eventos para uma conta de Armazenamento de Blobs do Azure desejada.</span><span class="sxs-lookup"><span data-stu-id="b56f2-104">Event Hubs Capture is a feature of Event Hubs that enables you to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span></span> <span data-ttu-id="b56f2-105">Essa capacidade facilita a execução de processamento em lote na transmissão de dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="b56f2-105">This capability makes it easy to perform batch processing on real-time streaming data.</span></span> <span data-ttu-id="b56f2-106">Este artigo descreve como usar a Captura de Hubs de Eventos com o Python.</span><span class="sxs-lookup"><span data-stu-id="b56f2-106">This article describes how to use Event Hubs Capture with Python.</span></span> <span data-ttu-id="b56f2-107">Para saber mais sobre a Captura de Hubs de Eventos, confira o [artigo de visão geral](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b56f2-107">For more information about Event Hubs Capture, see the [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="b56f2-108">Este exemplo usa o [SDK para Python do Azure](https://azure.microsoft.com/develop/python/) para demonstrar o recurso de Captura.</span><span class="sxs-lookup"><span data-stu-id="b56f2-108">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature.</span></span> <span data-ttu-id="b56f2-109">O programa sender.py envia telemetria de ambiente simulado para os Hubs de Eventos no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="b56f2-109">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span></span> <span data-ttu-id="b56f2-110">O Hub de Eventos está configurado para usar o recurso de Captura a fim de gravar esses dados no Armazenamento de Blobs em lotes.</span><span class="sxs-lookup"><span data-stu-id="b56f2-110">The event hub is configured to use the Capture feature to write this data to blob storage in batches.</span></span> <span data-ttu-id="b56f2-111">Em seguida, o aplicativo capturereader.py lê esses blobs e cria um arquivo de acréscimo por dispositivo e grava os dados em arquivos. csv.</span><span class="sxs-lookup"><span data-stu-id="b56f2-111">The capturereader.py app then reads these blobs and creates an append file per device, then writes the data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="b56f2-112">O que será realizado</span><span class="sxs-lookup"><span data-stu-id="b56f2-112">What will be accomplished</span></span>

1. <span data-ttu-id="b56f2-113">Criar uma conta de Armazenamento de Blobs do Azure e um contêiner de blobs dentro dela, usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b56f2-113">Create an Azure Blob Storage account and a blob container within it, using the Azure portal.</span></span>
2. <span data-ttu-id="b56f2-114">Criar um namespace do Hub de Eventos usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b56f2-114">Create an Event Hub namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="b56f2-115">Crie um Hub de Eventos com o recurso de Captura habilitado, usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b56f2-115">Create an event hub with the Capture feature enabled, using the Azure portal.</span></span>
4. <span data-ttu-id="b56f2-116">Envie dados para o Hub de Eventos com um script Python.</span><span class="sxs-lookup"><span data-stu-id="b56f2-116">Send data to the event hub with a Python script.</span></span>
5. <span data-ttu-id="b56f2-117">Leia os arquivos da captura e processe-os com outro script Python.</span><span class="sxs-lookup"><span data-stu-id="b56f2-117">Read the files from the capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b56f2-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b56f2-118">Prerequisites</span></span>

- <span data-ttu-id="b56f2-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="b56f2-119">Python 2.7.x</span></span>
- <span data-ttu-id="b56f2-120">Uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="b56f2-120">An Azure subscription</span></span>
- <span data-ttu-id="b56f2-121">Um [Namespace de Hubs de Eventos e Hub de Eventos ativos.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="b56f2-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="b56f2-122">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b56f2-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="b56f2-123">Faça logon no [Portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b56f2-123">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="b56f2-124">No painel de navegação esquerdo do portal, clique em **Novo**, em **Armazenamento** e em **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="b56f2-124">In the left navigation pane of the portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="b56f2-125">Preencha os campos na folha da conta de armazenamento e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b56f2-125">Complete the fields in the storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="b56f2-126">Depois de ver a mensagem **Implantações Bem-sucedidas**, clique no nome da nova conta de armazenamento e, na folha **Fundamentos**, clique em **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="b56f2-126">After you see the **Deployments Succeeded** message, click the name of the new storage account and in the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="b56f2-127">Quando a folha **Serviço Blob** abrir, clique em **+ Contêiner** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="b56f2-127">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="b56f2-128">Nomeie o contêiner **captura** e feche a folha do **Serviço Blob**.</span><span class="sxs-lookup"><span data-stu-id="b56f2-128">Name the container **capture**, then close the **Blob service** blade.</span></span>
5. <span data-ttu-id="b56f2-129">Clique em **Chaves de acesso** na folha esquerda e copie o nome da conta de armazenamento e o valor de **key1**.</span><span class="sxs-lookup"><span data-stu-id="b56f2-129">Click **Access keys** in the left blade and copy the name of the storage account and the value of **key1**.</span></span> <span data-ttu-id="b56f2-130">Salve esses valores no Bloco de notas ou em outro local temporário.</span><span class="sxs-lookup"><span data-stu-id="b56f2-130">Save these values to Notepad or some other temporary location.</span></span>

## <a name="create-a-python-script-to-send-events-to-your-event-hub"></a><span data-ttu-id="b56f2-131">Criar um script Python para enviar eventos a seu Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="b56f2-131">Create a Python script to send events to your event hub</span></span>
1. <span data-ttu-id="b56f2-132">Abra seu editor de Python favorito, como o [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="b56f2-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="b56f2-133">Crie um script chamado **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="b56f2-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="b56f2-134">Esse script envia 200 eventos para seu hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="b56f2-134">This script sends 200 events to your event hub.</span></span> <span data-ttu-id="b56f2-135">Eles são simples leituras de ambiente enviadas em JSON.</span><span class="sxs-lookup"><span data-stu-id="b56f2-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="b56f2-136">Cole o seguinte código em sender.py:</span><span class="sxs-lookup"><span data-stu-id="b56f2-136">Paste the following code into sender.py:</span></span>
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. <span data-ttu-id="b56f2-137">Atualize o código anterior para usar o nome do namespace, o valor de chave e o nome do hub de eventos obtidos ao criar o namespace dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="b56f2-137">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span></span>

## <a name="create-a-python-script-to-read-your-capture-files"></a><span data-ttu-id="b56f2-138">Criar um script Python para ler os arquivos da Captura</span><span class="sxs-lookup"><span data-stu-id="b56f2-138">Create a Python script to read your Capture files</span></span>

1. <span data-ttu-id="b56f2-139">Preencha a folha e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b56f2-139">Fill out the blade and click **Create**.</span></span>
2. <span data-ttu-id="b56f2-140">Criar um script chamado **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="b56f2-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="b56f2-141">Esse script lê os arquivos capturados e cria um arquivo por dispositivo para gravar os dados somente para esse dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b56f2-141">This script reads the captured files and creates a file per device to write the data only for that device.</span></span>
3. <span data-ttu-id="b56f2-142">Cole o código abaixo no capturereader.py:</span><span class="sxs-lookup"><span data-stu-id="b56f2-142">Paste the following code into capturereader.py:</span></span>
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. <span data-ttu-id="b56f2-143">Não se esqueça de colar os valores apropriados do nome da sua conta de armazenamento e da chave na chamada para `startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="b56f2-143">Be sure to paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span></span>

## <a name="run-the-scripts"></a><span data-ttu-id="b56f2-144">Executar os scripts</span><span class="sxs-lookup"><span data-stu-id="b56f2-144">Run the scripts</span></span>
1. <span data-ttu-id="b56f2-145">Abra um prompt de comando com o Python em seu caminho e execute estes comandos para instalar os pacotes de pré-requisito do Python:</span><span class="sxs-lookup"><span data-stu-id="b56f2-145">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="b56f2-146">Se você tiver uma versão anterior do Azure ou do Armazenamento do Azure, talvez precise usar a opção **--upgrade**</span><span class="sxs-lookup"><span data-stu-id="b56f2-146">If you have an earlier version of either azure-storage or azure, you may need to use the **--upgrade** option</span></span>
   
  <span data-ttu-id="b56f2-147">Você também precisa executar o seguinte (desnecessário na maioria dos sistemas):</span><span class="sxs-lookup"><span data-stu-id="b56f2-147">You might also need to run the following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="b56f2-148">Altere o diretório para o qual você salvou sender.py e capturereader.py e execute este comando:</span><span class="sxs-lookup"><span data-stu-id="b56f2-148">Change your directory to wherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="b56f2-149">Esse comando inicia um novo processo de Python para executar o remetente.</span><span class="sxs-lookup"><span data-stu-id="b56f2-149">This command starts a new Python process to run the sender.</span></span>
3. <span data-ttu-id="b56f2-150">Agora, aguarde alguns minutos para que a captura seja executada.</span><span class="sxs-lookup"><span data-stu-id="b56f2-150">Now wait a few minutes for the capture to run.</span></span> <span data-ttu-id="b56f2-151">Em seguida, digite o seguinte comando na janela de comando original:</span><span class="sxs-lookup"><span data-stu-id="b56f2-151">Then type the following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="b56f2-152">Esse processador de captura usa o diretório local para baixar todos os blobs do contêiner/da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b56f2-152">This capture processor uses the local directory to download all the blobs from the storage account/container.</span></span> <span data-ttu-id="b56f2-153">Ele processa todos os que não estão vazios e grava os resultados como arquivos .csv no diretório local.</span><span class="sxs-lookup"><span data-stu-id="b56f2-153">It processes any that are not empty, and writes the results as .csv files into the local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b56f2-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b56f2-154">Next steps</span></span>

<span data-ttu-id="b56f2-155">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="b56f2-155">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="b56f2-156">[Visão Geral da Captura de Hubs de Eventos][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="b56f2-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="b56f2-157">Um [aplicativo de exemplo completo que usa os Hubs de Eventos][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="b56f2-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="b56f2-158">O exemplo de [Escala horizontal do processamento de eventos com Hubs de Eventos][Scale out Event Processing with Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="b56f2-158">The [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="b56f2-159">[Visão Geral dos Hubs de Eventos][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="b56f2-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
